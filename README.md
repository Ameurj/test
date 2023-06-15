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




var requestNamePattern = 'oilandlubricants';
var requests = performance.getEntriesByType('resource');
var matchingRequests = requests.filter(function(request) {
  return request.name.includes(requestNamePattern);
});

if (matchingRequests.length > 0) {
  console.log('Matching Requests:');
  matchingRequests.forEach(function(request) {
    console.log(request.name);
  });
} else {
  console.log('No matching requests found.');
}
