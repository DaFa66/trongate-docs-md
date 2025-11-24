# File Uploader Example


Let's walk through building a document uploader using Trongate's upload_file() method. This example will demonstrate creating a secure PDF document uploader with proper validation and error handling.

> [!NOTE]
> **Just To Let You Know...**
>
> The following example pertains to a hypothetical custom module named as 'documents'.


## Step 1: Create the Upload Form


Create a view file (e.g., `upload_form.php`) in your module's views directory:

```vf
<h1>Upload PDF Document</h1>
<?= flashdata() ?>
<div class="card">
    <div class="card-heading">
        Upload PDF File
    </div>
    <div class="card-body">
        <?php
        echo validation_errors();
        echo form_open_upload('documents/submit');
        echo form_label('Select PDF File:', 'userfile');
        echo form_file_select('userfile', ['accept' => '.pdf']);
        echo csrf_field();
        echo form_submit('submit', 'Upload File', ['class' => 'alt']);
        echo form_close();
        ?>
    </div>
</div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> The 'accept' property is an HTML attribute for specifying acceptable file types for uploads. Here's how you can use it:
> 
> ```html
> <input type="file" accept=".jpg, .png, .pdf">
> ```


## Step 2: Create the Controller


Create a controller (e.g., `documents.php`) in your module's controllers directory:

```php
<?php
class Documents extends Trongate {
    
    function upload() {
        $data['view_module'] = 'documents';
        $data['view_file'] = 'upload_form';
        $this->template('admin', $data);
    }

    function submit() {
        // Set validation rules for the file upload
        $this->validation->set_rules('userfile', 'Document', 'required|allowed_types[pdf]|max_size[2048]');
        $result = $this->validation->run();

        if ($result == false) {
            $this->upload(); // Return to form with validation errors
            return;
        }

        // Configure the upload
        $config['destination'] = 'documents'; // Directory inside your module's assets
        $config['upload_to_module'] = true;   // Upload to module's assets directory
        $config['make_rand_name'] = true;     // Generate random filename

        try {
            $result = $this->upload_file($config);
            
            // Optional: Store file information in database
            $data['file_name'] = $result['file_name'];
            $data['file_path'] = $result['file_path'];
            $data['file_type'] = $result['file_type'];
            $data['file_size'] = $result['file_size'];
            $this->model->insert($data, 'documents');

            set_flashdata('The file was successfully uploaded');
            redirect('documents/success');

        } catch (Exception $e) {
            set_flashdata($e->getMessage(), 'error');
            redirect('documents/upload');
        }
    }

    function success() {
        $data['view_module'] = 'documents';
        $data['view_file'] = 'upload_success';
        $this->template('admin', $data);
    }
}
```

## Step 3: Create the Success View


Create a success view file (e.g., `upload_success.php`):

```vf
<div class="card">
    <div class="card-heading">
        Upload Successful
    </div>
    <div class="card-body">
        <?= flashdata() ?>
        <p>Your file has been successfully uploaded.</p>
        <p><?= anchor('documents/upload', 'Upload Another File', array('class' => 'button alt')) ?></p>
    </div>
</div>
```

## Directory Structure


Your module structure should look like this:

```
modules/
    documents/
        assets/
            documents/         <-- Uploaded files go here
        controllers/
            Documents.php
        views/
            upload_form.php
            upload_success.php
```

## Understanding the Configuration Options


|  |  |  |
| ---|---|---|
| Option | Description | Default |
| `destination` | Directory where files will be uploaded | Required |
| `upload_to_module` | If true, files are uploaded to the module's assets directory | false |
| `make_rand_name` | If true, generates a random filename for uploaded files | false |

## File Upload Validation Rules


Trongate provides several validation rules specifically for file uploads:


- `required`: Ensures a file was selected
- `allowed_types[type1,type2]`: Specify allowed file extensions (e.g., pdf,doc,txt)
- `max_size[size_in_kb]`: Maximum file size in kilobytes

> [!TIP]
> **Best Practices**
>
> - Always validate file types to prevent unauthorized file uploads
> - Use `make_rand_name` to prevent filename conflicts and increase security
> - Set appropriate file size limits to prevent server overload
> - Ensure your upload directory has correct permissions (typically 755)


## Handling the Upload Response


On successful upload, upload_file() returns an array containing:


- `file_name`: The name of the uploaded file
- `file_path`: The complete server path to the uploaded file
- `file_type`: The MIME type of the uploaded file
- `file_size`: The size of the uploaded file in bytes


In the next section, we'll explore using the upload_picture() method, which provides additional features specifically for handling image uploads.

