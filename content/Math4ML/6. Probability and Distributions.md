Phần này của bro Cao Anh Đức viết.

Tham khảo:

- [VNU-UET's Lectures](https://drive.google.com/drive/folders/12_z5yqb1-6R3Z9fFnV4O25MGLabTstZz?usp=sharing)
- [Math for CS](https://courses.csail.mit.edu/6.042/spring18/mcs.pdf)
- [Math for ML](https://mml-book.github.io/book/mml-book.pdf)

## Biến ngẫu nhiên rời rạc và liên tục

### Kiến thức cơ bản

![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/img/yank-note-picgo-img-20260204221802.png)

Các hàm PDF, CDF của biến ngẫu nhiên $X$ được ký hiệu là $f_X(x)$ và $F_X(x)$.
Đặc trưng của biến ngẫu nhiên rời rạc là _PMF_, còn liên tục là _PDF_. Đặc điểm chung của 2 loại biến ngẫu nhiên này là đều có hàm phân bố tích lũy **CDF** (Cumulative distribution function).
Trên thực tế, người ta hay sử dụng CDF để xử lý các bài toán liên quan tới xấp xỉ phân phối vv,... hơn là PMF hay PDF vì tính tổng quát của nó. (Trích lời thầy Đỗ Thái Dương)
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/img/yank-note-picgo-img-20260204221824.png)

### Phân bố liên hợp nhiều biến (joint probability)

Xác suất để xảy ra cả 2 sự kiện $X = x_i$ và $Y = y_j$ được mô tả bằng công thức:

$$
P(X = x_i, Y = y_j) = \frac{n_{ij}}{N}
$$

Trong đó, $N$ là tổng số sự kiện xảy ra và $n_{ij}$ là số lần xảy ra sự kiện $X = x_i$ và $Y = y_j$.
Phân bố liên hợp tuân thủ các tính chất của phân bố 1 biến, ví dụ như $\sum_{}P(X = x_i, Y = y_j) = 1$.

**Ví dụ**
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/img/yank-note-picgo-img-20260204221842.png)

Xác suất để $W = 1$ và $T = 2$ là $P(W = 1, T = 2) = 0.03$.
Ta cũng có thể giảm số chiều để tính $P(X = x_i)$ bằng cách lấy tổng tất cả các chiều còn lại mà có giá trị $X = x_i$.
Xác suất để $W = 1$ là $P(W = 1) = \sum_{i = 0}^{3}P(W = 1, T = t_i)$

## Bayes

$$
p(x|y) = \frac{p(y|x)p(x)}{p(y)}
$$

Trong đó

- $p(x|y)$: Hậu nghiệm (posterior) là tri thức có được sau khi nạp data từ $y$.
- $p(y|x)$: likelihood là xác suất của data $y$ nếu giả sử ta biết trước biến $x$.
- $p(x)$: tiên nghiệm (prior) là tri thức ban đầu khi chưa có bất kỳ data nào.
- $p(y)$: evidence

## Kỳ vọng và phương sai

### Kỳ vọng

Kỳ vọng của biến ngẫu nhiên $X$ được cho bởi công thức

$$
E[X] = \sum_{x}x_i\cdot p(x_i)
$$

(rời rạc)

$$
E[X] = \int_{X}x\cdot p(x)dx
$$

(liên tục)

Ta có thể coi biến ngẫu nhiên đa chiều $X$ là vector hữu hạn các biến ngẫu nhiên đơn chiều $[X_1, ..., X_n]^{\top},$ khi đó:

$$
E[X] =
\begin{equation*}
\begin{bmatrix}
E[X_1] \\
\vdots \\
E[X_n]
\end{bmatrix}
\end{equation*}
\in \mathbb{R}^D
$$

### variance, covariance, correlation

Tham khảo tài liệu ở đầu chương (sách MIT).

## Biến ngẫu nhiên trong không gian vector

Tham khảo concept: [MAT1101](https://www.overleaf.com/read/ywzztjqzxbfq#319264)

## Phân phối chuẩn Gauss

### Đơn biến

$$
p(x; \mu, \sigma^2) \frac{1}{\sqrt{2\pi} \sigma} exp \left(-\frac{1}{2\sigma^2} (x - \mu^2) \right)
$$

### Đa biến

Vector $[X_1, ... X_n]^{\top}$ được gọi là có phân phối Gauss đa biến với $\mu \in \mathbb{R}^n$ và ma trận covariance $\sum_{} \in \mathbb{S}_{++}^{n}$ nếu CDF của nó được xác định bởi công thức

$$
p \left(x; \mu, \sum \right) = \frac{1}{(2\pi)^{\frac{1}{2}}|\sum|^{\frac{1}{2}}} exp \left( - \frac{1}{2}(x-\mu)^{\top} {\sum}^{-1} (x - \mu)\right)
$$

Trong đó $x \in \mathbb{R}^D$. Ta viết $p(x) = \mathcal{N}(x|\mu, \sum)$ hay $x \sim \mathcal{N}(\mu, \sum)$.
Với $\mu = 0, \sum = I$ thì ta gọi đó là phân phối chuẩn tắc.

### Phân phối biên và phân phối có điều kiện Gauss là một phân phối Gauss

Cho $X$ và $Y$ là 2 biến ngẫu nhiên đa biến có thể có số chiều khác nhau. Ta có

$$
p(x, y) = \mathcal{N}
    \left(
        \begin{bmatrix}
            \mu_x \\
            \mu_y
        \end{bmatrix}
        ,
        \begin{bmatrix}
        \sum_{xx} && \sum_{xy} \\
        \sum_{yx} && \sum_{yy} \\
        \end{bmatrix}
    \right)
$$

Trong đó $\sum_{xx} = Cov[x, x], \sum_{yy} = Cov[y, y]$ là ma trận marginal-covariance của $x$ và $y$, và $\sum_{xy} = Cov[x, y]$ là ma trận cross-covariance giữa $x$ và $y$
Phân phối có điều kiện $p(x | y)$ được cho bởi công thức:

$$
p(x|y) = \mathcal{N}(\mu_{x|y}, {\sum}_{x|y}) \\
\mu_{x|y} = \mu_x + {\sum}_{xy}{\sum}_{yy}^{-1}(y - \mu_y) \\
{\sum}_{x|y} = {\sum}_{xx} - {\sum}_{xy}{\sum}_{yy}^{-1}{\sum}_{yx}
$$

Phân phối biên $p(x)$ của joint Gaussian distribution $p(x, y)$ cũng là một Gaussian distribution, đuọc cho bởi công thức:

$$
p(x) = \int p(x, y)dy = \mathcal{N} \left(x|\mu_x, {\sum}_{xx} \right)
$$

Ví dụ về biến ngẫu nhiêu 2 biến
[p.206]

### Các bài toán liên hệ phân phối Gauss có điều kiện

- The Kalman filter (signal processing)
- Gaussians processes
- Latent linear Gaussian models (analysis PPCA)

### Tích của mật độ Gauss

Với những bài toán hồi quy tuyến tính (linear regression), ta cần tính hàm likelihood Gauss, và có liên quan tới tích của chúng.
Tích của 2 phân phối Gauss $\mathcal{N}(x | a, A)\mathcal{N}(x | b, B)$ là một phân phối Gauss scaled bởi hằng số $c \in \mathbb{R}$, được cho bởi $c\mathcal{N}(x | c, C)$, với

- $C = (A^{-1} + B^{-1})^{-1}$
- $c = C(A^{-1}a + B^{-1}b)$
- $c = (2\pi)^{-\frac{D}{2}}|A + B|^{-\frac{1}{2}}
    \exp(
        -\frac{1}{2}(a - b)^{\top}(A + B)^{-1}(a - b)
    )$

Hằng số $c$ có thể được viết theo cách khác dưới dạng hàm mật độ Gauss với một ma trận covariance $A + B$. Vd: $c = \mathcal{N}(a|b, A + B) = \mathcal{N}(b|a, A + B)$, và cách viết này thường được sử dụng hơn.

### Sum & linear Transformations

Nếu $X, Y$ là 2 biến ngẫu nhiên Gauss thì $aX + bY$ cũng là biến ngẫu nhiên Gauss thỏa mãn

$$
    p(ax + by) = \mathcal{N} \left(a\mu_x + a\mu_y, a^2{\sum}_x + b^2{\sum}_y \right)
$$

Định lý: cho một hàm hỗn hợp của 2 hàm mật độ Gauss có dạng

$$
p(x) = \alpha p_1(x) + (1 - \alpha)p_2(x)
$$

thì Variance được tính bằng công thức

$$
    \mathbb{V}[x] = \left[\alpha \sigma_1^2 + (1 - \alpha)\sigma_2^2\right] + \left([\alpha\mu_1^2 + (1 - \alpha)\mu_2^2] - [\alpha \mu_1 + (1 - \alpha)\mu_2]^2 \right)
$$

Một số tính chất (đặt $y = Ax$):

- $\mathbb{V}_x[x] = \mathbb{E}_Y[\mathbb{V}_x[x|y]] + \mathbb{V}_Y[\mathbb{E}_X[x|y]]$ (định lý phương sai toàn phần)
- $\mathbb{V}[y] = \mathbb{V}[Ax] = A\mathbb{V}[x]A^{\top} = A\sum A^{\top}$
  $\Leftrightarrow p(y) = \mathcal{N} \left(y|A\mu, A\sum A^{\top} \right)$

Giả sử ta có bài toán ngược, cho $y = Ax$ và $p(y) = \mathcal{N} \left(y|Ax, \sum \right)$, tìm $p(x)$?
Giải: ta có $y = Ax \Leftrightarrow (A^{\top}A)^{-1}A^{\top}y = x$.
Vì $x$ là một ánh xạ tuyến tính của $y$ nên

$$
    p(x) = \mathcal{N} \left( x | (A^{\top}A)^{-1}A^{\top}y, (A^{\top}A)^{-1}\sum A(A^{\top}A)^{-1} \right)
$$

## Conjugacy and the Exponential Family

### Định nghĩa

Một tiên nghiệm (prior) được gọi là conjugate cho hàm hợp lý (likelihood) nếu hậu nghiệm (posterior) cùng form dạng với tiên nghiệm.
Ví dụ: bài toán tung đồng xu
Cho biến ngẫu nhiên nhị thức là số lần ra mặt ngửa trong $N$ lần tung đồng xu, có phân phối $X \sim B(N, \mu)$:

$$
p(x | N, \mu) =  {N \choose x} \mu_x(1 - \mu)^{N - x}, x = 0, 1, ..., N,
$$

Ta sử dụng một hàm tiên nghiệm Beta với tham số $\mu$, hay $\mu \sim Beta(\alpha, \beta)$:

$$
    p(\mu | \alpha, \beta) = \frac{\Gamma(\alpha + \beta)}{\Gamma(\alpha) \Gamma(\beta)}\mu^{\alpha - 1}(1 - \mu)^{\beta - 1}
$$

Để ý rằng nếu $x = h$ tức ra $h$ lần mặt ngửa trong $N$ lần tung, ta tính được phân phối hậu nghiệm trên $\mu$ như sau:

$$
\begin{align}
p(\mu | x = h, N, \alpha, \beta) &\propto p(x | N, \mu) p(\mu | \alpha, \beta) \\
&\propto \mu^h(1 - \mu)^{(N - h)}\mu^{\alpha - 1}(1 - \mu)^{\beta - 1} \\
&= \mu^{h + a - 1}(1 - \mu)^{(N - h) + \beta - 1} \\
&= Beta(h + \alpha, B - h + \beta)
\end{align}
$$

| Likelihood  | Conjugate prior          | Posterior                |
| ----------- | ------------------------ | ------------------------ |
| Bernoulli   | Beta                     | Beta                     |
| Binomial    | Beta                     | Beta                     |
| Gaussian    | Gaussian/inverse Gamma   | Gaussian/inverse Gamma   |
| Gaussian    | Gaussian/inverse Wishart | Gaussian/inverse Wishart |
| Multinomial | Dirichlet                | Dirichlet                |

Cho $x \in \{0,1\}$ là biến ngẫu nhiên phân phối Bernoulli với $\theta \in [0,1]$, tức

$$
p(x = 1 \mid \theta) = \theta
$$

Cho $\theta$ được biểu diễn bởi phân phối Beta với tham số $\alpha, \beta$:

$$
p(\theta \mid \alpha, \beta) \propto \theta^{\alpha-1}(1 - \theta)^{\beta-1}
$$

Tương tự ví dụ trên, ta được

$$
\begin{align}
p(\theta \mid x, \alpha, \beta)
&\propto p(x \mid \theta)\, p(\theta \mid \alpha, \beta) \\
&= \theta^{x}(1 - \theta)^{1-x}
  \theta^{\alpha-1}(1 - \theta)^{\beta-1} \\
&= \theta^{\alpha + x - 1}
  (1 - \theta)^{\beta + (1 - x) - 1} \\
&\propto p(\theta \mid \alpha + x, \beta + (1 - x))
\end{align}
$$

Điều này tương đương hàm beta với 2 tham số:

$$
(\alpha + x, \beta + (1 - x))
$$

### Sufficient Statistics

Một thống kê đủ (sufficient statistics) cho tham số $\theta$ là một đại lượng $T(X)$ được tính từ dữ liệu $X$ sao cho: nếu biết $T(x)$ là đủ thì dữ liệu gốc $X$ không cung cấp thông tin nào về $\theta$.
Nói cách khác, $T(x)$ giữ toàn bộ thông tin về $\theta$, và $X$ không giúp hiểu thêm gì về $\theta$.

Định lý Fisher-Neyman: Cho $X$ có hàm mật độ $p(x|\theta)$. Thống kê $\phi(x)$ là đủ cho $\theta$ khi và chỉ khi $p(x|\theta)$ có thể viết dưới dạng

$$
p(x|\theta) = h(x)g_{\theta}(\phi(x))
$$

trong đó $h(x)$ là một phân phối độc lập với $\theta$ và $g_{\theta}$ nắm bắt tất cả sự phụ thuộc vào $\theta$ qua thống kê đầy đủ $\phi(x)$

### Exponential family (họ hàm mũ)

Một họ hàm mũ là họ các phân phối xác suất tham số hóa bởi $\theta \in \mathbb{R}^D$ có dạng

$$
    p(x|\theta) = h(x) exp \left( \langle \theta, \phi(x) \rangle - A(\theta) \right)
$$

trong đó $\phi(x)$ là vector của thống kê đầy đủ.
Một góc nhìn trực quan hơn về họ hàm mũ rằng nó có thể rút gọn lại như sau:

$$
p(x | \theta) \propto \exp(\theta^{\top} \phi(x))
$$

Với dạng tham số hóa trên, $\theta$ được gọi là tham số tự nhiên (natural parameter)

Ví dụ: Cho phân phối Gauss đơn biến $\mathcal{N}\left(\mu, \sigma^2 \right)$. Đặt $\phi(x) = \begin{bmatrix} x \\ x^2 \end{bmatrix}$. Sử dụng định nghĩa của họ hàm mũ ta có:

$$
    p(x | \theta) \propto \exp(\theta_1 x + \theta_2 x^2)
$$

Đặt

$$
    \theta =
    \begin{bmatrix}
        \frac{\mu}{\sigma^2}, -\frac{1}{2\sigma^2}
    \end{bmatrix} ^ {\top}
$$

Thay vào biểu thức ban đầu ta được:

$$
    p(x | \theta) \propto \exp \left( \frac{\mu x}{\sigma^2} - \frac{x^2}{2\sigma^2} \right) \propto \exp \left( -\frac{1}{2\sigma^2}(x - \mu)^2 \right)
$$

Thống kê đủ $\mathcal{N}\left(\mu, \sigma^2 \right)$ và tham số tự nhiên $\theta$ của hàm Gauss trên cho thấy rằng đó là một phân phối thuộc họ hàm mũ.

**Chú ý**: mỗi thành viên của họ hàm mũ đều có một conjugate prior

$$
p({\theta} \mid {\gamma}) = h_c( {\theta}) \exp
\left(
    \left\langle
        \begin{bmatrix}
            \gamma_1 \\ \gamma_2
        \end{bmatrix},
        \begin{bmatrix}
            {\theta} \\ -A({\theta})
        \end{bmatrix}
    \right\rangle
    - A_c(\gamma)
\right)
$$

Với $\gamma = \begin{bmatrix} \gamma_1 \\ \gamma_2 \end{bmatrix}$ có số chiều $\dim(\theta) + 1$.
Thống kê đầy đủ của conjugate prior là $\begin{bmatrix} \theta \\ -A(\theta) \end{bmatrix}$.

## Inverse Transform

Tham khảo thêm bài tập ở chương 4 sách MIT.
Bài toán: Cho phân phối $X_1, X_2, ..., X_n$ thuộc một phân phối được biết nào đó. Hãy tìm phân phối của $Y = f(X_1, X_2, ..., X_n)$?

Cách 1: Tìm hàm CDF của $Y$ rồi lấy đạo hàm của chúng.
B1: Tìm $F_Y(y) = P(Y \leq y)$
B2: Lấy đạo hàm CDF để được hàm PDF: $f_Y(y) = \frac{d}{dy}F_Y(y)$

Định lý: Nếu $X$ là biến ngẫu nhiên có CDF là một hàm đơn điệu nghiêm ngặt thì biến ngẫu nhiên $Y = F_X(X)$ là một phân phối đều.

Cách 2: Đổi biến, từ hàm $Y = F(X)$ ta tìm hàm ngược, tức $X = F^{-1}(Y)$ rồi lấy đạo hàm CDF ra PDF.
Ta có

$$
    F_Y(y) = P(U(X) \leq Y) =  P(X \leq U^{-1}(y)) = \int_{a}^{U^{-1}(y)} f(x) dx
$$

$$
\begin{align}
\Leftrightarrow f(y) = \frac{d}{dy}F_Y(y) &= \frac{d}{dy} \int_{a}^{U^{-1}(y)} f(x) dx \\
&= \frac{d}{dy} \int_{a}^{U^{-1}(y)} f_x \left(U^{-1}(y) \right) U^{-1'}(y) dy \quad \text{(đổi biến)} \\
&= f_x \left(U^{-1}(y) \right) \cdot \left( \frac{d}{dy}U^{-1}(y) \right)
\end{align}
$$

Vì $U$ là hàm tăng ngặt, với trường hợp giảm ngặt thì nó có thêm dấu âm khi đạo hàm tương tự. Do đó thêm dấu giá trị tuyệt đối cho cả 2 trường hợp:

$$
    f(y) = f_x \left(U^{-1}(y) \right) \cdot \left| \frac{d}{dy}U^{-1}(y) \right|
$$

Định lý: với $y$ là vector đa biến, $y = U(x)$, khả vi và khả nghịch với mọi miền của $x$, thì tương ứng với mỗi giá trị của $y$, hàm xác suất mật độ $Y = U(X)$ được cho bởi công thức:

$$
     f(y) = f_x \left(U^{-1}(y) \right) \cdot \left| \det \left( \frac{\partial}{\partial y} U^{-1}(y)\right) \right|
$$

## Further Reading

- (Exponential families): Barndorff-Nielsen (2014)
- Normalizing flows (Jimenez Rezende và Mohamed, 2015)
- Variational inference (Goodfellow et al., 2016).
- Billingsley, 1995; Pollard, 2002 (lý thuyết độ đo)
- MacKay (2003), Bishop (2006), Rasmussen và Williams (2006), Barber (2012), Murphy (2012). (mô hình xác suất)

# Bernoulli & Poisson Processes

## Bernoulli Process

Là một dãy các biến ngẫu nhiên $X_1, X_2, ..., X_n$ mang giá trị $0/1$ với xác suất $p$ (giống kết quả tung đồng xu).
2 tính chất quan trọng của Bernoulli Process là

- Tính độc lập (independence): kết quả của các lần tung là độc lập với nhau.
- Tính không nhớ (memorylessness): giống phân phối mũ, kết quả của lần tung trong quá khứ không ảnh hưởng đến kết quả của lần tung trong tương lai.

### Independence

Với $n$ bất kỳ, một dãy các biến ngẫu nhiên $X_{n + 1}, X_{n + 2},...$ cũng là một Bernoulli Process, và độc lập với $X_1, X_2, ..., X_n$.
Cho $n$ là thời gian đã cho của quá trình, và đặt $\overline{T}$ là thời điểm đầu tiên tung đồng xu ra ngửa sau thời điểm $n$. Khi đó, $\overline{T} - n$ có phân phối hình học với xác suất $p$ (khá hiển nhiên =)) ) và độc lập với các biến ngẫu nhiên $X_1, ..., X_n$

### Interarrival Times

Một biến ngẫu nhiên quan trọng có liên quan tới Bernoulli Process là thời gian của lần thành công thứ $k$, ký hiệu là $Y_k$. Một biến ngẫu nhiên khác có liên quan nữa là khoảng thời gian giữa 2 lần thành công thứ $k$ (interarrival time) ký hiệu là $T_k$, được định nghĩa bởi:

$$
T_1 = Y_1, \quad T_k = Y_k - Y_{k - 1}, \quad k = 2, 3,...
$$

$$
Y_k = T_1 + T_2 + ... + T_k
$$

![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260308011907.png)

Dễ dàng chứng minh được $T_i$ độc lập với nhau và có phân phối hình học.

Có một mô tả khác của Bernoulli Process:

1. Bắt đầu với một dãy các biến ngẫu nhiên $T_1, T_2, ..., T_n$ với tham số $p$, và chúng đại diện cho interarrival times.
2. Ghi nhận lần thử thành công ở các thời điểm $T_1, T_1 + T_2, T_1 + T_2 + T_3, ...$

### Kth arrival time

Như ở trên đã đề cập, ta có

$$
Y_k = T_1 + T_2 + ... + T_k
$$

và các $Y_i$ độc lập với nhau, với cùng tham số $p$.
Kỳ vọng và phương sai của $Y_k$ được cho bởi công thức:

$$
    E[Y_k] = E[T_1] + E[T_2] + ... + E[T_k] = \frac{k}{p}
$$

$$
    var(Y_k) = var(T_1) + ...  var(T_k) = \frac{k(1 - p)}{p^2}
$$

hàm PMF của $Y_k$:

$$
    p_{Y_k} = {t - 1 \choose k - 1} p^k (1 - p)^{t - k},\quad t = k, k + 1,...
$$

còn được gọi là Pascal PMF of order $k$.

### Splitting & merging process

#### Splitting

![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260308013218.png)
Tách process với xác suất $q$ thì nhánh trên (nhánh chọn) là một Bernoulli Process với xác suất $pq$. Ngược lại, nhánh dưới (nhánh bỏ) cũng là một Bernoulli Process với xác suất $p(1 - q)$.

#### Merging

Trong tình huống ngược lại, bắt đầu với 2 Bernoulli Process khác nhau và chúng ta gộp lại thành 1 process duy nhất với xác suất là $p + q - pq$ và nó cũng là một Bernoulli Process.
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260308013640.png)

