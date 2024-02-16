# Curl Commands and Snips
The terminal allows us many functions that can be beneficial to our workflow. Perhaps you've made use of the `curl` command to make HTTP requests. In this article we aim to share some snippets you can add to your arsenal, inspired by the ingenious Julia Evans and her set of brain-teasing [Curl exercises](https://jvns.ca/blog/2019/08/27/curl-exercises/). 
#### Exercise 1: Request https://httpbin.org  from [Curl exercises](https://jvns.ca/blog/2019/08/27/curl-exercises/) `curl cmd`
**Snip you can use:** “Curl-url”: `curl ${url}`

**Input**
```
curl https://httpbin.org
```
**Output**
```html
<!DOCTYPE html>                     
<html lang="en">                                    
<head>
<meta charset="UTF-8">
<title>httpbin.org</title>           
<link href="https://fonts.googleapis.com/css?family=Open+Sans:400,700|Source+Code+Pro:300,600|Titillium+Web:400,600,700"rel="stylesheet">
<!-- Rest of the code for this page...-->
```
   ***Solution Explanation:*** This command sends a basic GET request to https://httpbin.org, a service that provides test endpoints for HTTP requests. The default behavior of `curl` is to perform a GET request, and in this case, it fetches the content from the specified URL.
#### Exercise 2: Request https://httpbin.org/anything. httpbin.org/anything will look at the request you made, parse it, and echo back to you what you requested. curl’s default is to make a GET request
**Snip you can use:** Reuse previous snip with `-i` flag

**Input**  
```bash
curl -i https://httpbin.org/anything
```
**Output**
```bash
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept": "*/*", 
    "Host": "httpbin.org", 
    "User-Agent": "curl/8.2.1", 
   #Rest of the code for this page
```
   ***Solution Explanation:*** Here, the `-i` flag is added to the `curl` command, enhancing the output by including the HTTP headers in the response. This request is directed to https://httpbin.org/anything, a special endpoint designed to inspect and echo back the details of the received request. The `-i` flag allows us to see not only the response body but also the headers, providing a more comprehensive view of the server response.
#### Exercise 3: Make a POST request to https://httpbin.org/anything
**Snip you can use:** “curl/post-request”: `curl -X POST -d ${data} ${url} `
**Note**: data flag, `-d` is optional

**Input** 
```bash
curl -X POST -d "key=value" https://httpbin.org/anything
```
**Output**
```bash
  #Rest of the code for this page
  "json": null, 
  "method": "POST", 
  "origin": "XXX.XXX.XXX.XX", 
  "url": "https://httpbin.org/anything"
}
```
   ***Solution Explanation:*** This command makes use of the `-X` flag to specify the HTTP method as POST, and the `-d` flag to include data in the request body. In this case, the data "key=value" is sent as part of the POST request to https://httpbin.org/anything. This exercise demonstrates how to use `curl` for making POST requests and sending data to a specific endpoint. **Note:** the method compared to the last curl, has changed from `GET` to `POST`.
#### Exercise 4: Make a GET request to https://httpbin.org/anything, but this time add some query parameters (set `value`=`panda`)
**Snip you can use:** "curl/request-with-query": `curl -X {GET|POST|PUT..} -d “${key}=${value}’ ${url}`

"curl/request-with-flags": `curl -X ${GET|POST...} ${--verbose} -d ${data} ${url}`

**Input** 
```bash
curl -X GET -d "value=panda" https://httpbin.org/anything
```
**Output**
```bash
{
  "args": {
    "value": "panda"
  }, 
  "data": "", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept": "*/*", 
   #Rest of the code for this page
```
   ***Solution Explanation:*** The `-d` flag is used to add data to the request, and in this case, the query parameter "value=panda" is attached.
#### Exercise 5: Request google’s robots.txt file (www.google.com/robots.txt)
**Snip you can use:** “Curl-url” 
   
   **Input** 
   ```bash
   curl https://www.google.com/robots.txt
   ```
**Output**
```bash
User-agent: *
Disallow: /search
Allow: /search/about
Allow: /search/static
Allow: /search/howsearchworks
Disallow: /sdch
Disallow: /groups
#Rest of the code for this page
```
   ***Solution Explanation:*** In this straightforward command, `curl` is used to fetch the robots.txt file from Google's domain, which often contains directives for web crawlers.
