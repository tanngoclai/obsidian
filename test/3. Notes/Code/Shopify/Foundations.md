---
Created at: 2024-04-09
Source:
  - https://academy.shopify.com/path/foundations-certification/foundations-shopify-101
tags:
---
## 1/ Shopify User
Gồm 2 user:
- **Merchant**: Người dùng Shopify để bán hàng.
- **Partner**: Người cung cấp giải pháp công nghệ, tư vấn cho người bán liên quan đến Shopify.
#### 1.1 Nhiệm vụ chính của Shopify Partner:
- **Theme**: build, bán theme.
- **Apps**: build, bán app.
- **Stores**: Xây dựng, cài đặt store.
- **Service**: tư vấn, thực hiện giải pháp để phát triển merchant's business.
#### 1.2 Các loại Shopify Partner:
- **Product partner**: Trực tiếp tư vấn, xây dựng giải pháp cho merchant.
- **Foundational Partner**: Cung cấp các công nghệ để xây dựng các function cơ bản của Shopify (Stripe, Facebook, các bên xây dựng apps/themes...) -> Thường khi nói "Shopify Partner" sẽ **không** ám chỉ các partner này. 
- **Growth Partner:** Giúp phát triển, tiếp thị Shopify đến nhiều người dùng mới. 
## 2/ Shopify Apps
- Gồm 2 loại apps:
	- **Public apps:** app được public ở Shopify App Store.
	- **Custom apps:** app dành riêng cho 1 store, không public ở Shopify App Store -> liên hệ Shopify Partner để build custom app.
- Shop app là một sales channel riêng, customer truy cập qua app. Merchant có thể manage Shop app ở Shopify admin. Shop app is built by Shopify.
## 3/ Payment method & Shopify money
- Payment method:
	- **Shopify Payments:** credit card và các phương thức phổ biến (nhiều lắm, được provided by default function).
	- **Shop pay vs Shop Pay Installments:** payment method built-in Shopify. Shop Pay Installments để pay later.
- Shopify money:
	- **Shopify Capital:** giúp merchant xin fund/vay -> tiền chuyển vào ngân hàng của merchant.
	- **Shopify Balance:** để trong tài khoản thì có lãi (% thay đổi theo thời kì).
## 4/ Shopify POS
#### 4.1 [Shopify POS plan](https://help.shopify.com/en/manual/sell-in-person/getting-started/pos-subscription-overview)

