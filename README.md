function() {
  var url = {{file download - file name}}; // Replace with your data layer variable name
  var fileName = url.substring(url.lastIndexOf('/') + 1);
  return fileName;
}