## Poisson Process

Poisson Process là một dạng liên tục của Bernoulli Process và được áp dụng khi không thể phân chia thời gian một cách rời rạc như Bernoulli Process.
Ta định nghĩa: $P(k, \tau)$ là xác suất có đúng $k$ arrivals trong khoảng thời gian độ dài $\tau$.
Một arrival process được gọi là Poisson Process với tỉ lệ $\lambda$ nếu thỏa mãn các tính chất sau:

- Đồng nhất theo thời gian (Time-homogeneity): Xác suất $P(k, \tau)$ của $k$ arrivals là như nhau với mọi khoảng có độ dài $\tau$.
- Độc lập: Số các arrivals của một khoảng cụ thể độc lập với các khoảng khác theo thời gian.
- Tính chất khoảng nhỏ: xác suất $P(k, \tau)$ thỏa:
  - $P(0, \tau) = 1 - \lambda \tau + o(\tau)$
  - $P(1, \tau) = \lambda \tau + o_1(\tau)$
  - $P(k, \tau) = o_k(\tau), \quad k = 2, 3,...$
    Trong đó $o(\tau)$ và $o_k(\tau)$ là các hàm của $\tau$ thỏa mãn:
    $$
        \lim_{\tau \to 0} \frac{o(\tau)}{\tau} = 0, \quad \lim_{\tau \to 0} \frac{o_k(\tau)}{\tau} = 0
    $$
    Có thể xem tính chất thứ 3 như khai triển Taylor.

