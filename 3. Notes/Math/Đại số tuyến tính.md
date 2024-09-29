
# 1 Phép toán với Ma trận 
## 1.1 Chuyển vị và chuyển vị liên hợp (Hermitian):
- Chuyển vị:
	- Cho $A \in R^{m \times n}$, $B \in R^{m \times n }$ là chuyển vị của $A$ nếu $b_{ij} = a_{ji}$. Tức $B$ là ma trận nhận được qua phép ánh xạ gương qua đường chéo của ma trận $A$ (đổi hàng thành cột, cột thành hàng).
	- Chuyển vị của ma trận $A$ là $A^T$. 
	- Nếu $A=A^T$ thì $A$ là ma trận đối xứng.
- Chuyển vị liên hợp:
	- Là chuyển vị + lấy liên hợp phức của phần tử ma trận. Liên hợp phức của $a + bi$ là $a-bi$.
	- Chuyển vị liên hợp của $A$ là $A^H$.
	-  Nếu $A=A^H$ thì $A$ là $Hermitian$.
## 1.2 Phép [[Nhân ma trận]]
- $A \in R^{m \times n}, B \in R^{n \times p} \rightarrow C=AB \in R^{m \times p}$
- Vector hàng của ma trận này nhân vector cột của ma trận kia.
- Một số tính chất:
	- Số cột của ma trận thứ nhất = số hàng của ma trận thứ 2.
	- Không có tính giao hoán.
	- Có tính kết hợp: $ABC=(AB)C=A(BC)$
	- Có tính phân phối với phép cộng: $A(B+C) = AB + AC$
	- Chuyển vị của tích: $(AB)^T = B^TA^T, (AB)^H=B^HA^H$
		- Tích vô hướng của 2 vector $x,y$: $x^Ty = y^Tx = \sum^{n}_{i=1} x_iy_i$.
		- Chú ý: $x^Hy = y^Hx \leftrightarrow x^Hy = y^Hx \in R$.
		- Tích vô hướng của 2 vector = 0 (nếu cả 2 vector khác 0) thì chúng vuông góc với nhau.
- Tích Hadamard của 2 ma trận cùng kích thước: $\begin{split}\mathbf{A} \odot \mathbf{B} = \begin{bmatrix} a_{11} b_{11} & a_{12} b_{12} & \dots & a_{1n} b_{1n} \\ a_{21} b_{21} & a_{22} b_{22} & \dots & a_{2n} b_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} b_{m1} & a_{m2} b_{m2} & \dots & a_{mn} b_{mn} \end{bmatrix}.\end{split}$
## 1.3 Một số ma trận đặc biệt
- **Ma trận đơn vị bậc n**: $I_{n} = \begin{bmatrix} 1 & 0 & 0 & ... & 0 \\ 0 & 1 & 0 & ... & 0 \\  0 & 0 & 1 & ... & 0 \\  ... & ... & ... & ... & ...\\ 0 & 0 & 0 & ... & 1 \end{bmatrix}$
	- Tính chất: $IA = A, IB = B, Ix = x$
- **Ma trận khả nghịch:**
	- Nếu $AA^{-1} = I$ và $A$ là ma trận vuông thì $A$ là ma trận khả nghịch, $A^{-1}$ là ma trận nghịch đảo của $A$.
	- $AA^{-1} = A^{-1}A = I$.
	- Nếu $A$ khả nghịch: $(A^T)^{-1} = (A^{-1})^T$.
	- Nếu $A$ khả nghịch và $Ax = b$:  $x = A^{-1}b$.
	- Nếu $A, B$ khả nghịch: $(AB)^{-1} = B^{-1}A^{-1}$.
- **Ma trận đường chéo:** là ma trận có tất cả các phần tử không nằm trên đường chéo chính đều bằng 0.
- **Ma trận tam giác trên/dưới:**
	- Là ma trận vuông có các phần tử nằm dưới/trên đường chéo chính đều bằng 0.
	- *Back substitution & forward substitution*: dùng để giải hệ phương trình nếu chứa ma trận tam giác trên/dưới.
## 1.4 Định thức
- Tính định thức bằng quy nạp: $$A \in R^{m \times n} \Rightarrow \det(A) = \sum^{n}_{j=1}(-1)^{i+j}a_{ij}\det(A_{ij})$$với $i$ bất kì, $1<= i <= m$, $A_{ij}$ là phần bù đại số của $A$ ứng với phần tử hàng $i$, cột $j$.
- Tính chất:
	- $\det(A) = \det(A^T)$.
	- $\det(A) = a_1a_{2}a_{3}\dots a_{n}$ nếu $A$ là ma trận đường chéo vuông.
	- $\det(I) = 1$.
	- $\det(AB)=\det(A)\det(B)$ nếu $A, B$ vuông và cùng số chiều.
	- Nếu $A$ có 1 hàng hoặc cột toàn 0 thì $\det(A)=0$.
	- $\det(A) \neq 0 \Leftrightarrow A$ khả nghịch.
	- $\det(A^{-1}) = \frac{1}{\det{(A)}}$.
# 2 Tổ hợp tuyến tính và không gian vector
## 2.1 Tổ hợp tuyến tính
### 2.1.1 Định nghĩa
- $\boldsymbol{b} = A \boldsymbol{x}$  thì $\boldsymbol{b}$ là tổ hợp tuyến tính các cột của $A$.
- Tập hợp tất cả $\boldsymbol{b}$ là không gian sinh các cột của $A$ (thường gọi là $span$ hoặc $span \space space$). Kí hiệu là $span(\boldsymbol{a_{1},...,a_{n}})$ ($A = [\boldsymbol{a_{1},...,a_{n}}]$).
- $\{\boldsymbol{a_{1}},\dots,\boldsymbol{a_{n}}\}$ và $\boldsymbol{0} = A \boldsymbol{x}$ thì hệ độc lập tuyến tính (*linear independence*) khi có nghiệm $\boldsymbol{x} = \boldsymbol{0}$ duy nhất thỏa mãn. Ngược lại, nếu  $\exists  \boldsymbol{x} \neq \boldsymbol{0}$ thỏa mãn thì là hệ phụ thuộc tuyến tính (*linear dependence*).
### 2.1.2 Tính chất
- Một hệ là phụ thuộc tuyến tính nếu và chỉ nếu tồn tại một vector trong hệ đó là tổ hợp tuyến tính của các vector còn lại.
- Hệ con của hệ độc lập tuyến tính là 1 hệ độc lập tuyến tính.
- Nếu $A$ khả nghịch, tập hợp các cột của $A$ là một hệ độc lập tuyến tính.
- Nếu số hàng > số cột của $A$, thì tồn tại $\boldsymbol{b}$ sao cho $A\boldsymbol{x} = \boldsymbol{b}$.
- Hệ vector cơ sở $\alpha$ của không gian n chiều $V \in R^n$ khi và chỉ khi:
	- $V = span(\alpha)$
	- $\alpha$ là hệ độc lập tuyến tính
## 2.2 Hạng
## 2.3 Đổi cơ sở
## 2.4 Trị riêng
## 2.5 Chuẩn
## 2.6 Vết





