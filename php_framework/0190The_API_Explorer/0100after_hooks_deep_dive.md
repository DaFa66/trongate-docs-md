# Using After Hooks


The goal of an after hook is to intercept an outbound HTTP response and then do *something* with it *before* the server issues a response to the end user.


An after hook can be added onto an API endpoint by adding the 'afterHook' property onto an endpoint's settings. Below is an example of an after hook called '_prep_date' being declared for a 'Get' endpoint. This setting (which would be stored on an api.json file) would invoke a protected method named `_prep_date()` whenever the server is about to issue a response, after having invoked the 'Get' endpoint.

```
"Get": {
  "url_segments": "api/get/fish",
  "request_type": "GET",
  "description": "Fetch rows from table",
  "enableParams": true,
  "authorization": "*",
  "afterHook": "_prep_date"
}
```

## The Outbound Response Array


All the information that gets passed into an after hook comes in the form of an array. We can call this array the 'outbound response array'.


The general structure of an after hook will facilitate taking in an outbound response array, doing something with it, then potentially returning the array. If we represent our outbound response array with the variable `$output`, then our after hook methods can take the following form:

```php
function _post_insert($output) {
  // do some stuff
  return $output;
}
```

## Diving Deeper


By using PHP's built-in `var_dump()` method, in combination with a `die` statement, it's possible to explore the contents of an outbound response array.

```php
function _post_insert($output) {
  var_dump($output);
  die();
}
```


This will reveal the following three parameters:


- **token - **If a Trongate security token was passed into the header of the inbound HTTP request, then the value of the security token will be assigned to the 'token' property of the outbound response array. Therefore, to access the token, we could say:

```php
$trongate_token = $output["token"];
echo $trongate_token;
die();
```


- **body** - The body is a string of text that is to be issued by the server. Often, though not always, the body can be JSON decoded into an array of key-value pairs. So, if 'id' with a value of '4' was being issued by the server, we could access the id with:

```php
$id = $output["body"]["id"];
echo $id; // outputs 4
die();
```


- **code** - Finally, our outbound response array will contain a 'code' parameter. The code parameter will be a numeric value representing the HTTP response status code from the server. To display the HTTP response server code, using PHP, we could say:

```php
echo $output["code"]; // outputs (something like) 200
die();
```

> [!TIP]
> **Best Practices**
>
> Learn about HTTP response status codes [here](https://trongate.io/docs_m/information/understanding-http-response-status-codes).


## Modifying The Outbound Response Array


Having access to the outbound HTTP response array means that we have the ability to manipulate the response before it gets served to the end user.


There are lots of situations where this might be useful. One example would be to format dates.


**EXAMPLE**


Let's imagine that you have an API endpoint that queries a database table and returns information about a record that's stored in the database table.


This could be something like a members table, and it's possible that the response body could take the form of a string of text that could be converted into a JSON object with the following properties:

```
{
  "id": 88,
  "username": "Rambo",
  "date_joined": 1629840563
}
```


As you can see, 'date_joined' is an integer that's ten digits in length. When we see this kind of value in PHP, we can be fairly confident that we're being issued with a Unix timestamp. However, before sending the response to the end user, we may wish to use an after hook to intercept the response and format the date so that it's presented in a more user-friendly and readable manner.


Below is an example of an after hook that could modify a response body so that 'date_joined' is nicely formatted.

```php
function _prep_date($output) {
  $date_joined = $output["body"]["date_joined"];
  $output["body"]["date_joined"] = date("l jS F Y", $date_joined);
  return $output;
}
```


The code above would modify the HTTP response body, giving us:

```
{
  "id": 88,
  "username": "Rambo",
  "date_joined": "Tuesday 24th August 2021"
}
```

