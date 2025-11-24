# sort_rows_by_property()


function sort_rows_by_property(array $array, string $property, string $direction = 'asc'): array

## Description

Sorts an array of objects by a specified property. This function is useful when you need to organize a collection of objects based on one of their properties. The sorting can be performed in either ascending or descending order.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $array | array | The array of objects to be sorted. Each element in the array should be an object. |
| $property | string | The property within each object by which to sort. The property must exist in each object of the array. |
| $direction | string | (optional) The direction in which to sort the array. Acceptable values are 'asc' for ascending (default) and 'desc' for descending. |

## Return Value


| Type | Description |
| ---|---|
| array | The sorted array of objects. |

## Example #1


The code sample below demonstrates basic usage of the `sort_rows_by_property` function with default parameters.

```
$data = [
      (object) ['name' => 'John', 'age' => 28],
      (object) ['name' => 'Jane', 'age' => 24],
      (object) ['name' => 'Doe', 'age' => 32],
  ];
  
  $sorted_data = sort_rows_by_property($data, 'age');
  
  // Output: [
  //   (object) ['name' => 'Jane', 'age' => 24],
  //   (object) ['name' => 'John', 'age' => 28],
  //   (object) ['name' => 'Doe', 'age' => 32],
  // ]
```

## Example #2


The code sample below demonstrates a more complex usage of the `sort_rows_by_property` function, sorting in descending order.

```
$data = [
      (object) ['name' => 'Apple', 'price' => 3.5],
      (object) ['name' => 'Orange', 'price' => 2.75],
      (object) ['name' => 'Banana', 'price' => 1.25],
  ];
  
  $sorted_data = sort_rows_by_property($data, 'price', 'desc');
  
  // Output: [
  //   (object) ['name' => 'Apple', 'price' => 3.5],
  //   (object) ['name' => 'Orange', 'price' => 2.75],
  //   (object) ['name' => 'Banana', 'price' => 1.25],
  // ]
```

## Notes


If the specified property does not exist in any of the objects, the behavior of the function may be unpredictable. Ensure that the property exists in each object before calling this function.
