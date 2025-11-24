# Image Uploader Example


Let's walk through building an image uploader using Trongate's upload_picture() method. This example will demonstrate creating a secure image uploader that includes automatic image processing capabilities.

> [!NOTE]
> **Just To Let You Know...**
>
> The following example pertains to a hypothetical custom module named as 'products'.


## Step 1: Create the Upload Form


Create a view file in your module's views directory:

```vf
<h1>Upload Product Picture</h1>
<?= flashdata() ?>
<div class="card">
    <div class="card-heading">
        Upload Picture
    </div>
    <div class="card-body">
        <?php
        echo validation_errors();
        echo form_open_upload('products/submit_upload_picture/'.$update_id);
        echo form_label('Select Picture:', 'picture');
        echo form_file_select('picture', ['accept' => '.jpg, .jpeg, .png, .gif']);
        echo form_submit('submit', 'Upload Picture');
        echo form_close();
        ?>
    </div>
</div>
```

## Step 2: Initialize Picture Settings


Create a method in your controller to define image settings:

```php
private function _init_picture_settings() { 
    $picture_settings['max_file_size'] = 2000;
    $picture_settings['max_width'] = 1200;
    $picture_settings['max_height'] = 1200;
    $picture_settings['resized_max_width'] = 450;
    $picture_settings['resized_max_height'] = 450;
    $picture_settings['destination'] = 'products_pics';
    $picture_settings['target_column_name'] = 'picture';
    $picture_settings['thumbnail_dir'] = 'products_pics_thumbnails';
    $picture_settings['thumbnail_max_width'] = 120;
    $picture_settings['thumbnail_max_height'] = 120;
    $picture_settings['upload_to_module'] = true;
    $picture_settings['make_rand_name'] = false;
    return $picture_settings;
}
```

## Step 3: Create the Upload Handler


Add the upload handler method to your controller:

```php
function submit_upload_picture($update_id) {
    $this->module('trongate_security');
    $this->trongate_security->_make_sure_allowed();

    if ($_FILES['picture']['name'] == '') {
        redirect($_SERVER['HTTP_REFERER']);
    }

    $picture_settings = $this->_init_picture_settings();
    extract($picture_settings);

    $validation_str = 'allowed_types[gif,jpg,jpeg,png]|max_size['.$max_file_size.']|max_width['.$max_width.']|max_height['.$max_height.']';
    $this->validation->set_rules('picture', 'item picture', $validation_str);

    $result = $this->validation->run();

    if ($result == true) {
        $config['destination'] = $destination.'/'.$update_id;
        $config['max_width'] = $resized_max_width;
        $config['max_height'] = $resized_max_height;

        if ($thumbnail_dir !== '') {
            $config['thumbnail_dir'] = $thumbnail_dir.'/'.$update_id;
            $config['thumbnail_max_width'] = $thumbnail_max_width;
            $config['thumbnail_max_height'] = $thumbnail_max_height;
        }

        $config['upload_to_module'] = (!isset($picture_settings['upload_to_module']) ? false : $picture_settings['upload_to_module']);
        $config['make_rand_name'] = $picture_settings['make_rand_name'] ?? false;

        $file_info = $this->upload_picture($config);

        //update the database with the name of the uploaded file
        $data[$target_column_name] = $file_info['file_name'];
        $this->model->update($update_id, $data);

        $flash_msg = 'The picture was successfully uploaded';
        set_flashdata($flash_msg);
        redirect($_SERVER['HTTP_REFERER']);

    } else {
        redirect($_SERVER['HTTP_REFERER']);
    }
}
```

## Directory Structure


Your module structure should look like this:

```
modules/
    products/
        assets/
            products_pics/         <-- Main images go here
                1/                 <-- Folders named by record ID
                2/
            products_pics_thumbnails/  <-- Thumbnails go here
                1/                 <-- Matching record ID folders
                2/
        controllers/
            Products.php
        views/
            picture_upload_form.php
```

## Understanding Picture Settings


|  |  |  |
| ---|---|---|
| Setting | Description | Default |
| `destination` | Directory where pictures will be uploaded | Required |
| `upload_to_module` | If true, pictures are uploaded to the module's assets directory | false |
| `make_rand_name` | If true, generates a random filename for uploaded pictures | false |
| `target_column_name` | The database column that stores the filename | Required |

> [!TIP]
> **Best Practices**
>
> - Always validate file types to prevent unauthorized file uploads
> - Set appropriate file size limits to prevent server overload
> - Organize images in subdirectories by record ID
> - Store only the filename in the database, not the full path



In the next section, we'll take a closer look at how file validation, including image validation, is handled with Trongate.

