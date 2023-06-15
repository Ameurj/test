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






var testURL = 'https://www.shophighlinewarren.com/search?SearchTerm=test';
var testRequest = new XMLHttpRequest();
testRequest.open('GET', testURL);
testRequest.send();

setTimeout(function() {
  var entries = performance.getEntries();
  entries.forEach(function(entry) {
    if (entry.name.includes(testURL) && entry.initiatorType === 'document' && entry.transferSize === 0) {
      console.log('Matching Request:', entry.name);
    }
  });
}, 1000);
