# remove_substr_between()


function remove_substr_between(string $start, string $end, string $haystack, bool $remove_all = false): string

## Description

Removes a portion of a string between two given substrings. If the optional `$remove_all` parameter is set to `true`, all matching portions will be removed.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $start | string | The starting substring. | N/A | Yes |
| $end | string | The ending substring. | N/A | Yes |
| $haystack | string | The string from which to remove the substring. | N/A | Yes |
| $remove_all | bool | Whether to remove all matching portions. | false | No |

## Return Value


| Type | Description |
| ---|---|
| string | The modified string. |

## Example Usage #1


The code below demonstrates how to remove a portion of text enclosed within HTML bold tags (<b> and </b>). In this example, the goal is to remove the substring **<b>Macbeth</b>** from the `$haystack` variable.


Note that **<b>Macbeth</b>** appears more than once in the `$haystack` variable. However, only the first instance of a matching substring is being removed.

```
$start = '<b>';
$end = '</b>';
$haystack = 'When <b>Macbeth</b> speaks, all listen. <b>Macbeth</b> is a forbidden word.';
echo remove_substr_between($start, $end, $haystack);
// Output:   When  speaks, all listen. <b>Macbeth</b> is a forbidden word.
```
## Example Usage #2


In this example, *all* occurrences of substrings that match the defined conditions are removed by passing a value of **true** as the optional fourth argument.

```
$start = '<b>';
$end = '</b>';
$haystack = 'When <b>Macbeth</b> speaks, all listen. <b>Macbeth</b> is a forbidden word.';
echo remove_substr_between($start, $end, $haystack, true);
// Output:   When  speaks, all listen.  is a forbidden word.
```
