# make_rand_str()


function make_rand_str(int $length = 32, bool $uppercase = false): string

## Description

Generates a random string of characters, customizable by length and whether to use uppercase. Ideal for generating secure and unique keys or tokens.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $length | int | Optional. The length of the random string to be generated. | 32 |
| $uppercase | bool | Optional. Whether the string should be returned in uppercase letters. | false |

## Return Value


| Type | Description |
| ---|---|
| string | Returns the randomly generated string. The string will be in uppercase if the $uppercase parameter is set to true; otherwise, it will be in lowercase. |

## Example Usage

```
echo make_rand_str(); // Output: jk7hjkmq89ph7nqmp89y3q4h3p89h3nq
echo make_rand_str(10, true); // Output: JH7JKM9PQH
```
