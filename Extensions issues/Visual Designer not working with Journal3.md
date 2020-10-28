If the product description is not taken from the Visual Designer module, but the default description is taken<br>
Just add this modification:

<h2>d_visualdesigner_journal3_fix</h2>

```xml
<?xml version="1.0" encoding="utf-8"?>
<modification>
  <name>d_visualdesigner_journal3_fix</name>
	<code>d_visualdesigner_journal3_fix</code>
	<description>Visual Designer fix for the Journal3 theme</description>
	<version>1.0.0</version>
	<author>Dreamvention</author>
	<link>http://dreamvention.com</link>

	<file path="catalog/controller/journal3/product_tabs.php">
		<operation error="skip">
			<search><![CDATA[return $this->renderView('journal3/module/product_tabs', $data);]]></search>
            <add position="before"><![CDATA[	
   

				// VISUAL DESIGNER FIX


				if(isset($data["items"][0]["content"])){
					$designer_data = array(
						'config' => 'product',
						'content' => $data["items"][0]["content"],
						'header' => &$data['header'],
						'field_name' => 'product_description['.(int)$this->config->get('config_language_id').'][description]',
						'id' => $this->request->get['product_id']
					);	

					$data["items"][0]["content"] = $this->load->controller('extension/d_visual_designer/designer', $designer_data);

					$data["items"][0]["content"] = html_entity_decode($data["items"][0]["content"], ENT_QUOTES, 'UTF-8');
				}


				// VISUAL DESIGNER FIX - END


			]]></add>
		</operation>
  </file>
						
</modification>
```
