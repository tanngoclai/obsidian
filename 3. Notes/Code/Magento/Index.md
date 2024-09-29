---
Created at: 2024-03-06
Source:
  - https://developer.adobe.com/commerce/php/development/components/indexing/
  - https://developer.adobe.com/commerce/php/development/components/indexing/optimization/
  - https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html
  - https://developer.adobe.com/commerce/php/development/components/indexing/custom-indexer/
Context: 
tags:
---
![[Pasted image 20240306150538.png]]

#### 1. Dùng use_application_lock (since 2.4.3)
``` 
	env.php
		return [
			'indexer' => [
				'use_application_lock' => true
			]
		];
```
- Khi reindex process bị lỗi sẽ lấy index  đúng hơn (không hiểu kiểu gì nhưng đại ý là vậy).
#### 2. Mview
- File mview.xml để xác định sự thay đổi trên db tương ứng với indexer nào -> sau đó thực hiện hàm execute trong class được khai báo
- Các bảng được subscribed sẽ được tạo MySQL trigger để theo dõi INSERT, UPDATE, SAVE.

```
	<view id="catalog_category_product" class="Magento\Catalog\Model\Indexer\Category\Product" group="indexer">
	  <subscriptions>
		<table name="catalog_category_entity" entity_column="entity_id" />
		<table name="catalog_category_entity_int" entity_column="entity_id" />
	  </subscriptions>
	</view>
```
- Change log table là các bảng: <INDEXER_TABLE_NAME> + \_cl
#### 3. Indexer optimization
- max_heap_table_size
- tmp_table_size
- BatchSizeManagementInterface
- IndexTableRowSizeEstimatorInterface
- Index catalogsearch_fulltext:
	- `partial_reindex` - represents how many products will be processed in a partial reindex.
	- `elastic_save` - represents how many products will be saved as a batch into Elasticsearch.
	- `mysql_get` - represents how many searchable products will be retrieved from Mysql.
### 4. Indexer table switching
- Để không bị gián đoạn khi index -> sử dụng các bảng <table_name>\_ replica
#### 5. Customer group
- Nếu nhiều customer group, nhiều website thì index Product Price và Catalog Rule rất lớn. Default là enable mọi website cho mọi customer group -> nên disable customer group khỏi các website không cần thiết.
#### 6. Parallel mode
- Run parallel mode sẽ reindex trên nhiều threads, tiết kiệm time hơn. Cần enable pcntl của PHP.
	- `Catalog Search Fulltext` can be paralleled by store views (default enabled).
	- `Category Product` can be paralleled by store views (default enabled).
	- `Catalog Price` can be paralleled by website and customer groups, websites.
	- `Catalog Permissions` can be paralleled by customer groups.
#### 7. Create custom indexer
- `indexer.xml` (`view_id`: The ID of the view element that is defined in the `mview.xml` configuration file).
- `mview.xml`.
- Class indexer implements `\Magento\Framework\Indexer\ActionInterface`, `\Magento\Framework\Mview\ActionInterface`.
