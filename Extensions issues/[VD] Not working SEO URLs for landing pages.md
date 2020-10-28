## Opencart version

3.0.3.2, 3.0.2.0, 2.3.0.2 etc.

## Issue

Visual Designer Landing: Not working SEO URLs to landing pages

##  Solution path

Method name needs to be changed from
```php
public function seo_url()
```
to
```php
public function seo_url_add_rewrite()
```

##  Additional information

Screenshot: http://i.imgur.com/ih79tb5.png
