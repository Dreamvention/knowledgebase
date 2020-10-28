# catalog/view/theme/journal3/js/checkout.js

1) Comment this line:<br>
[100]<br>
$('.quick-checkout-payment').html(...);

2) Add if-condition:<br>
[107]<br>
if ($('#paypal_form').length == 0) {

Screenshot: http://i.imgur.com/nq4JshC.png

# catalog/view/theme/default/template/extension/payment/paypal.twig

1) Add this style:<br>
.quick-checkout-wrapper .quick-checkout-payment #paypal_express_button.buttons {
	display: block !important;
}

Screenshot: http://i.imgur.com/a3xSLJY.png

# or you can install this modification

```xml

<?xml version="1.0" encoding="utf-8"?>
<modification>
    <name>d_paypal_journal3_fix</name>
    <code>d_paypal_journal3_fix</code>
    <description>PayPal Commerce Platform compatibility fix for Journal 3</description>
    <version>1.0.0</version>
    <author>Dreamvention</author>
    <link>http://dreamvention.com</link>
    <file path="catalog/view/theme/default/template/extension/payment/paypal.twig">
        <operation error="skip">
            <search><![CDATA[<style type="text/css">]]></search>
            <add position="after"><![CDATA[
            .quick-checkout-wrapper .quick-checkout-payment #paypal_express_button.buttons {
	            display: block !important;
            }
            ]]></add>
        </operation>
    </file>
    <file path="catalog/view/theme/journal3/js/checkout.js">
        <operation error="skip">
            <search><![CDATA[$('.quick-checkout-payment').html('<div class="journal-loading-overlay" style="position: relative;"><div class="journal-loading"><i class="fa fa-spinner fa-spin"></i></div></div>');]]></search>
            <add position="replace"><![CDATA[
            //$('.quick-checkout-payment').html('<div class="journal-loading-overlay" style="position: relative;"><div class="journal-loading"><i class="fa fa-spinner fa-spin"></i></div></div>');
            ]]></add>
        </operation>
        <operation error="skip">
            <search><![CDATA[$('.quick-checkout-payment').html(data);]]></search>
            <add position="before"><![CDATA[
            if ($('#paypal_form').length == 0) {
            ]]></add>
        </operation>
        <operation error="skip">
            <search index="1"><![CDATA[$('#quick-checkout-button-confirm, #button-login').button('reset');]]></search>
            <add position="after"><![CDATA[
            }
            ]]></add>
        </operation>
    </file>
</modification>

```

// IMPORTANT: modification operations for JS not working

# extra modification v3.0

```xml
<?xml version="1.0" encoding="utf-8"?>
<modification>
    <name>d_paypal_journal3_fix</name>
    <code>d_paypal_journal3_fix</code>
    <description>PayPal Commerce Platform compatibility fix for Journal 3</description>
    <version>3.0.0</version>
    <author>Dreamvention</author>
    <link>http://dreamvention.com</link>
    <file path="catalog/view/theme/default/template/extension/payment/paypal.twig">
        <operation error="skip">
            <search><![CDATA[<style type="text/css">]]></search>
            <add position="after"><![CDATA[
		.quick-checkout-wrapper .quick-checkout-payment #paypal_express_button.buttons {
			display: block !important;
		}
		.confirm-buttons {
			display: none;
		}
            ]]></add>
        </operation>
        <operation error="skip">
            <search><![CDATA[<script type="text/javascript">]]></search>
            <add position="after"><![CDATA[
            	$(document).on('change', function() {
			setTimeout(function(){ 
				updatePayPalDetails();
			}, 100);
		});

		function updatePayPalDetails() {
			const paymentDetailsBlock = document.querySelector(".checkout-payment-details");
			const confirmButton = document.querySelector(".confirm-buttons");
			if (paymentDetailsBlock.classList.contains("payment-paypal")) {
				confirmButton.style.display = "none";
			}
			else {
				confirmButton.style.display = "flex";
			}
		}
            ]]></add>
        </operation>
    </file>
    <file path="catalog/view/theme/journal3/js/checkout.js">
        <operation error="skip">
            <search><![CDATA[$('.quick-checkout-payment').html('<div class="journal-loading-overlay" style="position: relative;"><div class="journal-loading"><i class="fa fa-spinner fa-spin"></i></div></div>');]]></search>
            <add position="replace"><![CDATA[
            	//$('.quick-checkout-payment').html('<div class="journal-loading-overlay" style="position: relative;"><div class="journal-loading"><i class="fa fa-spinner fa-spin"></i></div></div>');
            ]]></add>
        </operation>
        <operation error="skip">
            <search><![CDATA[$('.quick-checkout-payment').html(data);]]></search>
            <add position="before"><![CDATA[
            	if (data.split('\n')[10] == "#paypal_form {") {
			$(".confirm-section .checkbox input").last().prop('checked', true);
			$(".confirm-section .checkbox input").last().prop('disabled', true);
			if ($('#paypal_form').length == 0) {
            ]]></add>
	    <add position="after"><![CDATA[
            		}	
		}
		else {
			$('.quick-checkout-payment').html(data);
			$(".confirm-section .checkbox input").last().prop('checked', false);
			$(".confirm-section .checkbox input").last().prop('disabled', false);
		}
            ]]></add>
        </operation>
    </file>
    <file path="catalog/view/theme/journal3/template/journal3/checkout/checkout.twig">
        <operation error="skip">
            <search><![CDATA[{{ confirm_block }}]]></search>
            <add position="replace"><![CDATA[
            	{# confirm_block #}
            ]]></add>
        </operation>
        <operation error="skip">
            <search><![CDATA[{{ cart_block }}]]></search>
            <add position="after"><![CDATA[
            	{{ confirm_block }}
            ]]></add>
        </operation>
    </file>
</modification>
```