### Biến ngẫu nhiên liên quan tới Poisson Process và các tính chất

Poisson Process với tham số $\lambda_{\tau}$: $N_{\tau}$ arrivals trong Poisson Process với tỉ lệ $\lambda$ trên khoảng độ dài $\tau$ có PMF, kỳ vọng và phương sai là:

$$
    p_{N_{\tau}} = P(k, \tau) = e^{-\lambda t} \frac{(\lambda \tau)^k}{k!}, \quad k = 0, 1, ... \\
    E[N_{\tau}] = \lambda \tau, \quad var(N_{\tau}) = \lambda \tau
$$

Phân phối mũ với tham số $\lambda$: thời điểm $T$ đầu tiên đến khi arrival đầu tiên, có PDF, kỳ vọng và phương sai là:

$$
    f_T(t) = \lambda e^{-\lambda t}, \quad t \geq 0
$$

$$
    E[T] = \frac{1}{\lambda}, \quad var(T) = \frac{1}{{\lambda}^2}
$$

Poisson Process cũng có 2 tính chất quan trọng giống Bernoulli Process:

- Với thời gian $t > 0$, lịch sử của các process sau thời điểm $t$ cũng là Poisson Process, và độc lập với mọi process khác tới thời điểm $t$.
  Cho $t$ là thời gian đã cho của quá trình, và đặt $\overline{T}$ là thời điểm xuất hiện arrival đầu tiên sau thời điểm $t$. Khi đó, $\overline{T} - t$ có phân phối mũ với tham số $\lambda$, và độc lập với lịch sử của process tới thời điểm $t$.