#### Exercise 6: Make a GET request to https://httpbin.org/anything and set the header `User-Agent: elephant`
**Snip you can use:** Curl/request-with-header: `curl -H "${Header-Name}: ${Header-Value}" ${url}`

**Input** 
```bash
curl -H "User-Agent: elephant" https://httpbin.org/anything
```
**Output**
```bash
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept": "*/*", 
    "Host": "httpbin.org", 
    "User-Agent": "elephant", 
   #Rest of the code for this page
```
   ***Solution Explanation:*** The `-H` flag is used to include a custom header in the `curl` request. In this case, we set the "User-Agent" header to "elephant".
#### Exercise 7: Make a DELETE request to https://httpbin.org/anything
**Snip you can use:** "curl/request": `curl -X ${GET|POST|DELETE|PATCH} ${url}`

**Input** 
```bash
curl -X DELETE https://httpbin.org/anything
```
**Output**
```bash
#Rest of the code for this page
 "json": null, 
  "method": "DELETE", 
  "origin": "XXX.XXX.XXX.XX", 
  "url": "https://httpbin.org/anything"
}

```
   ***Solution Explanation:*** By utilizing the `-X` flag, this command specifies the HTTP method as DELETE. The request is sent to https://httpbin.org/anything, showcasing how `curl` can be employed to make DELETE requests to a specific endpoint. This exercise highlights the simplicity of making requests with different HTTP methods. **Note:** the method is `DELETE`.
#### Exercise 8: Request https://httpbin.org/anything and also get the response headers ****
Use the `-i` flag!

**Input** 
```bash
curl -i https://httpbin.org/anything
```
**Output**
```bash
HTTP/2 200 
date: Day, XX Mon 2024 XX:XX:XX GMT
content-type: application/json
content-length: 343
server: gunicorn/19.9.0
access-control-allow-origin: *
access-control-allow-credentials: true

{
  "args": {}, 
  #Rest of the code for this page
```
   ***Solution Explanation:*** Similar to Exercise 2, the `-i` flag is employed here to include the HTTP headers in the response. We will use `curl/request-debug` snip later on that gives more information. 
#### Exercise 9: Make a POST request to https://httpbin.org/anything with the JSON body `value: panda`
**Snip you can use:**
"curl/request-json":  `curl --json {“${key}”: “${value}”} ${url}` 
"curl/request-json-from-file": `curl --json @${json-filename} ${url}`

**Input** 
```bash
curl --json '{"value": "panda"}' https://httpbin.org/anything
OR
curl --json @json.txt https://httpbin.org/anything
```
**Output**
```bash
  #...
  "files": {}, 
  "form": {
    "{\"value\": \"panda\"}": ""
  }, 
  "headers": {
    "Accept": "*/*", 
    "Content-Length": "18", 
    "Content-Type": "application/x-www-form-urlencoded", 
   #Rest of the code for this page
```
   ***Solution Explanation:*** Here, the `--json` flag sends a POST request and automatically sets `-H` and `-d` to JSON data input.
#### Exercise 10: Make the same POST request as the previous exercise, but set the Content-Type header to `application/json` (because POST requests need to have a content type that matches their body). Look at the `json` field in the response to see the difference from the previous one
**Snip you can use:** Reuse the curl/request-json

**Input**
```bash
curl --json '{"value": "panda"}' https://httpbin.org/anything
```
**Output**
```bash
  "data": "{\"value\": \"panda\"}", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept": "application/json", 
    "Content-Length": "18", 
    "Content-Type": "application/json", 
   #Rest of the code for this page
```
   ***Solution Explanation:*** Like Exercise 9, this command is identical thanks to `--json`.
#### Exercise 11: Make a GET request to https://httpbin.org/anything and set the header `Accept-Encoding: gzip` (what happens? why?)
**Snip you can use:** "Curl-custom-header-accept": `curl -H "Accept-${Encoding|Language}: ${Header-Value}" ${url}` 
    
