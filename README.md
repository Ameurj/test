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




var requestNamePattern = /oilandlubricants/;
var requests = performance.getEntriesByType('resource');
requests.forEach(function(request) {
  if (request.name.match(requestNamePattern)) {
    console.log('Matching Request:', request.name);
  }
});
