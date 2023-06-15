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



var requestNamePattern = 'search?SearchTerm=';
var requests = performance.getEntriesByType('resource');
requests.forEach(function(request) {
  if (request.name.includes(requestNamePattern)) {
    var searchTerm = request.name.match(/search\?SearchTerm=(.*?)&search=/)[1];
    console.log('Matching Request:', request.name);
    console.log('Search Term:', searchTerm);
  }
});
