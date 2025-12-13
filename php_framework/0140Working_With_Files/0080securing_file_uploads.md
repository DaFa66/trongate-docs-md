# Securing File Uploads

## Built-in Security Features


Trongate provides a comprehensive suite of security features designed to ensure that file uploads are handled safely and efficiently.

### File Validation


Trongate's [Validation class](../../reference/class_reference/The_Validation_Class) offers extensive control over allowed file types and characteristics. For example:

```php
$validation_str = 'allowed_types[gif,jpg,jpeg,png,webp]|max_size[2000]|max_width[1200]|max_height[1200]';
$this->validation->set_rules('picture', 'item picture', $validation_str);
```


Trongate implements several security measures during file validation, including:


- MIME type verification using PHP's finfo_file()
- Automatic path traversal protection to prevent directory manipulation
- Built-in protection against upload-based PHP code execution
- Automatic file extension normalization and validation
- Content scanning to detect potential security threats in the file

### File Upload Settings


Settings pertaining to upload behavior can be declared inside modules. The framework includes several built-in protections, such as:


- Automatic validation of upload destinations for proper permissions and security
- Prevention of uploads to restricted system directories
- Memory usage monitoring for safe image processing
- Secure file naming system that prevents naming conflicts


Example settings configuration:

```php
function _init_picture_settings() { 
    $picture_settings['max_file_size'] = 2000;
    $picture_settings['max_width'] = 1200;
    $picture_settings['max_height'] = 1200;
    $picture_settings['destination'] = 'pictures';
    $picture_settings['upload_to_module'] = true;
    return $picture_settings;
}
```

## Framework Philosophy


Trongate's approach to file uploading is designed to provide essential security features out of the box while allowing flexibility for additional measures. The framework emphasizes:


- Robust security features to protect against common vulnerabilities
- Efficient and maintainable core implementation
- Flexibility to extend and customize security measures as needed

## Example Implementation


Here's a typical implementation:

```php
class Upload extends Trongate {
    
    private $acceptable_file_types = ['jpg', 'jpeg', 'png', 'gif'];
    
    function upload_file() {
        $this->module('trongate_security');
        $this->trongate_security->_make_sure_allowed();

        $validation_str = 'allowed_types['.implode(',', $this->acceptable_file_types).']';
        $validation_str.= '|max_size[2000]';
        
        $this->validation->set_rules('file', 'File', $validation_str);
        $result = $this->validation->run();

        if ($result === true) {
            // proceed with upload
            $data['destination'] = 'uploads/files';
            $data['upload_to_module'] = false;
            $uploaded_data = $this->upload_file($data);
        }
    }
}
```

## Making Security Decisions


When evaluating if you need additional security measures, consider:


- Who can upload files?
- What types of files are allowed?
- How sensitive is your application?
- What are the consequences of a malicious upload?


Based on these answers, you can determine if Trongate's built-in features are sufficient or if you need additional security measures.

