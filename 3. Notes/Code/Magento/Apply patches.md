---
Created at: 2024-02-09
Source:
  - https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/patches/apply.html
  - https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/upgrade/apply-patches.html
Context: Magento Expert
tags:
  - MagentoCloud
---
## 1. Các loại patch

- Patch là 1 file chứa các code thay đổi (giống git diff) chủ yếu để fix bug các module cài qua composer.

| Type | Definition |
| ---- | ---- |
| Custom patches | Patch tự tạo ra. |
| Quality patches | Patch của Magento. |
| Cloud patches | Patch của Magento cho phiên bản Cloud. |

## 2. Cách apply patch

#### 2.1 Composer

1. **Đối tượng:** custom patches
2. **Thực hiện:** 
	- Tạo file patch (diff) và cho vào folder patches/composer.
	- Cài package *cweagans/composer-patches*: `composer require cweagans/composer-patches`
	- Sửa file composer.json để apply patch:
		```
		"extra": {
			"composer-exit-on-patch-failure": true,
			"patches": {
				"<package-name": {
					"<comment>": "<path-patch-without-root-folder>"
				}
			}
		}
		```
	- Chạy composer install để apply patch.
3. **Lưu ý:** path của file bị thay đổi trong file diff là tính từ folder folder code của module được apply, tức là không chứa phần `vendor/<vendor-name>/<module-name>`.

#### 2.2 Command line

1. **Đối tượng:** custom patches
2. **Thực hiện:**
	- Đưa file patch vào folder code.
	- Chạy command: `patch < <path>/<file-name>`
	- Path của file viết trong patch phải tính từ folder root.
3. **Lưu ý:** Khi điền sai path -> cần nhập lại đúng path của file mà patch được apply, nếu có nhiều file thì lần lượt nhập path của từng file.
	![[Pasted image 20240212232118.png]]

### 2.3 Quality patches

1. **Cách 1:** Có thể tự tạo quality patches giống như custom patch và apply bằng cách 2.1 và 2.2.
2. **Cách 2:**
	* Cài `composer require magento/quality-patches`
	* Kiểm tra patch available cho version hiện tại: `./vendor/bin/magento-patches status`
	* Apply patch theo tên patch chính thức của magento: `./vendor/bin/magento-patches apply MAGETWO-95591 MAGETWO-67097`
	- Revert thì thay chữ apply thành chữ revert.
#### 2.4 Cloud

 Với version Magento có Cloud package thì dùng ece-tools để apply patch, yêu cầu có `magento/magento-cloud-patches` and `magento/quality-patches`.
 
1. **Quality patches hoặc Cloud patches** (đại ý là patch do Magento release):
	- Thêm biến QUALITY_PATCHES vào file .magento.env.yaml để list các patch cần apply. Push commit là ở cloud sẽ tự apply patch. Ví dụ:
		```
		stage:
			build:
				QUALITY_PATCHES:
					- MCTEST-1002
					- MCTEST-1003
		```
	- Ở môi trường local cần:
		- Thêm patch vào file như bước trên.
		- Kiểm tra trạng thái patch: `./vendor/bin/ece-patches status
		- Apply patch: `./vendor/bin/ece-patches apply`

2. **Custom patches**
	- Tạo folder m2-hotfixes: `mkdir m2-hotfixes`
	- Copy file patch vào folder trên. **File patch phải có đuôi `.patch`**.
	- Commit file patch là ok. Muốn revert patch thì xóa file patch và deploy lại là được.
	- Ở môi trường local thì tự apply bằng command line.
