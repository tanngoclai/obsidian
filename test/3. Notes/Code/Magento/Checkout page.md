---
Created at: 2024-03-07
Source:
  - https://developer.adobe.com/commerce/php/tutorials/frontend/custom-checkout/
Context: 
tags:
---
#### 1. New checkout step
- Tạo js component extend uiComponent. Dùng `Magento_Checkout/js/model/step-navigator` và config sort order để config hiện trước hay sau shipping/payment step.
- Add step vào `checkout_index_index.xml`.
#### 2. New payment method
- Usually, create payment method renderer in `view/frontend/web/js/view/payment/method-renderer/`, extend `Magento/Checkout/view/frontend/web/js/view/payment/default.js`.
- Tạo template `.html` cho renderer.
- Put new method into render list: use `Magento_Checkout/js/model/payment/renderer-list`.
- Implement `\Magento\Checkout\Model\ConfigProviderInterface` to export backend config into `window.checkoutConfig`:
	```
	<type name="Magento\Checkout\Model\CompositeConfigProvider">
	    <arguments>
	        <argument name="configProviders" xsi:type="array">
	            <item name="%Custom_provider_name%" xsi:type="object">MyCustomPaymentConfigProvider</item>
	        </argument>
	    </arguments>
	</type>
	```
- Add new method to `checkout_index_index.xml`.
#### 3. Shipping method
#### 4. Validate info
- Create the validator.
	- Tạo js model chứa function validate, return bool.
	- Dùng `Magento_Ui/js/model/messageList`.
	- 
- Add validator to the validators pool.
- Declare the validation in the checkout layout.
#### 5. Custom field
##### Disable component
- It is loaded but not rendered.
```
<item name="%the_component_to_be_disabled%" xsi:type="array">
    <item name="config" xsi:type="array">
        <item name="componentDisabled" xsi:type="boolean">true</item>
    </item>
</item>
```
##### Remove component
- It is removed, not loaded.
- Unset it from layout processor. Then add custom processor to layout.
``` 
    public function process($jsLayout)
    {
        //%path_to_target_node% is the path to the component's node in checkout_index_index.
        unset($jsLayout['components']['checkout']['children']['steps'][%path_to_target_node%]);
        return $jsLayout;
    }
```
