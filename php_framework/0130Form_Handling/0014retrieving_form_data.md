# Retrieving Form Data


In Trongate, retrieving data submitted through HTML forms is both straightforward and secure. The framework provides a range of tools to help you access, clean, and process form data effectively. Whether you're working with standard form submissions or JSON payloads, Trongate ensures consistency and simplicity in handling user inputs.

## Form Data Handling in Trongate


Trongate supports retrieving data across all HTTP methods (GET, POST, PUT, PATCH, DELETE). Form data can be retrieved seamlessly, whether it is submitted via form-encoded content or as JSON payloads. Additionally, the framework includes features to clean and normalise user input where required.

### The post() Function


The post() function is a powerful tool for accessing form data. It allows you to retrieve data from any HTTP request and works with both form-encoded and JSON payloads. The function also includes an optional cleanup mechanism for trimming whitespace and normalising internal spaces.

#### Basic Usage


To retrieve the value of a specific form field, call the `post()` function with the field name:

```php
$task_title = post('task_title');
```


This will return the value of the `task_title` field. If the field does not exist, the function will return an empty string.

#### Cleaning Up Data


By passing `true` as the second argument to post(), you can clean up the retrieved data. This process trims any leading or trailing spaces and reduces multiple spaces within the string to a single space:

```php
$task_title = post('task_title', true);
```

> [!NOTE]
> **Just To Let You Know...**
>
> **Clarification:** The second argument (`true`) ensures that the retrieved value is cleaned up. This means:
> 
> 
> - Leading and trailing spaces are removed.
> - Multiple internal spaces are replaced with a single space.
> 
> 
> Therefore, if a user submits a value of:
> 
> ```
> Michael           Jackson
> ```
> 
> 
> The cleaned result will be:
> 
> ```
> Michael Jackson
> ```


## Working with Form Data in Controllers


Below is an example of how you might retrieve and process form data in a Trongate controller:

```php
public function submit(): void {
    $this->module('trongate_security');
    $this->trongate_security->_make_sure_allowed();

    $submit = post('submit', true);

    if ($submit === 'Submit') {
        // Retrieve and clean form data
        $task_title = post('task_title', true);
        $task_description = post('task_description', true);
        $complete = post('complete', true);

        // Prepare data for the database
        $data = [
            'task_title' => $task_title,
            'task_description' => $task_description,
            'complete' => ($complete === '1' ? 1 : 0),
        ];

        // Insert or update the record
        $update_id = segment(3, 'int');
        if ($update_id > 0) {
            $this->model->update($update_id, $data, 'tasks');
            $flash_msg = 'The record was successfully updated';
        } else {
            $update_id = $this->model->insert($data, 'tasks');
            $flash_msg = 'The record was successfully created';
        }

        set_flashdata($flash_msg);
        redirect('tasks/show/' . $update_id);
    }
}
```

## Conclusion


Retrieving form data in Trongate is designed to be straightforward, secure, and efficient. By using tools like the `post()` function, you can handle user input with confidence, whether it originates from standard HTML forms or complex JSON payloads. This consistent approach ensures a smooth development experience for handling form submissions across different scenarios.