Các định nghĩa về $Y_k$ và $T_k$ tương tự như Bernoulli Process với $Y_k$ là hàm phân phối mũ.
Kỳ vọng và phương sai của $Y_k$ được cho bởi công thức:

$$
    E[Y_k] = E[T_1] + E[T_2] + ... + E[T_k] = \frac{k}{\lambda}
$$

$$
    var(Y_k) = var(T_1) + ...  var(T_k) = \frac{k}{{\lambda}^2}
$$

hàm PDF của $Y_k$:

$$
    f_{Y_k}(y) = \frac{\lambda^k y^{k - 1} e^{-\lambda y}}{(k - 1)!}, \quad y \geq 0
$$

còn được gọi là Erlang PDF of order $k$.

## Tính chất của tổng số ngẫu nhiên của các biến ngẫu nhiên

Cho $N, X_1, X_2, ...$ là các biến ngẫu nhiên đôc lập, với $N$ là số nguyên không âm. Đặt $Y = X_1 + ... + X_N$, $Y = 0$ khi $N = 0$.

- Nếu $X_i \sim Ber(p), N \sim Bin(m, q)$ thì $Y \sim Bin(m, pq$
- Nếu $X_i \sim Ber(p), N \sim P(\lambda)$ thì $Y \sim P(\lambda p)$
- Nếu $X_i \sim Geo(p), N \sim Geo(q)$ thì $Y \sim Geo(pq)$
- Nếu $X_i \sim Exp(p), N \sim Exp(\lambda)$ thì $Y \sim Exp(\lambda p)$

**Note:** chương này khá ảo và hay, t chưa viết kỹ lắm =))

