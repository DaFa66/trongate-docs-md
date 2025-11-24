# _attempt_get_valid_token()


public function _attempt_get_valid_token($user_levels = null): string|bool

## Description

Attempts to validate and return a token based on optional user level(s) condition.
      This method checks for a valid token in the following locations, in order of priority:


- HTTP headers (`$_SERVER['HTTP_TRONGATETOKEN']`)
- Cookies (`$_COOKIE['trongatetoken']`)
- Session (`$_SESSION['trongatetoken']`)


The method then verifies the token against the provided user levels, if any, and returns the valid token if found.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| `$user_levels` | int\|array\|null | User levels to filter tokens. | `null` | No |

## Return Value


| Type | Description |
| ---|---|
| string\|bool | The valid token if found, or false if none is found. |

## Attaching Tokens To Headers Using XMLHttpRequest


The code below demonstrates how to attach a 'Trongate token' to an **HTTP GET request** using JavaScript.  In the example, a PHP variable named `$trongate_token` has been made available within the JavaScript, and is being assigned to a JavaScript constant named, **token**.

```
<script>
const targetUrl = 'your_api_endpoint_here';
const token = '<?= $trongate_token ?>';

const http = new XMLHttpRequest();
http.open('GET', targetUrl);
http.setRequestHeader('Content-type', 'application/json');
http.setRequestHeader('trongateToken', token);
http.send();
http.onload = function() {
  console.log(http.status);
  console.log(http.responseText);
}
</script>
```


The code below demonstrates similar usage of XMLHttpRequest.  However, in this example we are submitting values to an endpoint via an **HTTP POST request**, using JavaScript.

```
<script>
const targetUrl = 'your_api_endpoint_here';
const token = '<?= $trongate_token ?>';

const params = {
  firstName: 'John',
  lastName: 'Smith',
  age: 21
}

const http = new XMLHttpRequest();
http.open('POST', targetUrl);
http.setRequestHeader('Content-type', 'application/json');
http.setRequestHeader('trongateToken', token);
http.send(params);
http.onload = function() {
  console.log(http.status);
  console.log(http.responseText);
}
</script>
```

## Attaching Tokens To Headers Using Fetch API


The Fetch API provides an alternative method for making HTTP requests in JavaScript, offering a more modern and flexible approach. Below are examples of how to achieve the same functionality as demonstrated with XMLHttpRequest, but using the Fetch API instead.


The code below demonstrates how to attach a 'Trongate token' to an **HTTP GET request** using the Fetch API.

```
<script>
const targetUrl = 'your_api_endpoint_here';
const token = '<?= $trongate_token ?>';
fetch(targetUrl, {
    method: 'GET',
    headers: {
        'Content-Type': 'application/json',
        'trongateToken': token
    }
})
.then(response => response.json())
.then(data => {
    console.log(data);
})
.catch(error => console.error('Error:', error));
</script>
```


The code below demonstrates similar usage of the Fetch API. However, in this example, we are submitting values to an endpoint via an **HTTP POST request**.

```
<script>
const targetUrl = 'your_api_endpoint_here';
const token = '<?= $trongate_token ?>';

const params = {
    firstName: 'John',
    lastName: 'Smith',
    age: 21
}

fetch(targetUrl, {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'trongateToken': token
    },
    body: JSON.stringify(params)
})
.then(response => response.json())
.then(data => {
    console.log(data);
})
.catch(error => console.error('Error:', error));
</script>
```

## Example Usage #1


The PHP code sample below demonstrates how to fetch **any** valid 'Trongate token' from **any** user level.

```
$this->module('trongate_tokens');
$token = $this->trongate_tokens->_attempt_get_valid_token(); // Any user level
```
## Example Usage #2


The code below demonstrates how to fetch and return a valid 'Trongate token' for a logged-in user with an '**admin**' user level. This example assumes that the 'trongate_user_levels' database table contains a row with an 'id' of 1 and a 'level_title' of 'admin'.

```
$this->module('trongate_tokens');
$token = $this->trongate_tokens->_attempt_get_valid_token(1); // admin
```
## Example Usage #3


In the final example, the code attempts to fetch and return a valid 'Trongate token' for a user with **either an 'admin' or a 'member'** user level. This example assumes that the 'trongate_user_levels' database table contains two specific rows: one with an 'id' of 1 and a 'level_title' of 'admin', and another with an 'id' of 2 and a 'level_title' of 'member'.

```
$this->module('trongate_tokens');
$token = $this->trongate_tokens->_attempt_get_valid_token([1, 2]); // admin or member
```
