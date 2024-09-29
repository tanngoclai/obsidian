---
Created at: 2024-03-06
Source:
  - https://developer.adobe.com/commerce/php/development/components/attributes/
  - https://developer.adobe.com/commerce/php/development/components/add-attributes/
Context: 
tags:
---
#### Phân biệt với Attribute
- Đều dùng để lưu trữ dữ liệu.
- Extension attribute: attribute được thêm vào khi xử lí dữ liệu của đối tượng, không thực sự được lưu ở db.
	- Để lưu các dữ liệu không thực sự mô tả cho đối tượng, thường là các loại dữ liệu phức tạp hơn attribute thông thường.
	- Được tạo ra bằng cách join các bảng hoặc tính toán từ các từ liệu khác.
	- Để tạo extension attribute:
		- Define attribute trong extension_attributes.xml
		- Dùng afterGetExtensionAttributes để kiểm tra entity có extension attribute trước khi get/set, không có thì create và return empty object.
		- Get/set có 2 cách:
			- Dùng plugin afterGet, afterGetList, afterSave... để lưu data vào extension attribute. 
			- Dùng extensionActions của `\Magento\Framework\EntityManager\Operation\ExtensionPool`, khai báo trong di.xml.

#### Declare extension attributes
`<Module>/etc/extension_attributes.xml`
	```
	<config>
		<extension_attributes for="Path\To\Interface must be implement ExtensibleDataInterface, this object will use this attribute">
			<attribute code="name_of_attribute" type="<datatype>">
			   <resources>
				  <resource ref="permission"/>
			   </resources>
			   <join reference_table="" reference_field="" join_on_field=""> // Use for search, use for getList()
				  <field>fieldname</field> //Select from datatype, use <column> to select from reference_table
			   </join>
			</attribute>
		</extension_attributes>
	</config>
	```