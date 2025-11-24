# insert_batch()


public function insert_batch(string $table, array $records): int

## Description

Insert multiple records into the specified table in a batch using a single SQL statement. This method is designed for efficiency when inserting a large number of records at once.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| table | string | The name of the table to insert records into. | N/A | Yes |
| records | array | An array containing associative arrays representing records to be inserted. | N/A | Yes |

## Return Value


| Type | Description |
| ---|---|
| int | The number of records successfully inserted. |

## Throws


| Exception | Description |
| ---|---|
| PDOException | If an error occurs during the database operation. |

> [!WARNING]
> **Warning!**
>
> > [!NOTE]
> > ** Warning!
> 
> 
> > [!NOTE]
> > This method should only be used in controlled environments to prevent potential security vulnerabilities arising from direct user input.


## Example Usage


Below is an example of how to insert three records into an 'employees' table in a single batch:

```php
$employee_records = [
    [
        'name' => 'John Doe',
        'position' => 'Software Engineer',
        'salary' => 80000
    ],
    [
        'name' => 'Jane Smith',
        'position' => 'UX Designer',
        'salary' => 75000
    ],
    [
        'name' => 'Mike Johnson',
        'position' => 'Data Analyst',
        'salary' => 70000
    ]
];

$num_inserted = $this->model->insert_batch('employees', $employee_records);
echo "Successfully inserted $num_inserted records into the 'employees' table.";
```