| Compare                 | Lite                                                                         | Pro                                                                          |
| ----------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Price                   | Free with all Shopify plan                                                   | Plan price + $89/month per location                                          |
| Install                 | Default on all Shopify plan                                                  |                                                                              |
| Rate 3rd payment method | >= 5% rate cho 3rd card                                                      | >= 0.6%-2% rate cho 3rd card (tùy plan)                                      |
| Số máy POS              | 1 POS                                                                        | Ulimited POS (nhưng +89$/localtion :D)                                       |
| Staff account           | 0                                                                            | 5 or 15, tùy plan                                                            |
| Function                | [Point of Sale Features - Shopify USA](https://www.shopify.com/pos/features) | [Point of Sale Features - Shopify USA](https://www.shopify.com/pos/features) |
| Target merchant         | Merchant không có staff, không cần dùng POS thường xuyên                     | Merchant dùng thường xuyên, có nhiều cửa hàng và staff.                      |
|                         |                                                                              |                                                                              |
- Special feature:
	- Omnichannel selling (pro): local pick-up, local delivery, Buy in-store & ship sau, buy online & pay in-store... (đủ các hình thức bán hàng).
	- Tracking inventory (pro)
	 ...
#### 4.2 Hardware
- Dùng Shopify POS hardware & Integrated Payments (powered by Shopify Payments):
	- Shopify POS hardware là các device đáp ứng [điều kiện](https://help.shopify.com/en/manual/sell-in-person/hardware/getting-started#device) để chạy Shopify app, có thể tự mua hoặc mua của Shopify. Tùy device sẽ có các phương thức giao tiếp/sử dụng khác nhau.
- Dùng 3rd-party hardware, connect với Shopify POS app.
## 5/ Shopify Markets
#### 5.1 Mô tả
- Giúp người bán quản lý multi-store trong 1 admin. Phù hợp với:
	- Merchants use Shopify Payments.
	- Use multiple local currencies & languages dựa trên khu vực.
	- Available ở tất cả Shopify plans.
	- Plans: Market và [[Market Pro]] (more local payment method, tax...).
	![[Pasted image 20240413122920.png]]
#### 5.2 Guide
- Markets quản lí store theo group:
	- Primary market: quốc gia/khu vực mặc định, được lấy làm default settings.
	- Other markets: các quốc gia/khu vực khác, không phải default. Các quốc gia/khu vực thuộc cùng 1 **group** sẽ có chung tên miền/language/price..., nói chung là setting giống nhau.
	- Các quốc gia không muốn bán: ở những nơi này sẽ không mua hàng được.
- Các setting config ở markets group:
	- Price, nếu dùng Shopify payments thì price sẽ được automatically convert, hoặc merchant có thể tự config.
	- Languages (include static content).
	- Payment methods: tùy chỉnh enable payment method, nhưng chỉ store dùng Shopify Payments là primary gateway mới thanh toán bằng nội tệ được.
	- Domains.
	- Thuế **(Advanced and Plus plans only)**.
- Suggested app:
	- Geolocation.
	- Translate & Adapt app.
#### 5.3 [Shopify Markets Pro](https://academy.shopify.com/path/foundations-certification/foundations-introduction-to-cross-border-selling/1529339/scorm/2ojhuhefbclfv)
- Ưu điểm lớn so với Shopify Market là Shopify Market Pro giúp nhanh chóng mở rộng store mà không cần lo lắng pháp nhân quốc tế, các vấn đề liên quan đến chính phủ sẽ do Shopify lo, merchant chỉ cần mở store và bán hàng.
## 6/ Multiple stores
- Mỗi store/khu vực sẽ cần setup 1 admin store khác nhau, hoạt động như các store riêng biệt (additional stores / expansion stores).
	- Ưu điểm: customize nhiều hơn.
	- Nhược điểm: không đồng bộ được setting, product, catalog... giữa các store.
- Shopify plus có 9 free additional store.
-> Bình thường thì không cần multiple stores.
## 7/ Shopify Plus
- **Shopify Plus Partner Program:** Partner gạ được khách mới dùng Plus thì hưởng 20% revenue subscribes/month của Merchant đó.
- **Shopify Plus Certified App Program:** mấy ông làm apps cho Shopify Plus.

## 8/ Development
- Apps: Gồm Backend & Frontend
- Theme
- Custom storefronts (Cannot customize 3rd-party apps)
#### 8.1 Tools
- **Development stores:** Free, có giới hạn tính năng, có thể truy cập sớm 1 số tính năng sắp ra mắt, build development store để giới thiệu cho khách...
- **Collaborator accounts:** Merchant tạo account và cấp quyền phù hợp cho partner để truy cập vào store của merchants. Collab account được tạo unlimited.
#### 8.2 Make money ([Shopify Partner earnings](https://help.shopify.com/en/partners/how-to-earn))
- Bán apps: nhận 80%; trường hợp đăng kí mới nhận 100% cho 1m$ đầu tiên, sau đó là 85%.
- Bán themes: Tương tự bán apps.
- Giới thiệu merchant: 
	- Giới thiệu khách qua development store: 20% monthly subscription fee (trừ Starter plan thì không được gì).
	- Giới thiệu khách mới (chỉ Shopify Plus): 20% monthly subscription fee (Plus Certified App Partners and Shopify Plus Integration Partners không được tham gia chương trình này).
#### 8.3 Apps
- Shopify App Bridge
- App types:
	- Public apps
	- Custom apps
	- Draft apps
	- 



