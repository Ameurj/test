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
  function makeAjaxRequest() {
    var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function() {
      if (xhr.readyState === 4) {
        if (xhr.status === 200) {
          var responseText = xhr.responseText;
          console.log('Response Payload:', responseText);
          // Perform further processing with the response payload
        } else if (xhr.status === 302) {
          var redirectedUrl = xhr.getResponseHeader('Location');
          console.log('Redirected URL:', redirectedUrl);
          // Perform further processing with the redirected URL
        }
      }
    };

    // Set up the AJAX request
    xhr.open('GET', 'URL_OF_REQUEST', true);
    xhr.send();
  }

  makeAjaxRequest();
</script>
