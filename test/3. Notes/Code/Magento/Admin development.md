---
Created at: 2024-03-06
Source:
  - https://developer.adobe.com/commerce/php/tutorials/admin/create-admin-page/
  - https://developer.adobe.com/commerce/frontend-core/ui-components/components/form/
  - https://developer.adobe.com/commerce/frontend-core/ui-components/components/listing-grid/
  - https://developer.adobe.com/commerce/php/development/components/add-admin-grid/
  - https://developer.adobe.com/commerce/frontend-core/ui-components/concepts/modifier/ 
Context: 
tags:
---
#### 1. Create admin module, admin page
Tạo file theo directory structure

```
MyCompany
	|-- ExampleAdminNewPage
	    |
	    |-- Controller
	    |   |-- Adminhtml
	    |       |-- HelloWorld
	    |           |-- Index.php
	    |-- etc	
	    |   |-- adminhtml	
	    |   |   |-- menu.xml	
	    |   |   |-- routes.xml	
	    |   |-- module.xml	
	    |-- view	
	    |   |-- adminhtml	
	    |       |-- layout	
	    |       |   |-- exampleadminnewpage_helloworld_index.xml	
	    |       |-- templates	
	    |           |-- helloworld.phtml	
	    |-- composer.json
```

#### 2. Listing/form component
#### 3. PHP modify UI component 
- `modifyData()`: for modifying UI component's data (for example, the list of options for a select element)
- `modifyMeta()`: for modifying UI component's metadata (for example, name, label, description, type)
	i) Tạo pool modified :
	```
		<type name="%YourNamespce\YourModule\Ui\DataProvider\YourDataProviderClass%">
		    <arguments>
		        <argument name="pool" xsi:type="object">%YourNamespace\YourModule\DataProvider\Modifier\Pool%</argument>
		    </arguments>
		</type>
	```
	ii) Khai báo class modified:
	```
	<virtualType name="%YourNamespace\YourModule\DataProvider\Modifier\Pool%" type="Magento\Ui\DataProvider\Modifier\Pool">
	     <arguments>
	         <argument name="modifiers" xsi:type="array">
	             <item name="modifier_name" xsi:type="array">
	                 <item name="class" xsi:type="string">%YourNamespce\YourModule\Modifier\YourModifierClass%</item>
	                 <item name="sortOrder" xsi:type="number">10</item>
	             </item>
	         </argument>
	     </arguments>
	</virtualType>
	```
	iii) Class modified extend  \\Magento\\Ui\\DataProvider\\Modifier\\ModifierInterface
	