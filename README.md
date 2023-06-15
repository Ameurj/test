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
var testURL = 'https://www.example.com/search?SearchTerm=test';
var testRequest = new XMLHttpRequest();
testRequest.open('GET', testURL);
testRequest.send();

setTimeout(function() {
  var requests = performance.getEntriesByType('resource');
  requests.forEach(function(request) {
    if (request.name.includes(testURL)) {
      console.log('Matching Request:', request.name);
    }
  });
}, 1000);
