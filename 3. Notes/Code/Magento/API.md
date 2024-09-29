### Thêm config vào graphql:
- Thêm field vào schema.graphqls:
```
	type StoreConfig {
		section_group_field : String  @doc(description: "Extended Config Data - section/group/field")
	}
```
- Thêm value vào etc/graphql/di.xml:
```
	<?xml version="1.0" ?>
	<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
	  <type name="Magento\StoreGraphQl\Model\Resolver\Store\StoreConfigDataProvider">
		<arguments>
		  <argument name="extendedConfigData" xsi:type="array">
			<item name="section_group_field" xsi:type="string">section/group/field</item>
		  </argument>
		</arguments>
	  </type>
	</config>
```

### Thêm biến mặc định vào request api:
- File di.xml định nghĩa biến:
```
<type name="Magento\Webapi\Controller\Rest\ParamsOverrider">
	<arguments>
		<argument name="paramOverriders" xsi:type="array">
			<item name="%my_value%" xsi:type="object">VENDOR\MODULE\Controller\Rest\ParamOverriderMyValue</item>
		</argument>
	</arguments>
</type>	
```
- File webapi.xml dùng biến đã định nghĩa cho các request api:
```
<route url="/V1/example/me/service" method="GET">
	<service class="Magento\Customer\Api\GroupRepositoryInterface" method="getById"/>
	<resources>
		<resource ref="Magento_Customer::group"/>
	</resources>
	<data>
		<parameter name="myValue" force="true">%my_value%</parameter>
	</data>
</route>
```

### Limit input:
- GraphQL và REST đều có limit của input item và page size -> Có thể sửa trong admin.

