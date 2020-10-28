## Opencart version

2.1.0.2

## Issue

Cart arrows to change product quantity on checkout page not working
These arrows: http://i.imgur.com/7lqPsFg.png

##  Solution path

Add two foreachs inside `update()` method
in the file
`/catalog/controller/extension/d_quickcheckout/cart.php`

Foreach 1:
```php
foreach ($_POST['cart'] as $key => $value) {
      foreach ($_SESSION['default']['cart']['products'] as $key2 => $value2) {
          if ($value2['key'] == $key) {
              $_SESSION['default']['cart']['products'][$key2]['quantity'] = $value;
          }
      }
  }
```

Foreach 2:
```php
foreach ($_POST['cart'] as $key => $value) {
      foreach ($data['session']['cart']['products'] as $key2 => $value2) {
          if ($value2['key'] == $key) {
              $data['session']['cart']['products'][$key2]['quantity'] = $value;
          }
      }
  }
```

##  Additional information

Screenshot: http://i.imgur.com/BhwRLys.png


### Update 1:
There is something wrong with .tag files.
You may install the AQC v6.6.5
