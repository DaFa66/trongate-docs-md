# form_search()


function form_search(string $name, ?string $value = null, ?array $attributes = null): string

## Description

Generates a search input form field element.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $name | string | The name attribute for the input element. |
| $value | string\|null | (optional) The value attribute for the input element. Default is null. |
| $attributes | array\|null | (optional) Additional attributes for the input element as an associative array. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML input element. |

## Example #1


The code sample below demonstrates the basic usage of the `form_search` function with default parameters.

```
$name = 'search_query';
$value = 'example';
echo form_search($name, $value);
// Output: '<input type="search" name="search_query" value="example">'
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_search` function with additional attributes.

```
$name = 'search_query';
$value = 'example';
$attributes = ['class' => 'form-control', 'id' => 'search-input', 'placeholder' => 'Search...'];
echo form_search($name, $value, $attributes);
// Output: '<input type="search" name="search_query" value="example" class="form-control" id="search-input" placeholder="Search...">'
```
