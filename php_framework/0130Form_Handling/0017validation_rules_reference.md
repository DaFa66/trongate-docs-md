# Validation Rules Reference


The following table lists all of Trongate's built-in form validation rules, including those for file and image uploads.


| Rule | Parameter | Description | Example |
| ---|---|---|---|
| **allowed_types** | Yes | Specifies the allowed file extensions (e.g., gif, jpg, png). | allowed_types[gif,jpg,jpeg,png] |
| **decimal** | No | Returns FALSE if posted value is not numeric with at least one decimal place. | decimal |
| **differs** | Yes | Returns FALSE if form element matches another specified form element. | differs[name] |
| **exact_length** | Yes | Returns FALSE unless posted value has a string length equal to specified value. | exact_length[12] |
| **greater_than** | Yes | Returns FALSE unless posted value is greater than specified value. | greater_than[17] |
| **integer** | No | Returns FALSE if posted value is not an integer (i.e., not a whole number). | integer |
| **less_than** | Yes | Returns FALSE unless posted value is less than specified value. | less_than[31] |
| **max_height** | Yes | Specifies the maximum height for images (in pixels). | max_height[1200] |
| **max_length** | Yes | Returns FALSE if posted value has a string length greater than specified value. | max_length[75] |
| **max_size** | Yes | Specifies the maximum file size in kilobytes (e.g., 2000 for 2MB). | max_size[2000] |
| **max_width** | Yes | Specifies the maximum width for images (in pixels). | max_width[1200] |
| **matches** | Yes | Returns FALSE if posted value does not match another specified form element. | matches[password] |
| **min_height** | Yes | Specifies the minimum height for images (in pixels). | min_height[100] |
| **min_length** | Yes | Returns FALSE if posted value has a string length less than specified value. | min_length[3] |
| **min_width** | Yes | Specifies the minimum width for images (in pixels). | min_width[100] |
| **numeric** | No | Returns FALSE if posted value is not numeric. | numeric |
| **required** | No | Returns FALSE if posted value is empty. | required |
| **square** | No | Ensures the image is square (width equals height). | square |
| **valid_datepicker_eu** | No | Returns FALSE if posted value is not a valid datepicker value of the European format dd-mm-yyyy. | valid_datepicker_eu |
| **valid_datepicker_us** | No | Returns FALSE unless posted value is a valid datepicker value of the United States of America format mm-dd-yyyy. | valid_datepicker_us |
| **valid_datetimepicker_eu** | No | Returns FALSE if posted value is not a valid datetime picker value. | valid_datetimepicker_eu |
| **valid_datetimepicker_us** | No | Returns FALSE if posted value is not a valid datetime picker value. | valid_datetimepicker_us |
| **valid_email** | No | Returns FALSE if posted value is not formatted like an email address. | valid_email |
| **valid_time** | No | Returns FALSE if posted value is not a valid time. | valid_time |

