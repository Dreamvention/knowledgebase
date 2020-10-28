## Opencart version

3.0.3.2, 3.0.2.0

## Issue

Error 500 when trying to refresh modifications

##  Solution path

Reason: It's because some modification doesn't have `<add>` tag.

Add if-condition to prevent modifications without `<add>` tag here:
`/admin/controller/marketplace/modification.php`

```php
if ($operation->getElementsByTagName('add')->item(0) == null) {
  continue;
}
```

##  Additional information

Screenshot: http://i.imgur.com/Ryla58w.png
