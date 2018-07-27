
---

title: API Reference

  

language_tabs: # must be one of https://git.io/vQNgJ

- js
- shell
- python
- cs
- php

  

toc_footers:

- <a href='#'></a>

- <a href='#'>Documentation Powered by Ciptex</a>

  

includes:

- errors

  

search: true

---

  

# Introduction

  

Welcome to Hermes API.

  

In this document, you will find essential API calls you need to get up and start with your deployment.

  

# Authentication

  

> To authorize, use this code:

  

```js
function token() {

	//Your Username and Password

	var email = "test";
	var password = "test";


	//Contructing the XML Request

	var req = new XMLHttpRequest();


	//Initialasing the URL Path to the endpoint

	var url = "https://auth-api.ciptex.net/token";

  

	//Setting up the pramateres for the XML Request

	var params = "grant_type=password&username=" + email + "&password=" + password;


	//Setting up the XML Method

	req.open("POST", url, true);


	//Send the proper header information along with the request

	req.setRequestHeader("Content-type", "application/x-www-form-urlencoded");

	req.onreadystatechange = function () { //Call a function when the state changes.

		if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part

			var j = JSON.parse(req.responseText); //Parsing the body of the XML Request

			j.issuetime = new Date().getTime(); //

			sessionStorage.access_token = JSON.stringify(j);

			login(sessionStorage.access_token);

		}
		else

		{

			console.log(req.status); //If the Status was not equal to 200 you will get an error in the console which most likely is a failure in authentication

		}

	}

	//and finally sending the parameters to the server.


	req.send(params);
```

> cURL

```bash
curl -i -H 'Content-Type: application/x-www-form-urlencoded' -d 'grant_type=password&username=test&password=test'  -X POST https://auth-api.ciptex.net/token
```

> Python 

```py
import http.client

conn = http.client.HTTPSConnection("") 

payload = "{\"grant_type\":\"password\",\"username\": \"test\",\"password\": \"test\"}" # Grant type for the call

headers = { 'content-type': "application/x-www-form-urlencoded" } # Relevant header 

conn.request("POST", "https://auth-api.ciptex.net/token", payload, headers) # Method and endpoint 

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8")) # Your Access code
```
> Objective C

```cs
// Setting up you prams and relevant headers
NSDictionary *headers = @{ @"content-type": @"application/x-www-form-urlencoded" };
NSDictionary *parameters = @{ @"grant_type": @"password",
                              @"username": @"test",
                              @"password": @"test";

NSData *postData = [NSJSONSerialization dataWithJSONObject:parameters options:0 error:nil];
// Pointing the call to the right endpoint
NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"https://auth-api.ciptex.net/token"] cachePolicy:NSURLRequestUseProtocolCachePolicy 
timeoutInterval:10.0];
// Setting the method as Post
[request setHTTPMethod:@"POST"];
[request setAllHTTPHeaderFields:headers];
[request setHTTPBody:postData];
// Setting up an NS session
NSURLSession *session = [NSURLSession sharedSession];
NSURLSessionDataTask *dataTask = [session dataTaskWithRequest:request
completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
  // Simple validation
    if (error) {
        NSLog(@"%@", error);
  } else {
        NSHTTPURLResponse *httpResponse = (NSHTTPURLResponse *) response;
        NSLog(@"%@", httpResponse);
  }
}];

[dataTask resume];
  
```
> PHP 

```php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://auth-api.ciptex.net/token", // Address for the endpoint
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST", // Method type for the api call
  CURLOPT_POSTFIELDS => "{\"grant_type\":\"password\",\"username\": \"test\",\"password\": \"test\",}", // Setting up the relevant grant type
  CURLOPT_HTTPHEADER => array(
    "content-type: application/x-www-form-urlencoded" // Setting up the right header for the call
  ),
));

$response = curl_exec($curl); 
$err = curl_error($curl);

curl_close($curl);

if ($err) { // Simple validation
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```


  

> Make sure to replace `{bearer_token}` with your API key.

  

Authenticate the user with the system and obtain the auth_token

  

`Authorization: Bearer {bearer_token}`

  

<aside  class="notice">



</aside>

  

# Hermes

  

## Get Agents

  > JavaScript

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/agents";
var req = new XMLHttpRequest(); // making a new XML request
req.open("GET", url, true); // Setting the method to the GET for the new request.

req.setRequestHeader("Content-type", "application/json"); // setting headers for our XML request
req.setRequestHeader("Authorization", "Bearer" + " " + "<ACCESS_TOKEN>");