**Input**
```bash
curl -H "Accept-Encoding: gzip" https://httpbin.org/anything
```
**Output**
```bash
"args": {}, 
  "data": "", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept": "*/*", 
    "Accepting-Encoding": "gzip",
  #Rest of the code for this page
```
   ***Solution Explanation:*** This command sends a GET request while specifying the "Accept-Encoding" header as "gzip." The server may respond with a compressed gzip file if it supports gzip compression, reducing the size of the response and improving transfer speed. **Note:** If gzip is supported, a set of unrepresentable character will display instead of the shown output. 
#### Exercise 12: Put a bunch of a JSON in a file and then make a POST request to https://httpbin.org/anything with the JSON in that file as the body
**Snip you can use:** "curl/post-with-header": `curl --json @${json-filename} --json ', "end": "true"}' ${url}`
    
**Input**
```bash
 curl --json @json.txt --json ', "end": "true"}'  https://httpbin.org/anything
```
**Output**
```bash
"args": {}, 
  "data": "null\n, \"end\": \"true\"}", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept": "application/json", 
    "Content-Length": "21", 
    "Content-Type": "application/json", 
  #Rest of the code for this page
```
   ***Solution Explanation:*** In this command, `-d @file.json` is used to include the JSON data stored in a file named "file.json" as the body of the POST request sent to https://httpbin.org/anything. By referencing a file, you can easily handle large or complex JSON data without cluttering the command line.
#### Exercise 13: Make a request to https://httpbin.org/image and set the header ‘Accept: image/png’. Save the output to a PNG file and open the file in an image viewer. Try the same thing with different `Accept`: headers
**Snip you can use:** "curl/download" 

   OR "curl/request-accept-type-save-output": ` curl -H "Accept: ${image/png}" ${url}/image -o ${image-filename}`
   
**Input**
```bash
curl -H "Accept: image/png" https://httpbin.org/image -o image.png
```
**Output**
```bash
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  8090  100  8090    0     0  86817      0 --:--:-- --:--:-- --:--:-- 86989
```
   ***Solution Explanation:*** By setting the "Accept" header to "image/png," this command will ensure the returned image is in PNG format. The `-o` flag is used to save the output to a file named "image.png."
#### Exercise 14: PUT request to https://httpbin.org/anything
**Snip you can use:** "curl/request-method": `curl -X ${GET|POST|PUT} ${url}` 

**Input** 
```bash
curl -X PUT https://httpbin.org/anything
```
**Output**
```bash

#Rest of the code for this page
"json": null, 
  "method": "PUT", 
  "origin": "XXX.XXX.XXX.XX", 
  "url": "https://httpbin.org/anything"
}
```
   ***Solution Explanation:*** Here, `curl` is used to make a PUT request to https://httpbin.org/anything. PUT requests are commonly used for updating or replacing resources on the server. This exercise showcases the simplicity of making PUT requests with `curl`.
#### Exercise 15: Request https://httpbin.org/image/jpeg, save it to a file, and open that file in your image editor
**Snip you can use:** "curl/download"

**Input**
```bash
curl -L  https://httpbin.org/image/jpeg -o image.jpeg
```
**Output**
```bash
 % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 35588  100 35588    0     0   137k      0 --:--:-- --:--:-- --:--:--  137k
```
   ***Solution Explanation:*** This snip fetches the content of a URL and saves it. In this case, the image located at https://httpbin.org/image/jpeg and saves it as "image.jpeg" using the `-o` flag. Run `open image.jpeg` to view the image.
#### Exercise 16: Request https://www.twitter.com. You’ll get an empty response. Get curl to show you the response headers too, and try to figure out why the response was empty
**Snip you can use:** "curl/request-debug": `curl -X ${GET|POST|...|} {--include |--verbose} ${url}`

**Input**
```bash
curl -i https://www.twitter.com
```
**Output**
```bash
HTTP/2 200                          
date: Day, XX Mnt Year 00:00:00 GMT 
perf: 7469935968  
expiry: Tue, 31 Mar 1981 05:00:00 GMT           
pragma: no-cache 
server: tsa_b 
#Rest of the code for this page
```
   ***Solution Explanation:*** By adding the `-i` or `--include` flag, this command displays the response headers in addition to the response body when making a GET request to https://www.twitter.com. The empty response might be due to various reasons such as server misconfiguration or redirection. Analyzing the response headers can provide insights into the server's behavior. `--verbose` will add addition informational text. **Note:** `--include` does the same as `-i`, it is just the long form.
