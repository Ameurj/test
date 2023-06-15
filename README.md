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
  (function() {
    var originalFetch = window.fetch;
    window.fetch = function(resource, init) {
      return originalFetch(resource, init)
        .then(function(response) {
          var url = response.url;
          if (url.includes('/search?SearchTerm=')) {
            var searchTerm = new URL(url).searchParams.get('SearchTerm');
            window.dataLayer = window.dataLayer || [];
            window.dataLayer.push({
              'event': 'website_search',
              'searchTerm': searchTerm
            });
          }
          return response;
        });
    };
  })();
</script>
