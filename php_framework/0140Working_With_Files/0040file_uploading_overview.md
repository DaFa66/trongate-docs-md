# File Uploading - An Overview


Trongate provides the necessary tools to build custom file uploaders. The process of building a file uploader is similar to building any other form, but with a few additional steps to handle the file itself.


Here is a list of the main components that make up a custom file uploader:


- **A webpage with a file upload form:** This is the user interface that allows users to select a file and submit it to the server.
- **A method for receiving post requests from the uploader:** This is the server-side code that handles the file once it has been submitted by the user.
- **Some validation tests:** These ensure that the submitted file meets the requirements set by the application (e.g., file type, size).
- **A means of gracefully dealing with errors:** This includes handling errors that occur during validation, as well as errors that may happen during the file upload process.
- **A destination directory where files are to be uploaded to:** This is the location on the server where the uploaded file will be saved.
- **A little bit of configuration:** This includes setting up the destination directory and any other settings that the application requires.
- **A success message or page:** This is the message or page that is displayed to the user once the file has been successfully uploaded.


Most of these components are similar to what you would expect in any form-building scenario. The upcoming sections of this chapter will provide a detailed guide on how to build each of these components and put them together to create a custom file uploader using Trongate.


---

## Trongate’s Two Upload Methods


The main Trongate class (Trongate.php) contains two distinct methods for handling file uploads: upload_file() and upload_picture(). While both methods facilitate file uploads, they serve different purposes and are optimized for different scenarios.

### The upload_file() Method


The upload_file() method is designed for general-purpose file uploads. It handles the basic process of moving a file from a temporary location to its final destination on your server. This method is ideal when you need to:


- Upload non-image files (PDFs, text files, documents, etc.)
- Upload images without requiring any additional processing
- Perform basic file operations without any specialized handling

### The upload_picture() Method


The upload_picture() method is specifically designed for handling image uploads that require additional processing. Beyond the basic upload functionality, this method can:


- Automatically resize images to meet specified dimensions
- Generate thumbnails of uploaded images
- Handle image-specific validation and processing

### Choosing the Right Method


When building a file uploader, selecting the appropriate method is crucial. Here's a guide to help you make the right choice:

#### Use upload_file() when:


- You're uploading non-image files (documents, PDFs, etc.)
- You need to upload images but don't require any resizing or thumbnail generation
- You want simple, straightforward file handling without additional processing

#### Use upload_picture() when:


- You're working specifically with image files (JPEG, PNG, GIF, etc.)
- You need automatic image resizing capabilities
- You want to generate thumbnails automatically
- You require image-specific processing or validation

### Handling Mixed File Types


If your application needs to handle both image and non-image files, you can implement logic to determine which method to use based on the file type. Here's an example:

```php
$file_type = mime_content_type($_FILES['userfile']['tmp_name']);

if (strpos($file_type, 'image/') === 0) {
    // Handle as an image using upload_picture()
    $result = $this->upload_picture($config);
} else {
    // Handle as a regular file using upload_file()
    $result = $this->upload_file($config);
}
```

> [!TIP]
> **Best Practices**
>
> While it might be tempting to use `upload_file()` for all uploads to keep things simple, it's recommended to use `upload_picture()` when working with images that require processing. This ensures you get the benefit of Trongate's built-in image handling capabilities and keeps your code clean and maintainable.



In the next sections, we'll look at practical examples of how to implement both types of uploaders and explore their configuration options in detail.

