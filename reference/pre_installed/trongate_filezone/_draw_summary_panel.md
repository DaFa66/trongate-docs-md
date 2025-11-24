# _draw_summary_panel()


function _draw_summary_panel(int $update_id, array $filezone_settings): void

## Description

Renders the summary panel for a given update ID and Filezone settings.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $update_id | int | The ID of the update. | N/A |
| $filezone_settings | array | Settings related to the Filezone. | N/A |

## Return Value


| Type | Description |
| ---|---|
| void | N/A |

## Example Usage


The code below demonstrates how to render a Filezone summary panel, within a view file.

```
<?= Modules::run('filezone/_draw_summary_panel', $update_id, $filezone_settings) ?>
```

NOTE:  In order for the summary panel to be succesfully rendered, the code above would be passed into a view file.  Also, an array of key / value pairs (in this instance, named as **$filezone_settings**) should also be passed into the view file.   The code sample below shows an example of Filezone settings being initialized from within a controller file.

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
