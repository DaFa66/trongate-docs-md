# sort_by_property()


function sort_by_property(array &$array, string $property, string $direction = 'asc'): array

## Description

Sorts an array of associative arrays by a specified property. This function is useful when you need to organize data within an array of associative arrays based on one of the properties in each array element. The sorting can be done in either ascending or descending order.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $array | array | The array of associative arrays to be sorted. This parameter is passed by reference, meaning the original array will be modified. |
| $property | string | The property within each associative array by which to sort. The property must exist in each element of the array. |
| $direction | string | (optional) The direction in which to sort the array. Acceptable values are 'asc' for ascending (default) and 'desc' for descending. |

## Return Value


| Type | Description |
| ---|---|
| array | The sorted array of associative arrays. |

## Example #1


The code sample below demonstrates basic usage of the `sort_by_property` function with default parameters.

```
$data = [
      ['name' => 'John', 'age' => 28],
      ['name' => 'Jane', 'age' => 24],
      ['name' => 'Doe', 'age' => 32],
  ];
  
  $sorted_data = sort_by_property($data, 'age');
  
  // Output: [
  //   ['name' => 'Jane', 'age' => 24],
  //   ['name' => 'John', 'age' => 28],
  //   ['name' => 'Doe', 'age' => 32],
  // ]
```

## Example #2


The code sample below demonstrates a more complex usage of the `sort_by_property` function, sorting in descending order.

```
$data = [
      ['name' => 'Apple', 'price' => 3.5],
      ['name' => 'Orange', 'price' => 2.75],
      ['name' => 'Banana', 'price' => 1.25],
  ];
  
  $sorted_data = sort_by_property($data, 'price', 'desc');
  
  // Output: [
  //   ['name' => 'Apple', 'price' => 3.5],
  //   ['name' => 'Orange', 'price' => 2.75],
  //   ['name' => 'Banana', 'price' => 1.25],
  // ]
```

## Notes


If the specified property does not exist in any of the associative arrays, the behavior of the function may be unpredictable. Ensure that the property exists in each array element before calling this function.