#### Exercise 17: Make any request to https://httpbin.org/anything and just set some nonsense headers (like `panda`: `elephant`)
**Snip you can use:**
"curl/request-with-header"

**Input**
```bash
curl -H "panda: elephant" https://httpbin.org/anything
```
**Output**
```bash
#...
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept": "*/*", 
    "Host": "httpbin.org", 
    "Panda": "Elephant", 
#Rest of the code for this page
```
   ***Solution Explanation:*** This command adds a nonsensical header "panda: elephant" to the request sent to https://httpbin.org/anything. While the server may ignore unknown headers, this exercise demonstrates how to include arbitrary headers in a `curl` request.
#### Exercise 18: Request https://httpbin.org/status/404 and https://httpbin.org/status/200. Request them again and get curl to show the response headers
**Snip you can use:** "curl/request-debug"

**Input**
```bash
curl -i https://httpbin.org/status/404
curl -i https://httpbin.org/status/200
```
**Output**
```bash
HTTP/2 404 
date: Tue, XX Mon Year XX:XX:XX GMT
content-type: text/html; charset=utf-8
content-length: 0
server: gunicorn/19.9.0
access-control-allow-origin: *
access-control-allow-credentials: true
#----------------------------------------
HTTP/2 200 
date: Tue, XX Mon Year XX:XX:XX GMT
content-type: text/html; charset=utf-8
content-length: 0
server: gunicorn/19.9.0
access-control-allow-origin: *
access-control-allow-credentials: true
```
   ***Solution Explanation:*** These commands make GET requests to URLs that return specific HTTP status codes: 404 (Not Found) and 200 (OK). By including the `-i` flag, we can again examine the response headers. HTTP/2 404  and HTTP/2 200 in the output correspond to the protocol (HTTP/2) and status code (404 and 200).



#### Exercise 19: Request https://httpbin.org/anything and set a username and password (with `-u username:password`)
**Snip you can use:** "curl/request-user-pass": `curl -u ${username}:${password} ${url}`

**Input**
```bash
curl -u username:password https://httpbin.org/anything
```
**Output**
```bash
  #...
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept": "*/*", 
    "Authorization": "Basic Zm9vOmJhcg==", 
   #Rest of the code for this page
```
   ***Solution Explanation:*** By using the `-u` flag followed by the username and password separated by a colon.
(show how the request looks internally?)
#### Exercise 20: Download the Twitter homepage (https://twitter.com) in Spanish by setting the `Accept-Language: es-ES` header
**Snip you can use:** "curl/request-with-header" 
	
   OR "Curl-custom-header-accept-save": `curl -H "Accept-${Encoding|Language}: ${Header-Value}" ${url} -o ${web-name}`

**Input**
```bash
curl -H "Accept-Language: es-ES" https://twitter.com
```
**Output**
```html
<!DOCTYPE html>
<html dir="ltr" lang="es">
  <head>
<!-- Rest of the code for this page...-->
```
   ***Solution Explanation:*** Here, the "Accept-Language" header is set to "es-ES," indicating a preference for Spanish content. 

#### Exercise 21: Make a request to the Stripe API with curl. (see https://stripe.com/docs/development for how, they give you a test API key). Try making exactly the same request to https://httpbin.org/anything
**Snip you can use:** "curl/request-with-header"

OR "curl/request-stripe-api": `curl ${url}   -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \ -d ${data}\ ${-d data\}`

**Input**
```bash
curl https://httpbin.org/anything \
-u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
-d amount=900 \
-d currency=usd \
-d source=tok_visa \
-d receipt_email="jane.doe@example.com"
```
**Output**
```bash
#...
 "form": {
    "amount": "900", 
    "currency": "usd", 
    "receipt_email": "jane.doe@example.com", 
    "source": "tok_visa"
  }, 
  "headers": {
    "Accept": "*/*", 
    "Authorization": "Basic c2tfdGVzdF80ZUMzOUhxTHlqV0Rhcmp0VDF6ZHA3ZGM6", 
    "Content-Length": "74", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org", 
   #Rest of the code for this page
```
   ***Solution Explanation:***
