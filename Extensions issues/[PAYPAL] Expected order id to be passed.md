## Opencart version

3.0.3.2, 3.0.2.0, 2.3.0.2 etc.

## Issue

Console error: Expected order id to be passed...<br>
Network responce: {"order_id":"","error":{"warning":"The specified country requires a postal code"}}

##  Solution path

Reason: No postal code

Get postal code from session here:<br>
/catalog/controller/payment/paypal.php<br>
http://i.imgur.com/YIjQPQ2.png

```php
// POST CODE FIX

if(isset($order_info['shipping_postcode']) && strlen($order_info['shipping_postcode']) > 0) {
  $shipping_info['address']['postal_code'] = $order_info['shipping_postcode'];
}
else {
  $shipping_info['address']['postal_code'] = $this->session->data['shipping_address']['postcode'];
}

// POST CODE FIX - END
```