req.onreadystatechange = function () { //Call a function when the state changes.
	if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
		return JSON.parse(req.responseText); //Parsing the body of the XML Request
	}
}
req.send();
```

> cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/agents
```

> Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/agents' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/agents"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]] forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/agents';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```

  

> The above command returns JSON structured like this:

  

```json

[
  {
    "oid": "Sod-FHwK",
    "createat": "2018-01-31T11:20:21Z",
    "updateat": "2018-01-10T17:29:03Z",
    "firstname": "Agent",
    "lastname": "Test",
    "agentid": 1000
  }
]

```

  

This endpoint retrieves all Agents.

  

### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/agents`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

  

## Get Break Codes

> JavaScript

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/break-codes";
 var req = new XMLHttpRequest();// making a new XML request
 req.open("GET", url, true);// Setting the method to the GET for the new request.

 req.setRequestHeader("Content-type", "application/json");// setting headers for our XML request
 req.setRequestHeader("Authorization", "Bearer" +" "+ "<ACCESS_TOKEN>"); 

 req.onreadystatechange = function () { //Call a function when the state changes.
    if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
        return JSON.parse(req.responseText); //Parsing the body of the XML Request
    } 
}
req.send();
```

> cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/break-codes
```

> Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/break-codes' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/break-codes"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]]  forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/break-codes';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```

  

> The above command returns JSON structured like this:

  

```json

[
  {
    "oid": "SogrYcgK",
    "createat": "2017-05-31T14:25:12Z",
    "updateat": "2017-05-31T14:25:12Z",
    "description": "Break AM",
    "allowedtime": 10,
    "pausecodeid": 0,
    "groupname": "Standard"
  }
]

```

  

This endpoint retrieves all Break Codes.

  

### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/break-codes`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

  

## Get Email Campaigns

  > JavaScript  

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/email";
 var req = new XMLHttpRequest();// making a new XML request
 req.open("GET", url, true);// Setting the method to the GET for the new request.

 req.setRequestHeader("Content-type", "application/json");// setting headers for our XML request
 req.setRequestHeader("Authorization", "Bearer" +" "+ "<ACCESS_TOKEN>"); 

 req.onreadystatechange = function () { //Call a function when the state changes.
    if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
        return JSON.parse(req.responseText); //Parsing the body of the XML Request
    } 
}
req.send();
```

> cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/email
```

> Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/email' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/email"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]]  forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/email';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```
  

> The above command returns JSON structured like this:

  

```json

[
  {
    "oid": "SozCIXUK",
    "createat": "2018-06-01T11:18:16Z",
    "updateat": "2018-06-07T09:03:25Z",
    "description": "Test",
    "queueid": 0,
    "openingid": "35F64636424415B4",
    "holidayid": "35F64692456437B4",
    "statusgroup": 1,
    "priority": 0,
    "phonedisplayspecific": "01613750777",
    "mediatype": "Email",
    "campaignid": "35F6A734538555B4",
    "scriptid": 0,
    "scriptname": "",
    "email": "",
    "replayemail": ""
  }
]

```

  

This endpoint retrieves all Email Campaigns.

  

### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/email`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

  

## Get Inbound Campaigns

  > JavaScript  

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/inbound";
 var req = new XMLHttpRequest();// making a new XML request
 req.open("GET", url, true);// Setting the method to the GET for the new request.

 req.setRequestHeader("Content-type", "application/json");// setting headers for our XML request
 req.setRequestHeader("Authorization", "Bearer" +" "+ "<ACCESS_TOKEN>"); 

 req.onreadystatechange = function () { //Call a function when the state changes.
    if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
        return JSON.parse(req.responseText); //Parsing the body of the XML Request
    } 
}
req.send();
```
> cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/inbound
```

> Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/inbound' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/inbound"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]]  forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/inbound';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```

> The above command returns JSON structured like this:

  

```json

[
  {
    "oid": "Sov1lLcK",
    "createat": "2018-06-01T07:41:09Z",
    "updateat": "2018-07-09T09:57:03Z",
    "description": "TEST",
    "queueid": 100,
    "openingid": "35F64636424415B4",
    "holidayid": "",
    "statusgroup": 3,
    "deflanguage": "EN",
    "priority": 80,
    "phonedisplayspecific": "01613750777",
    "mediatype": "Telephony",
    "campaignid": "221050",
    "scriptid": 26,
    "scriptname": "Test",
    "voicescriptname": "",
    "endvoicescriptname": "",
    "clienthoursoid": "SodGwBcK"
  }
]

```

  

This endpoint retrieves all Inbound Campaigns.

  

### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/inbound`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

  
  

