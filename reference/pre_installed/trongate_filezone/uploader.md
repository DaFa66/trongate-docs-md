# uploader()


public function uploader(): void

## Description

Renders a page that displays the uploader view. This method is responsible for setting up the necessary data and rendering the uploader view for the Trongate Filezone module, which is a multi-file uploader that allows users to drag and drop files. The method also handles authentication using Trongate's token system.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not take any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return any value. |

## Settings


The Trongate Filezone module is configured using the following settings, which are typically declared inside the main controller file of the respective module:


| Setting | Type | Description |
| ---|---|---|
| targetModule | string | The name of the module where the files will be uploaded. |
| destination | string | The directory within the module where the files will be stored. |
| max_file_size | int | The maximum file size allowed for uploads (in kilobytes). |
| max_width | int | The maximum width allowed for uploaded images (in pixels). |
| max_height | int | The maximum height allowed for uploaded images (in pixels). |
| upload_to_module | bool | A flag indicating whether the files should be uploaded to the module's directory or not. |

## Example Usage


To access the Filezone uploader page, go to your base URL followed by 'trongate_filezone/uploader/module_name/n', replacing 'module_name' with the name of your target module and 'n' with the 'id' of the record for which you'd like to upload files.


In addition, a 'public' method named '_init_filezone_settings' should be added inside the controller file of the target module.  This method should contain settings that are to be applied to the Filezone uploader.  For example:

```php
public function _init_filezone_settings() {
    $data['targetModule'] = 'tasks';
    $data['destination'] = 'tasks_pictures';
    $data['max_file_size'] = 1200;
    $data['max_width'] = 2500;
    $data['max_height'] = 1400;
    $data['upload_to_module'] = true;
    return $data;
}
```
