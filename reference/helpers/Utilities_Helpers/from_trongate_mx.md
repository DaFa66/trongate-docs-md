# from_trongate_mx()


function from_trongate_mx(): bool

## Description

Checks if the HTTP request has been invoked by Trongate MX. This function inspects the HTTP headers to determine if the request contains a specific header indicating that it originated from Trongate MX. It is useful for distinguishing requests made from Trongate MX from those made by other sources.
## Return Value


| Type | Description |
| ---|---|
| bool | Returns `true` if the request has the `X-Trongate-MX-Request` header set to `true`, otherwise `false`. |

## Example


The code sample below demonstrates basic usage of the `from_trongate_mx` function.

```
if (from_trongate_mx()) {
      echo 'Request is from Trongate MX';
  } else {
      echo 'Request is not from Trongate MX';
  }
  // Output: 'Request is from Trongate MX' if the header is set, otherwise 'Request is not from Trongate MX'
```

## Notes


The function checks specifically for the `X-Trongate-MX-Request` header. If the header is not present or is set to a value other than `true`, the function will return `false`. Ensure that the header is correctly set in requests where this function needs to be utilized.
