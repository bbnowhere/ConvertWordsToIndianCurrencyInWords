# ConvertWordsToIndianCurrencyInWords

A small PHP utility that converts a decimal-formatted numeric string into Indian rupees and paise written in English words.

```text
123456.78 → One Lakh Twenty Three Thousand Four Hundred Fifty Six rupees and Seven Eight paise
```

## What it does

`IndianCurrencyInWords($number)` splits the supplied string at a decimal point. It converts the integer part using Indian place values and spells each character of the decimal part as a separate digit word. The output uses `rupees` and, when the decimal conversion is non-empty, `paise`.

Indian place values used by the converter include:

- **Thousand** (1,000)
- **Lakh** (100,000)
- **Crore** (10,000,000)

For example, `123456` is grouped as one lakh, twenty-three thousand, four hundred fifty-six. Decimal digits are not converted as a combined number: `.78` becomes “Seven Eight paise.”

## Requirements

- PHP CLI or a PHP runtime capable of loading the source file.
- No external libraries or package manager are required.

## Setup and usage

Clone or download the repository, then run the PHP file from the project directory:

```sh
php IndianCurrencyInWords.php
```

The file includes a built-in example and prints its result when run. To call the function from another PHP script:

```php
<?php
require_once 'IndianCurrencyInWords.php';

echo IndianCurrencyInWords('123456.78');
```

Loading the file also prints its built-in example (`600575`) before the function call, because the example is executed at file scope in the current implementation.

## Examples

| Input string | Output |
| --- | --- |
| `600575.00` | `Six Lakhs Five Hundred Seventy Five rupees` |
| `123456.78` | `One Lakh Twenty Three Thousand Four Hundred Fifty Six rupees and Seven Eight paise` |

The `.00` fractional part produces no paise phrase because zero digits map to empty strings in the implementation.

## Implementation and project structure

- **Language:** PHP
- **Dependencies:** None
- **Source:** [`IndianCurrencyInWords.php`](IndianCurrencyInWords.php)
- **Tests:** No test files or test runner are present in this repository.

The source defines `IndianCurrencyInWords`, `convertIntegerToWords`, and `convertDecimalToWords`. It also runs a sample conversion when loaded.

## Limitations

- Pass a string containing a decimal point, such as `'123456.78'`. The function directly splits on `.` and does not validate the input format; an input without a decimal point can produce a PHP warning and an incomplete result.
- The decimal portion is spoken one digit at a time. The implementation does not enforce a two-digit paise limit, round values, or parse a decimal amount according to numeric rules.
- The integer conversion is designed for up to nine digits (through 99,99,99,999). Longer integer strings return the source's “Sorry This does not support more than 99 Crores” message as the integer words, followed by `rupees`.
- Input is not validated as numeric. Negative signs, separators, and other non-digit characters are unsupported and can lead to incorrect output or PHP notices.
- Zero digits are omitted by the word map. As a result, an integer part of `0` does not produce “Zero,” and a zero-only fractional part does not produce “Zero paise.”
- The word map contains spelling errors for some number words (for example, “fouteen,” “fourty,” and “ninty”); output reflects these source spellings where applicable.

## Contributing

Contributions that clarify or improve the utility are welcome. Please keep documentation and examples aligned with the current implementation.