## Get Manual Campaigns

  > JavaScript  

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/manual";
 var req = new XMLHttpRequest();// making a new XML request
 req.open("GET", url, true);// Setting the method to the GET for the new request.

 req.setRequestHeader("Content-type", "application/json");// setting headers for our XML request
 req.setRequestHeader("Authorization", "Bearer" +" "+ "<ACCESS_TOKEN>"); 

 req.onreadystatechange = function () { //Call a function when the state changes.
    if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
        return JSON.parse(req.responseText); //Parsing the body of the XML Request
    } 
}
req.send();
```
> cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/manual
```

> Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/manual' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/manual"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]]  forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/manual';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```

> The above command returns JSON structured like this:

  

```json

[
  {
    "oid": "Sow3gWsK",
    "createat": "2018-06-01T11:06:56Z",
    "updateat": "2018-06-06T12:16:09Z",
    "description": "Test",
    "openingid": "",
    "holidayid": "",
    "statusgroup": 1,
    "deflanguage": "EN",
    "phonedisplayspecific": "01613750777",
    "mediatype": "Telephony",
    "campaignid": "35F69738717537B4",
    "scriptid": 23,
    "scriptname": "Test"
  }
]

```

  

This endpoint retrieves all Manual Campaigns.

  

### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/manual`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

  
  

## Get Outbound Campaigns

   > JavaScript 

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/outbound";
 var req = new XMLHttpRequest();// making a new XML request
 req.open("GET", url, true);// Setting the method to the GET for the new request.

 req.setRequestHeader("Content-type", "application/json");// setting headers for our XML request
 req.setRequestHeader("Authorization", "Bearer" +" "+ "<ACCESS_TOKEN>"); 

 req.onreadystatechange = function () { //Call a function when the state changes.
    if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
        return JSON.parse(req.responseText); //Parsing the body of the XML Request
    } 
}
req.send();
```
> cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/outbound
```
> Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/outbound' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/outbound"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]]  forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/outbound';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```

> The above command returns JSON structured like this:

  

```json

[
  {
    "oid": "SqeGfBsK",
    "createat": "2018-06-06T13:21:19Z",
    "updateat": "2018-06-07T09:04:13Z",
    "description": "Test",
    "openingid": "",
    "holidayid": "",
    "statusgroup": -1,
    "deflanguage": "EN",
    "phonedisplayspecific": "01613750777",
    "mediatype": "Telephony",
    "campaignid": "35175645615437B4",
    "scriptid": -1,
    "scriptname": "",
    "endvoicescriptname": "",
    "clienthoursoid": "",
    "outmode": "Preview"
  }
]

```

  

This endpoint retrieves all Outbound Campaigns.

  

### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/campaigns/outbound`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

  
  

## Get Customer Hours

  > JavaScript  

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/customer-hours";
 var req = new XMLHttpRequest();// making a new XML request
 req.open("GET", url, true);// Setting the method to the GET for the new request.

 req.setRequestHeader("Content-type", "application/json");// setting headers for our XML request
 req.setRequestHeader("Authorization", "Bearer" +" "+ "<ACCESS_TOKEN>"); 

 req.onreadystatechange = function () { //Call a function when the state changes.
    if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
        return JSON.parse(req.responseText); //Parsing the body of the XML Request
    } 
}
req.send();
```

  > cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/customer-hours
```

> Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/customer-hours' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/customer-hours"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]]  forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/customer-hours';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```

> The above command returns JSON structured like this:

  

```json
[
  {
    "oid": "SodBRBQK",
    "createat": "2018-05-31T10:19:45Z",
    "updateat": "2018-05-31T10:21:03Z",
    "description": "Test",
    "openinghour": [
      {
        "begin": 480,
        "end": 1200
      },
      {
        "begin": 1920,
        "end": 2640
      },
      {
        "begin": 3360,
        "end": 4080
      },
      {
        "begin": 4800,
        "end": 5520
      },
      {
        "begin": 6240,
        "end": 6960
      },
      {
        "begin": 7680,
        "end": 8220
      }
    ]
  }
]
```

  

This endpoint retrieves all Customer Hours.

  

### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/customer-hours`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

  

## Get Disposition Groups

   > JavaScript 

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/disposition-groups";
 var req = new XMLHttpRequest();// making a new XML request
 req.open("GET", url, true);// Setting the method to the GET for the new request.

 req.setRequestHeader("Content-type", "application/json");// setting headers for our XML request
 req.setRequestHeader("Authorization", "Bearer" +" "+ "<ACCESS_TOKEN>"); 

 req.onreadystatechange = function () { //Call a function when the state changes.
    if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
        return JSON.parse(req.responseText); //Parsing the body of the XML Request
    } 
}
req.send();
```
> cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/disposition-groups
```

> Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/disposition-groups' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/disposition-groups"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]]  forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/disposition-groups';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```

> The above command returns JSON structured like this:

  

```json
[
  {
    "oid": "SogsrdsK",
    "createat": "2018-05-31T14:26:35Z",
    "updateat": "2018-05-31T14:26:43Z",
    "description": "Test",
    "currency": "£",
    "statusgroupid": 1
  }
]
```

  

This endpoint retrieves all Disposition Groups.


### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/disposition-groups`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

  

## Get Dispositions

  > JavaScript  

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/dispositions";
 var req = new XMLHttpRequest();// making a new XML request
 req.open("GET", url, true);// Setting the method to the GET for the new request.

 req.setRequestHeader("Content-type", "application/json");// setting headers for our XML request
 req.setRequestHeader("Authorization", "Bearer" +" "+ "<ACCESS_TOKEN>"); 

 req.onreadystatechange = function () { //Call a function when the state changes.
    if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
        return JSON.parse(req.responseText); //Parsing the body of the XML Request
    } 
}
req.send();
```

> cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/dispositions
```  

> Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/dispositions' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/dispositions"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]]  forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/dispositions';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```

> The above command returns JSON structured like this:

  

```json

[
  {
    "oid": "SoguweEK",
    "createat": "2018-05-31T14:29:52Z",
    "updateat": "2018-05-31T14:29:52Z",
    "description": "Test",
    "statusgroupid": 1,
    "statuscode": 1,
    "statusdetailed": 0,
    "positive": false,
    "argued": false,
    "nonargued": false,
    "cost": 0,
    "validquota": false
  }
]

```

  

This endpoint retrieves all Dispositions.

  

### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/dispositions`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

  

## Get Holiday Groups

  > JavaScript  

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/holiday-groups";
 var req = new XMLHttpRequest();// making a new XML request
 req.open("GET", url, true);// Setting the method to the GET for the new request.

 req.setRequestHeader("Content-type", "application/json");// setting headers for our XML request
 req.setRequestHeader("Authorization", "Bearer" +" "+ "<ACCESS_TOKEN>"); 

 req.onreadystatechange = function () { //Call a function when the state changes.
    if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
        return JSON.parse(req.responseText); //Parsing the body of the XML Request
    } 
}
req.send();
```

> cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/holiday-groups
```
> Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/holiday-groups' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/holiday-groups"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]]  forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/holiday-groups';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```

> The above command returns JSON structured like this:

  

```json

[
  {
    "oid": "SodYDDsK",
    "createat": "2018-05-31T10:39:47Z",
    "updateat": "2018-06-06T13:10:12Z",
    "description": "Default Holidays",
    "timezoneid": "GMT Standard Time",
    "holidaygroupid": "35F61735444437B4",
    "holidayitems": [
      {
        "oid": "SodYODwK",
        "description": "Bank holiday",
        "closedday": 7,
        "closedmonth": 5,
        "closedyear": 0,
        "message": "\\\\10.255.0.135\\acd_c\\hermes_p\\Files\\35F6B4653464D4B4\\recep t\\221050\\BankHoliday.wav",
        "hourbegin": 0,
        "hourend": 2359,
        "holidayitemid": 1
      }
    ]
  }
]

```

  

This endpoint retrieves all Holiday Groups.

  

### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/holiday-groups`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

  

## Get Queues

   > JavaScript 

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/queues";
 var req = new XMLHttpRequest();// making a new XML request
 req.open("GET", url, true);// Setting the method to the GET for the new request.

 req.setRequestHeader("Content-type", "application/json");// setting headers for our XML request
 req.setRequestHeader("Authorization", "Bearer" +" "+ "<ACCESS_TOKEN>"); 

 req.onreadystatechange = function () { //Call a function when the state changes.
    if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
        return JSON.parse(req.responseText); //Parsing the body of the XML Request
    } 
}
req.send();
```
> cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/queues
```
 
 > Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/queues' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/queues"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]]  forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/queues';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```

> The above command returns JSON structured like this:

  

```json

[  
   {  
      "oid":"SodB5B4W",
      "createat":"2018-05-31T10:25:45Z",
      "updateat":"2018-05-31T10:25:45Z",
      "description":"TEST",
      "queueid":100
   }
]

```

  

This endpoint retrieves all Queues.

  

### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/queues`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

  