# Markov Chain

Các process ở trên có tính không nhớ, thì Markov chain lại có thể dùng các kết quả ở quá khứ để dự đoán tương lai.

# Deviation from the Mean

Đọc chương Central Limit Theorem và từng bước cải tiến từ bất đẳng thức Markov -> bất đẳng thức Chebyshev -> Luật số lớn để tối ưu $n$ cho bài toán bầu cử.

# Random Walk

Bước đi ngẫu nhiên trên tọa độ và cách nó được sử dụng trong công cụ tìm kiếm google để tìm những kết quả liên quan.

## Gambler's Ruin

Bạn bắt đầu với số vốn là $n$ và chơi với một chuỗi các ván cược, mỗi ván 1 dollar:

- Nếu thắng, bạn nhận được $1$ (xác suất $p$)
- Nếu thua, bạn mất $1$ (xác suất $p$)

Mục tiêu là kiếm được $T$. Trò chơi kết thúc khi:

- Vốn chạm mốc $0$
- Ăn được tổng cộng $T$

Xác suất để bạn chiến thắng trước khi phá sản là bao nhiêu?

Gọi $w_n$ là xác suất chiến thắng khi có $n$ trong tay.

$$
w_0 = 0, w_T = 1 \\
w_n = p \cdot w_{n + 1} + q \cdot w_{n - 1} \quad (q = 1 - p)
$$

