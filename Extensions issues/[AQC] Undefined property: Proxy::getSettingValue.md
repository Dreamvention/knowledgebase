### Opencart version

2.3.0.2

### Issue

Notice: Undefined property: Proxy::getSettingValue in /home4/r83167vipf/public_html/catalog/model/extension/d_quickcheckout/account.php on line 62

##  Solution path

In the `catalog/model/extension/d_quickcheckout/account.php` file on line 128 replace `getSettingValue()` function by the `getSetting()` function.


##  Additional information

Screenshot: http://i.imgur.com/kkcGKmP.png