## Get Service Hours

   > JavaScript 

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/service-hours";
 var req = new XMLHttpRequest();// making a new XML request
 req.open("GET", url, true);// Setting the method to the GET for the new request.

 req.setRequestHeader("Content-type", "application/json");// setting headers for our XML request
 req.setRequestHeader("Authorization", "Bearer" +" "+ "<ACCESS_TOKEN>"); 

 req.onreadystatechange = function () { //Call a function when the state changes.
    if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
        return JSON.parse(req.responseText); //Parsing the body of the XML Request
    } 
}
req.send();
```
> cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/service-hours
```

> Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/service-hours' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/service-hours"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]]  forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/service-hours';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```

> The above command returns JSON structured like this:

  

```json

[  
   {  
      "oid":"SodW4DEK",
      "createat":"2018-05-31T10:32:08Z",
      "updateat":"2018-05-31T10:32:41Z",
      "description":"Standard Hours",
      "timezoneid":"GMT Standard Time",
      "servicehoursgroupid":"35F62665434454B4",
      "openinghour":[  
         {  
            "begin":480,
            "end":1200
         },
         {  
            "begin":1920,
            "end":2640
         },
         {  
            "begin":3360,
            "end":4080
         },
         {  
            "begin":4800,
            "end":5520
         },
         {  
            "begin":6240,
            "end":6960
         },
         {  
            "begin":7740,
            "end":7920
         }
      ]
   }
]

```

  

This endpoint retrieves all Service Hours.

  

### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/service-hours`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

  

## Get Supervisor Groups

   > JavaScript 

```js
 var url = "https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/supervisor-groups";
 var req = new XMLHttpRequest();// making a new XML request
 req.open("GET", url, true);// Setting the method to the GET for the new request.

 req.setRequestHeader("Content-type", "application/json");// setting headers for our XML request
 req.setRequestHeader("Authorization", "Bearer" +" "+ "<ACCESS_TOKEN>"); 

 req.onreadystatechange = function () { //Call a function when the state changes.
    if (req.readyState === 4 && req.status === 200) { //Making sure if the status was 200 then moving to the next part
        return JSON.parse(req.responseText); //Parsing the body of the XML Request
    } 
}
req.send();
```

  > cURL

```bash
curl -i -H "Content-type: application/json" -H "Authorization: Bearer <ACCESS_TOKEN>" -X GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/supervisor-groups
```

> Python

```py
import requests
import json
url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/supervisor-groups' # Ednpoint URL
headers = {'Content-Type':'application/json', 'Authorization':'Bearer ' + '<ACCESS_TOKEN>'} # Replace the <ACCESS_TOKEN> with your token
response = requests.get(url, verify=True) # Check for validation
if response.status_code == 200:
print (response.text) # Printing your response in the terminal (Optional)
 
json.loads(response.text) # The respond from the endpoint
```

> Objective C

```cs
NSURL *url = @"https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/supervisor-groups"; // Endpoint URL
  NSURLSession *session = [NSURLSession sharedSession]; 

  NSMutableURLRequest *request = [[NSMutableURLRequest alloc] initWithURL:url];

  [request setHTTPMethod:@"GET"]; // Setting the Request method

  [request setValue:@[NSString stringWithFormat:["Bearer%@" + "<ACCESS_TOKEN>"]]  forHTTPHeaderField:@"Authorization"];
  [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"]; // Setting the relevant headers 

   // add any additional headers or parameters
   NSURLSessionDataTask *downloadTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
    if (!error) {
   // do your response handling
   id json = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    NSArray * resultDict =[json objectForKey:@"result"];
  }
  }];

  [downloadTask resume];

  
```

> PHP 

```php
$token
$remote_url = 'https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/supervisor-groups';

// Create a stream
$opts = array(
  'http'=>array(
    'method'=>"GET",
    'header' => "Authorization: Bearer ".$token)                 
  )
);

$context = stream_context_create($opts);

// Open the file using the HTTP headers set above
$file = file_get_contents($remote_url, false, $context);

print($file);
```

> The above command returns JSON structured like this:

  

```json

{
  "oid": "SoKFGUUK",
  "createat": "2018-05-30T12:42:26Z",
  "updateat": "2018-07-10T11:21:44Z",
  "description": "default group",
  "supervisegroupid": 0,
  "agents": [
    1000,
    1001,
    1002
  ]
}

```

  

This endpoint retrieves all Supervisor Groups.

  

### HTTP Request

  

`GET https://0rnnu19j3f.execute-api.eu-west-2.amazonaws.com/Dev/supervisor-groups`

  

### Query Parameters

  

<aside  class="success">

200 HTTP Status Code

</aside>

