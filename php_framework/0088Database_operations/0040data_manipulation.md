# Data Manipulation


The Trongate Model class provides the following methods for inserting, updating, and deleting database data:


- insert()
- update()
- update_where()
- delete()
- insert_batch()

## Creating Database Records With The Insert Method


The insert() method inserts a row of data into a database table. With this method, rows of new data are represented by a PHP array. This method accepts the following parameters:


- **$data** (required) - an array of key-value pairs representing the table row that is to be inserted.
- **$target_table** (optional) - the name of the database table where the new row is to be inserted. By default, the Model will assume the target table is equal to the value in the first URL segment.

## What Gets Returned?


If the method results in a new table row being inserted, the 'id' of the newly inserted record will be returned.

## Example


The syntax below shows the simplest insert example possible. In this example, we create an array of data that represents a new table row. Then, we invoke the insert method to add a new row to a database table using the array we created.

```php
$data["first_name"] = "Eric"; 
$data["last_name"] = "Clapton"; 
$data["trongate_user_id"] = 91; 
$this->model->insert($data);
```


The code above will produce the following SQL query:


**INSERT INTO *****tablename***** (first_name, last_name, trongate_user_id) VALUES ('Eric', 'Clapton', 91)**

> [!NOTE]
> **Just To Let You Know...**
>
> In a working example, 'tablename' would be replaced with the first segment from the URL.


## Updating Database Records With The Update Method


The update() method updates a record in a database table. This method takes the ID of the record to update, an associative array containing column names as keys and their corresponding values, and an optional parameter specifying the name of the database table to update. It constructs and executes an SQL query to perform the update, returning true if the update was successful and false otherwise. This method accepts the following parameters:


- **$update_id** (required) - the ID of the record to update.
- **$data** (required) - an associative array containing column names as keys and their corresponding values.
- **$target_table** (optional) - the name of the database table to update. By default, the Model will assume the target table is equal to the value in the first URL segment.

## What Gets Returned?


If the method successfully updates the record, it returns `true`. Otherwise, it returns `false`.

## Example


The code sample below demonstrates how to use the update() method to update a record in the database.

```php
// ID of the record to update
$update_id = 123;
// Data to update
$data["first_name"] = "John"; 
$data["last_name"] = "Doe"; 
$data["email"] = "john.doe@example.com"; 
$this->model->update($update_id, $data);
```

## Deleting Database Records With The Delete Method


The delete() method deletes a record from a database table based on its ID. This method takes the ID of the record to delete and an optional parameter specifying the name of the database table. It constructs and executes an SQL query to delete the record, returning true if the delete operation was successful and false otherwise. This method accepts the following parameters:


- **$id** (required) - the ID of the record to delete.
- **$target_table** (optional) - the name of the database table. By default, the Model will assume the target table is equal to the value in the first URL segment.

## What Gets Returned?


If the method successfully deletes the record, it returns `true`. Otherwise, it returns `false`.

## Example


The code sample below demonstrates how to use the delete() method to delete a record from the database.

```php
// ID of the record to delete
$id = 123; 
// Name of the target table
$target_table = 'products'; 
$is_deleted = $this->model->delete($id, $target_table);
if ($is_deleted) {
echo "Record with ID {$id} was successfully deleted from the {$target_table} table.";
} else {
echo "Failed to delete record with ID {$id} from the {$target_table} table.";
}
```

## Video Tutorial: Creating, Updating & Deleteing Records


The video below demonstrates how how to create, update and delete database records using Trongate's Model class.


https://www.youtube.com/watch?v=-3jZY3iO3Is

