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
  function makeAjaxRequest(requestName) {
    var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function() {
      if (xhr.readyState === 4) {
        var responseText = xhr.responseText;
        console.log('Response Payload:', responseText);
        // Perform further processing with the response payload

        // Push data layer event indicating successful request
        dataLayer.push({
          'event': 'test_success',
          'requestName': requestName
        });
      }
    };

    // Set up the AJAX request
    xhr.open('GET', requestName, true);
    xhr.send();
  }

  // Filter the requests based on their names
  var requestNamePattern = 'https://www.shophighlinewarren.com/search?SearchTerm=';
  var requests = performance.getEntriesByType('resource');
  requests.forEach(function(request) {
    if (request.name.includes(requestNamePattern)) {
      makeAjaxRequest(request.name);
    }
  });
</script>