TH1: Trò chơi công bằng ($p = 1/2$)

Khi này, $w_n = n/T$

TH2: Trò chơi không công bằng (nhà cái có lợi thế $p < 1/2$)

Chứng minh...

$w_n = \frac{r^n - 1}{r^T - 1}$

$$
P(\text{the gambler wins}) =
    \begin{cases}
        \frac{n}{T}, \quad p = \frac{1}{2} \\
        \frac{r^n - 1}{r^T - 1}, \quad p \neq \frac{1}{2}
    \end{cases}
$$

Với $r = \frac{q}{p}$

Khi nhà cái có lợi thế thì $q > p$, do đó $r > 1$. Từ công thức ở TH2 ta có:

$$
    w_n = \frac{r^n - 1}{r^T - 1} = \frac{r^n}{r^T} \cdot \frac{1 - \frac{1}{r^n}}{1 - \frac{1}{r^T}} < \frac{r^n}{r^T} = \left( \frac{1}{r} \right)^{T - n}
$$

Khi nhà cái có nguồn vốn vô hạn thì $w_n \to 0$, bạn sẽ trắng tay.
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260308032345.png)
Ý tưởng của mô hình này giống như việc đứng trên 1 trục số và di chuyển trái phải 1 đơn vị một cách ngẫu nhiên.

