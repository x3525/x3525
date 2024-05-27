---
glightbox: true
icon: material/circle-small
---

# File Inclusion Prevention

## Preventing Directory Traversal

```php
while(substr_count($input, '../', 0)) {
    $input = str_replace('../', '', $input);
};
```

## Web Server Configuration

* [x] `allow_url_fopen = Off`
* [x] `allow_url_include = Off`
