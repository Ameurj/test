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
  function captureReferrerLink() {
    var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function() {
      if (xhr.readyState === 4 && xhr.status === 200) {
        var referrerLink = xhr.getResponseHeader('Referer');
        console.log('Referrer Link:', referrerLink);
        // Extract the search term from the referrer link
        var searchQuery = extractSearchTermFromReferrerLink(referrerLink);
        console.log('Search term:', searchQuery);
        // Perform any necessary actions with the captured search term
      }
    };

    // Make the request to the redirected page
    xhr.open('GET', 'URL_OF_REDIRECTED_PAGE', true);
    xhr.send();
  }

  // Helper function to extract the search term from the referrer link
  function extractSearchTermFromReferrerLink(referrerLink) {
    // Implement your logic to extract the search term from the referrer link
    // Return the extracted search term
  }

  captureReferrerLink();
</script>