## Random Walks on Graphs

Thuật toán PageRank.
Mạng internet có thể dược mô phỏng thành một đồ thị có hướng khổng lồ với mỗi trang web là mỗi đỉnh. Nếu trang $x$ có lên kết trỏ tới trang $y$ thì sẽ là một cạnh có hướng từ $x \to y$.
Khi đang ở trang $x$, người dùng sẽ nhấp vào link đi ra trang đó với xác suất đồng đều và bằng $\frac{1}{outdeg(x)}$.
Nếu quá trình lướt web (random walk) diễn ra liên tục trên đồ thị, xác suất người dùng ở lại trang nhất định sau một thời gian dài phản ánh mức độ quan trọng (thứ hạng) của trang đó.
Tuy nhiên, có những web không chứa liên kết trỏ ra trang web khác, ta thêm một siêu đỉnh (supervertex) và tất cả các trang trỏ đến siêu đỉnh này và có xác suất bằng nhau.
Khi lướt web đủ lâu thì sẽ đạt tới trạng thái phân phối dừng (Stationary Distribution). Ở trạng thái này, số người đến trang X bằng đúng số người từ trang X rời đi. Nhờ vậy, tổng số người có mặt tại trang X sẽ không thay đổi. Khi này:

$$
    Rank(x) = \sum_{\langle y \to x \rangle} \frac{Rank(y)}{outdeg(y)}
$$

Và

$$
    \sum Rank(x) = 1
$$
