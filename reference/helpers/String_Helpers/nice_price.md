# nice_price()


function nice_price(float $num, ?string $currency_symbol = null): string|float

## Description

Formats a number as a price with commas for thousands and optionally adds a currency symbol. If the formatted price is a whole number, decimals are removed.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $num | float | The number to be formatted as a price. | N/A |
| $currency_symbol | string\|null | Optional. The currency symbol to prepend to the price. | null |

## Return Value


| Type | Description |
| ---|---|
| string\|float | Returns the formatted price. If no decimals, returns as float, otherwise as string with currency symbol if specified. |

## Example Usage

```
echo nice_price(123456.00); // Output: 123,456
echo nice_price(123456.78, '$'); // Output: $123,456.78
```
