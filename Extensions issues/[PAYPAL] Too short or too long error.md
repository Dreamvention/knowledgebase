## Opencart version

3.0.3.2, 3.0.2.0, 2.3.0.2 etc.

## Issue

Error: Value is too short or too long

##  Solution path

Reason: Name of product is too long.

Add substring to name here:
/catalog/controller/extension/payment/paypal.php

```php
public function createOrder() {

...

  foreach ($this->cart->getProducts() as $product) {
    $product_price = number_format($this->currency->format($product['price'], $currency_code, $currency_value, false), 2, '.', '');


    // LONG NAME FIX
    $product_name = $product['name'];
    if (utf8_strlen($product_name) > 100) {
      $product_name = mb_substr($product_name, 0, 142, "utf-8");
    }

    // OR

    if (strlen($product_name) > 100) {
			$product_name = substr($product_name, 0, 99);
		}


    $item_info[] = array(
      'name' => $product_name,
      'sku' => $product['model'],
      'url' => $this->url->link('product/product', 'product_id=' . $product['product_id'], true),
      'quantity' => $product['quantity'],
      'unit_amount' => array(
        'currency_code' => $currency_code,
        'value' => $product_price
      )
    );

    $item_total += $product_price * $product['quantity'];
  }
```

##  Additional information

Screenshot: http://i.imgur.com/TB0FlYP.png




