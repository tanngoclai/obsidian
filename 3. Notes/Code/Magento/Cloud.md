---
Created at: 2024-03-16
Source:
  - https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli/cloud-cli-overview
  - https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/architecture/pro-develop-deploy-workflow
  - https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/overview
Context: 
tags:
---
#### 0. Cloud Architecture
1. Có 2 plan: starter plan và pro plan:
	- Feature: Đều có feature cơ bản và Paypal, Pro có thêm B2B module, starter muốn có B2B thì mất thêm phí.
	- Infra + deploy: 
		- Đều có CI và unlimited users.
		- Đều có Fastly, image optimize, security, Firewall, New Relic APM
		- Pro có New Relic production và alert.
		- Pro có 3 máy chủ  (IaaS).
	- Environment:
		- Start có 4 loại môi trường: Integration (gồm 2 môi trường test, 2 active branch) + Staging (merge branch integration vào branch staging), Production (branch master), inactive (unlimited branch).
		- Pro có 4 loại như trên và Global (global là nhánh master, không cần deploy lên đâu cả, chỉ là để lưu code và backup cho production, có thể dùng để debug với production data mà không cần down live site).
		- Chỉ support nginx (không apache) và opensearch (không elasticserch, nếu có thể).
	- Backup (snapshot) in Console Cloud: not available for pro environments, environment phải active mới backup được.
#### 1. Architecture & flow:
- Environment là read-only, deploy qua push code, mỗi môi trường có 1 db.
- Rẽ nhánh integration từ staging, rẽ staging từ master.
- Môi trường integration không có new relic và cdn. Có tối đa 2 active branch.
- Flow code, test, deploy là Development > Staging (staging branch) > Production (master branch).
- Pro:
	- **Global**: Nhánh master, clone của production, dùng để debug live site.
	- **Production** environment: master branch -> Live site.
	- **Staging** environment: staging branch -> Site để test, UAT, gần giống live site nhất.
	- **Integration** environment: integration branch -> Site để dev.
	- Staging và production có auto backup, run on Iaas hardware riêng.
	- Cần submit ticket để lấy được backup. Có thể tự tạo backup bằng cli.

![[Pasted image 20240319182601.png]]

  Khi push/merge code vào các branch trên thì Cloud sẽ tự động build & deploy code với môi trường tương ứng nếu branch active 
  Git flow tương tự git flow mới của BS nhưng có thêm nhánh integration để test trước khi lên staging.

- Structure folder:
	- Tuy environment là read-only nhưng 1 vài folder writable: `app/etc, var, pub/static, pub/media, /tmp`.
	- Update lại toàn bộ code base: 
		- Sửa composer.json: 
			```
				"extra": {
					"magento-force": true
					"magento-deploystrategy": "copy"
				}
			```
		- Remove git cache và add lại -> push -> deploy lại.

| File                      | Description                                                                                                                                                                                                                                                                  |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/.magento/routes.yaml`   | Configuration file that redirects `www` to the apex domain and `php` application to serve HTTP. See [Configure routes](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/routes/routes-yaml).                                           |
| `/.magento/services.yaml` | A configuration file that defines a MySQL instance (MariaDB), Redis, and OpenSearch or Elasticsearch. See [Configure services](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/service/services-yaml).                                |
| `/app`                    | The `code` folder is used for custom modules. The `design` folder is used for [custom themes](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/custom-theme). The `etc` folder contains configuration files for the application. |
| `/m2-hotfixes`            | Used for custom patches.                                                                                                                                                                                                                                                     |
| `/update`                 | A service folder used by the support module.                                                                                                                                                                                                                                 |
| `.gitignore`              | Specify which files and directories to ignore. See [`.gitignore` reference](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/file-structure#ignoring-files).                                                                             |
| `.magento.app.yaml`       | A configuration file that defines the properties to build your application. See [Configure application](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/configure-app-yaml).                                                      |
| `.magento.env.yaml`       | Configuration file for the build, deploy, and post-deploy phases. The `ece-tools` package includes a sample of this file. See [Configure environments](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/configure-env-yaml).       |
| `composer.json`           | Fetches Adobe Commerce and the configuration scripts to prepare your application. See [Required packages](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/overview).                                                                    |
| `composer.lock`           | Stores version dependencies for every package. See [Required packages](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/overview).                                                                                                       |
| `magento-vars.php`        | Used to define [multiple stores](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/multiple-sites) and sites using variables.                                                                                                     |
- 
#### 2. Developer tool
##### 2.1 Cloud CLI
- Cần cài `magento-cloud` CLI
- Command: 
	- `magento-cloud login`	
	- `magento-cloud list`	
	- `magento-cloud ssh	
	- `magento-cloud web` : open Cloud Console web version.
	- `magento-cloud environment:list`		
	- `magento-cloud environment:redeploy <environment-name>`	
	- `magento-cloud environment:branch <new-name> <parent-branch> `: Tạo branch mới và gắn với 1 môi trường. Push 1 empty commit để trigger deploy môi trường đó.
