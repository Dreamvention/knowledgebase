# Opencart version

2.3.0.2

# Issue

Ajax Quick Checkout not showing up in OpenCart 2.3.0.2 store

#  Solution path

Just add this modification:

```xml
<?xml version="1.0" encoding="utf-8"?>
<modification>
  <name>d_quickcheckout_oc2302_fix</name>
	<code>d_quickcheckout_oc2302_fix</code>
	<description>Ajax Quick Checkout fix for the OpenCart 2.3.0.2</description>
	<version>1.0.0</version>
	<author>Dreamvention</author>
	<link>http://dreamvention.com</link>

	<file path="catalog/controller/checkout/checkout.php">
		<operation error="skip">
			<search><![CDATA[$this->response->setOutput($this->load->view('checkout/checkout', $data));]]></search>
            <add position="replace"><![CDATA[	
   

				// AJAX QUICK CHECKOUT FIX


				if($this->config->get( 'd_quickcheckout_status')){
            $this->load->model('extension/d_quickcheckout/view');
            $supports = $this->model_extension_d_quickcheckout_view->browserSupported();
            if($supports){
                if(true){
                    $template = 'd_quickcheckout';
                    $this->response->setOutput($this->load->view($this->model_extension_d_quickcheckout_view->template('checkout/'.$template), $data));
                }else{
                    $html_dom = new d_simple_html_dom();
                    $html_dom->load((string)$output, $lowercase = true, $stripRN = false, $defaultBRText = DEFAULT_BR_TEXT);
                    $html_dom->find('body > #content', 0)->innertext = $data['d_quickcheckout'];
                    
                    $this->response->setOutput((string)$html_dom);
                }
            }
            
        }


				// AJAX QUICK CHECKOUT FIX - END


			]]></add>
		</operation>
  </file>
						
</modification>
```

#  Additional information

Event `view_checkout_checkout_after` not firing
