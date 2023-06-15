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
  window.addEventListener('popstate', function() {
    var searchTerm = new URL(window.location.href).searchParams.get('SearchTerm');
    if (searchTerm) {
      window.dataLayer = window.dataLayer || [];
      window.dataLayer.push({
        'event': 'website_search',
        'searchTerm': searchTerm
      });
    }
  });
</script>
