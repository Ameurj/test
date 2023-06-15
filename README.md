function() {
  var searchTerms = [];

  // Attach event listener to capture search term
  window.addEventListener('fetch', function(event) {
    var url = event.request.url;
    if (url.includes('/search?Searchterm=')) {
      var searchTerm = new URL(url).searchParams.get('Searchterm');
      searchTerms.push(searchTerm);
      
      // Push event to the data layer
      dataLayer.push({
        'event': 'website_search',
        'searchTerm': searchTerm
      });
    }
  });

  // Return the captured search term(s)
  return searchTerms.join(', ');
}

<script>
  window.addEventListener('fetch', function(event) {
    var requestName = event.request.url;
    var searchTerm = null;

    if (requestName.includes('search?SearchTerm=')) {
      var queryString = requestName.split('?')[1];
      var params = new URLSearchParams(queryString);
      searchTerm = params.get('SearchTerm');
    }

    if (searchTerm) {
      window.dataLayer = window.dataLayer || [];
      window.dataLayer.push({
        'event': 'website_search',
        'searchTerm': searchTerm
      });
    }
  });
</script>
