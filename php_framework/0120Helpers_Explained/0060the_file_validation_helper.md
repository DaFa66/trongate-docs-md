# The File Validation Helper


Trongate is loaded with a variety of features that can assist with the uploading of files such as images. Before exploring Trongate's file validation helper, let's have a reminder of how to draw a file uploader form using Trongate:

```vf
<?php
echo form_open_upload("members/submit_upload_picture/".$update_id);  
echo validation_errors();
echo "Please choose a picture from your computer and then press \"Upload\".";  
echo form_file_select("picture");  
echo form_submit("submit", "Upload");  
echo form_close();
?>
```


The code above could be used to produce a form that looks like this:



    ![screenshot](https://trongate.io/images/29/pic_uploaQqj.png)
    
*Screenshot showing example of file uploader form.*


> [!WARNING]
> The example shown in the screenshot contains some CSS and a little additional HTML to improve the appearance of the uploader form.


## Understanding The Uploader Form


The uploader form, above, starts by invoking the form_open_upload() method.

```vf
echo form_open_upload("members/submit_upload_picture/".$update_id);
```


As can see, an argument has been passed into the method. The argument represents the destination for the uploader form. The destination is the URL where the user is sent to when the form is submitted. The opening line produces the following HTML code:

```vf
<form action="http://localhost/your_app/members/submit_upload_picture/1" method="post" enctype="multipart/form-data">
```

> [!WARNING]
> The assumption being made with this example is that an `$update_id` variable has been passed into the view file. We're also assuming that the `BASE_URL` value is set to:
> 
> ```
> http://localhost/your_app/
> ```
> 
> .



Next, we invoked Trongate's validation_errors() method.

```vf
validation_errors();
```


The `validation_errors()` method displays form validation errors, if there are any.


After displaying some text-based instructions, the next important part of our form is:

```vf
echo form_file_select("picture");
```


The form_file_select method displays a form file uploader field. As you can see, the argument `'picture'` has been passed into the method. The `'picture'` argument represents the name of the file uploader form field. The HTML code that gets generated from the `form_file_select()` method is shown below:

```html
<input type="file" name="picture" value="">
```

> [!WARNING]
> The form_file_select method can accept the following three arguments:
>   
> - name
> - attributes
> 
> 
> What these two attributes represent and how they behave is identical to how ordinary form_input() methods work. See the [Form Helpers API Reference](documentation-ref/list_refs/helpers/form-helpers) for details.



The 'submit' button has been assigned with a name of **'submit'** but the word 'Upload' appears inside the button.

```vf
echo form_submit("submit", "Upload");  
echo form_close();
```


The uploader form is closed by invoking form_close().

