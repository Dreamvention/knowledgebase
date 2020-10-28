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
// ORDER ID EXPECTED TO BE PASSED - ERROR FIX

// var_dump($this->session->data);

if(isset($order_info['shipping_city']) && strlen($order_info['shipping_city']) > 0) {
  $shipping_info['address']['admin_area_2'] = $order_info['shipping_city'];
}
else if(isset($this->session->data['shipping_address']['city']) && strlen($this->session->data['shipping_address']['city']) > 0) {
  $shipping_info['address']['admin_area_2'] = $this->session->data['shipping_address']['city'];
}
else {
  $shipping_info['address']['admin_area_2'] = "-";
}

if(isset($order_info['shipping_postcode']) && strlen($order_info['shipping_postcode']) > 0) {
  $shipping_info['address']['postal_code'] = $order_info['shipping_postcode'];
}
else {
  $shipping_info['address']['postal_code'] = $this->session->data['shipping_address']['postcode'];
}

// ORDER ID EXPECTED TO BE PASSED - ERROR FIX - END
```