- Manage user: 
	- `magento-cloud user:<command>`
- Secure connection:
	- `magento-cloud login` and `magento-cloud ssh-key:add ~/.ssh/id_rsa.pub`.
	- SSH by `ssh` command or use cloud CLI `magento-cloud ssh -p <project-ID> -e <environment-ID>`.
	- `magento-cloud tunnel:<command>` -> set up tunnel để ssh nhanh hơn (kiểu như config ssh).
- Backup:
	- Snapshot: `magento-cloud snapshot:create --live` (--live means avoid downtime).
- Disk:
	- `magento-cloud db:size`
	- `magento-cloud mount:size`
	- `.magento.app.yaml` manages total disk, `.magento/services.yaml` manages disk for each service.
	- 
##### 2.2 ECE tool
- By default, these `ece-tools` commands are in the [hooks property](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/app/properties/hooks-property) of the `.magento.app.yaml` configuration file.
- `php .vendor/bin/ece-tools config:dump` chỉ dump các config khác với default. `php bin/magento app:config:dump` dump hết config -> nên dùng ece-tools.
- Thứ tự apply patch: 
	- Apply all required Commerce patches included in the Cloud Patches for Commerce package.
	- Apply selected optional Commerce patches included in the Quality Patches Tool.
	- Apply custom patches in the `/m2-hotfixes` directory in alphabetical order by patch name.
#### 3. Config
##### 3.1 Application: .magento.app.yaml
- Define build, hook, cron, db, php, disk
- Xác định những ứng dụng sẽ cài lên server
##### 3.2 Environment: .magento.env.yaml
- Focus on environment config (staging, production...)
##### 3.3 Routes: .magento/routes.yaml
- Config url, upstream, redirect, cache.
##### 3.4 Service:	.magento/services.yaml
- Config service: MariaDB, PHP extensions, Redis, RabbitMQ, and Elasticsearch/Opensearch
- Check service running: 
	-  Ở local: `magento-cloud relationships`
	- Ở remote server: `php ./vendor/bin/ece-tools env:config:show services` hoặc `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp`
- Xác định tên của các loại service (name) sẽ chạy với ứng dụng nào (trong file `.magento.app.yaml`).

#### 4. Cloud console
Page 1: Login -> thấy all project -> Vào 1 project

Page 2: Project overview:
- Project name
- Region, Project ID
- Plan, allotted storage, environments, users
- Storefront URL with **Set a custom domain** button

Page 3: Environment overview
- Environment name, type
- Region, Project ID
- Date and time of last activity, including backup. Vào backup tab để xem list backup và backup button.
- HTTP access and search engine status
- Machine name assigned to environment
- Environment status (Active or Inactive)
- Storefront URL with **Set a custom domain** button

Page 4: Project setting menu

| Option       | Description                                                                                                                                                                                                                                                                                                |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| General      | Manage the timezone for use with scheduling backups or maintenance.                                                                                                                                                                                                                                        |
| Access       | Manage [user access](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/user-access) to project and environment types.                                                                                                                                                   |
| Certificates | View a list of the SSL certificates associated with the project.                                                                                                                                                                                                                                           |
| Deploy Key   | Add and view the public key to the project code repository.                                                                                                                                                                                                                                                |
| Domains      | Add a domain name to the project. See [Manage domains](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration).                                                                                                                   |
| Integrations | Add and manage [integrations](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/dev-tools/integrations/overview), such as health notifications and webhooks.                                                                                                                    |
| Variables    | Add [project-level variables](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/variable-levels) that are available at build and runtime in all environments. Ngoài ra có thể set variable bằng cloud cli. Show variables bằng command `magento-cloud variables`. |

Page 5: Environment setting menu

| Option    | Description                                                                                                                                                                                            |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| General   | Configure display name, environment type, and parent environment.  <br>Toggle different environment settings:                                                                                          |
|           | **Enable outgoing emails**: Send [outgoing emails](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/outgoing-emails) from the environment using the SMTP protocol. |
|           | **Hide from search engines**: Block search engine indexers and crawlers from the site.                                                                                                                 |
|           | **HTTP access control**: Enable security configuration for the Cloud Console using a login and IP address access control.                                                                              |
|           | Status is `active` or `inactive`. Most of your work is in an active environment. You can deactivate or delete the environment.                                                                         |
| Variables | View, create, and manage [environment-level variables](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/variable-levels) available at runtime.               |
| Domains   | View a list of [configured routes](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/routes/routes-yaml).                                                         |
