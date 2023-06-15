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
    event.request.clone().text().then(function(text) {
      var url = event.request.url;
      if (url.includes('/search?SearchTerm=')) {
        var searchTerm = new URL(url).searchParams.get('SearchTerm');
        window.dataLayer = window.dataLayer || [];
        window.dataLayer.push({
          'event': 'website_search',
          'searchTerm': searchTerm
        });
      }
    });
  });
</script>
