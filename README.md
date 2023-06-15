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
  function captureRedirectedURL() {
    var a = document.createElement('a');
    a.href = document.location.href;
    var redirectedURL = a.href;
    console.log('Redirected URL:', redirectedURL);
    // Perform any necessary actions with the captured redirected URL
    // You can extract the search term or pass it to the redirected page
  }
  
  captureRedirectedURL();
</script>
