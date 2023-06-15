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


<script id="gtm-jq-ajax-listen" type="text/javascript">
(function() {
  'use strict';

  function bindToAjaxSearch() {
    // Add your AJAX search event binding code here
    // ...

    // Customize the attributes to include search-specific data
    dataLayer.push({
      'event': 'searchComplete',
      'attributes': {
        'searchQuery': opts.data, // Example: Capture the search query parameter
        'response': (jqXhr.responseJSON || jqXhr.responseXML || jqXhr.responseText || '')
        // Add other relevant attributes specific to the search
      }
    });
  }

  function init(n) {
    // Ensure jQuery is available before anything
    if (typeof jQuery !== 'undefined') {
      // Define our $ shortcut locally
      var $ = jQuery;
      bindToAjaxSearch();
    } else if (n < 20) {
      n++;
      setTimeout(function() {
        init(n);
      }, 500);
    }
  }

  // Initialize the function
  init(0);
})();
</script>
