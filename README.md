# Split Large HTML String

A PHP library that splits or truncates large HTML strings into smaller parts based on a given length — while preserving valid HTML tag structure.

## Installation

### Direct include

```php
require_once 'path/to/TruncateHTML.php';
```

### Via Composer (GitHub repository)

Add the repository to your `composer.json`:

```json
{
  "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/shamimmoeen/split-large-html-string"
    }
  ],
  "require": {
    "shamimmoeen/split-large-html-string": "dev-master"
  }
}
```

Then run `composer install`.

## Usage

```php
$truncate = new TruncateHTML();
$truncate->set_length(80);       // Target split length (characters of plain text)
$truncate->set_max_length(100);  // Maximum allowed length before forcing a split
$truncate->set_content($html);
```

### Truncate

Returns the first chunk of the HTML string, cut at the nearest safe boundary:

```php
$result = $truncate->get_truncated();
```

### Split

Splits the entire HTML string into an array of parts. Joining them produces the original string:

```php
$parts = $truncate->get_splitted();

// $parts[0] . $parts[1] . ... === $html
```

## How it works

- `length` — the target character count (plain text, excluding tags) at which to look for a split point.
- `max_length` — the upper bound. If completing a parent element would exceed this, the split happens before that element instead.

The library splits at parent-element boundaries, so each chunk contains complete, well-formed HTML.

## Running tests

```bash
composer install
composer test
```

## License

GPL-3.0-or-later — see [LICENSE](LICENSE) for details.
