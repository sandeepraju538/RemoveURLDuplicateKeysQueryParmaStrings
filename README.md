# RemoveURLDuplicateKeysQueryParmaStrings

Jquery: 

***function removeDuplicate(url) {
  url = decodeURIComponent(url);                  // decode the url,remove %5B becomes
  var query = url.split('?')[1];                  // get only the query
  var parts = query.split('&');                  // split the query into parts
  var params = {};
  for (var i = 0; i < parts.length; i++) {
    var nv = parts[i].split('=');
    if (!nv[0]) continue;
    var value = nv[1] || true;
    if (params[nv[0]] && params[nv[0]].indexOf(value)) {
      params[nv[0]].push(value);
    } else {
      params[nv[0]] = [value];
    }
  }
  url = url.split('?')[0] + '?';
  var keys = Object.keys(params);
  for (var i = 0; i < keys.length; i++) {
    url += keys[i] + '=' + params[keys[i]].join('+');
    if (i !== keys.length - 1) url += '&';
  }
  return url;
}***

Higher order function(filter): most recommended
const link = "http://example.com/?foo=42&bar=43&foo=42&bar=43"
const params = link.replace(/.*\?/g, '')                    // replace everything before '?'
                   .split('&')                              // split by '&'
                   .filter((e, i, a) => a.indexOf(e) === i) // filter duplicates
                   .join('&')                               // join by '&'
const res = link.replace(/\?.*/g, '?' + params)             // replace link params with params without duplicates
console.log(res)
