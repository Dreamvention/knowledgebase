# Opencart version
3.0.2.0

# Problem type
Opencart default issues

# Issue
Notice: Trying to access array offset on value of type null in /var/www/vhosts/tekstgraveren.nl/storage/vendor/scss.inc.php on line 1753Notice: Trying to access array offset on value of type null in /var/www/vhosts/tekstgraveren.nl/storage/vendor/scss.inc.php on line 1753Notice: Trying to access array offset on value of type null in /var/www/vhosts/tekstgraveren.nl/storage/vendor/scss.inc.php on line 1753Notice: Trying to access array offset on value of type null in /var/www/vhosts/tekstgraveren.nl/storage/vendor/scss.inc.php on line 1753Notice: Trying to access array offset on value of type null in /var/www/vhosts/tekstgraveren.nl/storage/vendor/scss.inc.php on line 1753Notice: Trying to access array offset on value of type null in /var/www/vhosts/tekstgraveren.nl/storage/vendor/scss.inc.php on line 1753Notice: Trying to access array offset on value of type null in /var/www/vhosts/tekstgraveren.nl/storage/vendor/scss.inc.php on line 1753Notice: Trying to access array offset on value of type null in /var/www/vhosts/tekstgraveren.nl/storage/vendor/scss.inc.php on line 1753Notice: Trying to access array offset on value of type null in
<br><br>Example: http://i.imgur.com/deKtbbY.png

#  Solution path
You might try and change the code in /storage/vendor/scss.inc.php , line 1753 to:
```php
if (is_array($key)) $key = $key[1];
```

# Additional information
Forum thread: https://forum.opencart.com/viewtopic.php?t=212652
