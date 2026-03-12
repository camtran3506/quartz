# Problem Formulation

Vì xuất hiện nhiễu (noise) từ những dữ liệu thực tế trong quá trình quan sát, bài toán hồi quy thường được tiếp cận theo hướng xác suất. Trong cách tiếp cận này, nhiễu được mô hình hóa một cách rõ ràng thông qua hàm likelihood.

## Mối quan hệ hàm số và nhiễu

Mối quan hệ giữa các đầu vào $x \in \mathbb{R}^D$ và các giá trị hàm chứa nhiễu (hay target) $y \in \mathbb{R}$ được biểu diễn bằng phương trình:

$$
    y = f(x) + \epsilon
$$

trong đó

- $f(x)$ là hàm thực tế chưa biết mà ta đang cố gắng suy diễn.
- $\epsilon \sim \mathcal{N}(0, \sigma^2)$ là nhiễu đo lường Gauss có phân phối đồng nhất và độc lập.

Từ đó, ta có hàm likelihood biểu diễn xác suất của $y$ khi biết $x$:

$$
    p(y | x) = \mathcal{N}(y | f(x), \sigma^2)
$$

## Mô hình tham số và hồi quy tuyến tính

Ta cần chọn bộ tham số $\theta$ tốt để mô hình hóa dữ liệu. Giả định $\sigma^2$ đã biết trước, ta chỉ cần tập trung vào việc học tham số $\theta$.

Trong bài toán hồi quy tuyến tính, ta xét trường hợp đặc biệt khi các tham số $\theta$ xuất hiện một cách tuyến tính trong mô hình. Phương trình hồi quy tuyến tính được định nghĩa như sau:

$$
    p(y | x, \theta) = \mathcal{N}(y | x^{\top}\theta, \sigma^2) \Leftrightarrow y = x^{\top}\theta + \epsilon
$$

- Trong mô hình này, $\theta \in \mathbb{R}^D$ là các tham số chúng ta cần tìm.
- Hàm likelihood chính là hàm PDF của $y$ được đánh giá tại $x^{\top}\theta$.

**Lưu ý:** Nguồn gốc duy nhất gây ra sự không chắc chắn trong mô hình này chính là nhiễu quan sát $\epsilon$. Nếu không có $\epsilon$ thì mối quan hệ giữa $x$ và $y$ sẽ là tất định và hàm likelihood sẽ thu gọn lại thành một hàm delta Dirac (hàm có giá trị bằng 0 ở mọi nơi ngoại trừ 1 điểm, và có tích phân bằng 1).
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260312002316.png)

# Parameter Estimation

## MLE

Cách tiếp cận phổ biến để tìm $\theta_{MLE}$ là tìm cực đại của hàm likelihood, hay nói cách khác là tìm tham số sao cho phân phối dự đoán của mô hình khớp nhất với dữ liệu huấn luyện:

$$
    \theta_{MLE} \in \underset{\theta}{\text{argmax}}p(\mathcal{Y} | \mathcal{X}, \theta)
$$

Thay vì cực đại hóa hàm khả năng, ta thường cực tiểu hóa đối logarit âm của hàm khả năng (negative log-likelihood hay error function). Việc này giúp tránh lỗi tràn số dưới (numerical underflow) khi nhân nhiều xác suất nhỏ với nhau và biến phép nhân thành phép cộng giúp đạo hàm dễ dàng hơn:

$$
    -\log p(\mathcal{Y} | \mathcal{X}, \theta) = -\log \prod_{n = 1}^{N} p(y_n | x_n, \theta) = -\sum_{n = 1}^{N} \log p(y_n | x_n, \theta)
$$

Đối với mô hình hồi quy tuyến tính chứa nhiễu Gauss, việc cực tiểu hóa logarit âm của hàm khả năng tương đương với việc giải bài toán bình phương tối thiểu (least-squares problem). Ta đạo hàm theo $\theta$ và thu được nghiệm:

$$
    \theta_{MLE} = (X^{\top}X)^{-1}X^{\top}y
$$

Trong đó, $X = [x_1,...,x_n]^{\top} \in \mathbb{R}^{N \times D}$ là design matrix chứa các vector đầu vào $x_n$, và $y = [y_1,...,y_n] \in \mathbb{R}^N$ là vector chứa các label $y_n$.

Mô hình hồi quy tuyến tính không bị giới hạn ở các đường thẳng. Ta có thể áp dụng một phép biến đổi phi tuyến $\phi(.)$ lên đầu vào để đưa nó lên một không gian đặc trưng (feature space) cao chiều hơn (ví dụ: biến đổi x thành các đa thức $1, x, x^2,...$). Khi đó ma trận $X$ được thay thế bằng ma trận đặc trưng $\Phi$. Nghiệm trở thành:

$$
    \theta_{MLE} = (\Phi^{\top} \Phi)^{-1} \Phi^{\top}y
$$

**Lưu ý:** Cả hai nghiệm trên đều yêu cầu ma trận $X^{\top}X$ hoặc $\Phi^{\top} \Phi$ phải khả nghịch.

Bằng cách tương tự, ta cũng có thể ước lượng phương sai nhiễu $\sigma^2_{MLE}$. Kết quả cho thấy nó chính là trung bình thực nghiệm của các bình phương khoảng cách giữa giá trị dự đoán và quan sát thực tế.

## Overfitting in Linear Regression

### Thước đo đánh giá sai số

Khi đánh giá chất lượng mô hình, ta có thể dùng sai số toàn phương trung bình (root mean square error - RMSE). Lợi ích của RMSE là nó được chuẩn hóa theo kích thước tập dữ liệu và có cùng đơn vị đo lường với biến mục tiêu $y$ và bỏ qua hằng số phương sai nhiễu $\sigma^2$:

$$
    \sqrt{\frac{1}{N}||y - \Phi \theta||^2} = \sqrt{\frac{1}{N}(y - \phi^{\top}(x_n )\theta)^2}
$$

### Visualizing Overfitting

Hãy tưởng tượng một tập dữ liệu nhỏ gồm $N = 10$ điểm dữ liệu. Nếu ta dùng MLE để khớp các đa thức có bậc $M$ khác nhau vào dữ liệu này, ta sẽ quan sát thấy các hiện tượng sau
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260312005542.png)

- Underfitting ($M = 0, 1$)
- Fitting well ($M = 3, 4$)
- Overfitting ($M = 9$)

### Training Error vs Test Error

Cách định lượng rõ ràng nhất hiện tượng quá khớp là quan sát sự chênh lệch giữa hiệu suất trên tập huấn luyện (training error) và tập kiểm tra (test error - dữ liệu mới hoàn toàn chưa từng thấy).
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260312005758.png)

- Sai số huấn luyện (Đường màu xanh): Khi tăng bậc $M$, sai số huấn luyện không bao giờ tăng
- Sai số kiểm tra (Đường màu cam): Mới đầu khi tăng $M$, sai số kiểm tra giảm xuống vì mô hình bớt tình trạng underfitting và đạt mức tối thiểu ở vùng fit tốt (ví dụ $M = 4$). Tuy nhiên nếu tăng $M$ thì error sẽ tăng vọt một cách khủng khiếp.

Kết luận: Hiện tượng hàm mất mát trên tập huấn luyện gần như bằng $0$ nhưng hàm mất mát trên tập kiểm tra khổng lồ chính là định nghĩa chuẩn xác nhất của Overfitting

## Maximum A Posteriori Estimation (MAP)

Phương pháp MLE dễ dẫn đến overfitting khi lượng dữ liệu mô hình nhỏ nhưng mô hình quá phức tạp.

Để giảm thiểu tình trạng này, ta có thể đặt một phân phối tiền nghiệm (prior distribution) $p(\theta)$ lên các tham số. Phân phối này mã hóa niềm tin ban đầu của chúng ta về việc các giá trị tham số nào là hợp lý (trước khi ta quan sát bất kỳ dữ liệu nào). Ví dụ $p(\theta) = \mathcal{N}(0, 1)$ mã hóa rằng giá trị tham số được kỳ vọng nằm trong khoảng $[-2, 2]$.

Thay vì tìm tham số cực đại hóa likelihood như MLE, MAP tìm bộ tham số cực đại hóa phân phối hậu nghiệm $p(\theta, \mathcal{X}, \mathcal{Y})$:

$$
    p(\theta| \mathcal{X}, \mathcal{Y}) = \frac{p(\mathcal{Y} | \mathcal{X}, \theta)p(\theta)}{p(\mathcal{Y} | \mathcal{X})}
$$

Vì mẫu số không phụ thuộc vào $\theta$ nên thường được viết thành

$$
    p(\theta | \mathcal{X}, \mathcal{Y}) \propto p(\mathcal{Y} | \mathcal{X}, \theta)p(\theta)
$$

Lấy logarit 2 vế, hàm log-posterior trở thành

$$
    \log p(\theta | \mathcal{X}, \mathcal{Y}) = \log p(\mathcal{Y} | \mathcal{X}, \theta) + \log p(\theta) + \text{const}
$$

Điều này cho thấy ước lượng MAP là sự kết hợp (hay thỏa hiệp) giữa dữ liệu thực tế và kiến thức tiền nghiệm.

Để tìm $\theta_{MAP}$, ta tìm

$$
     \theta_{MAP} \in \underset{\theta}{\text{argmin}} \{ -\log p(\mathcal{Y} | \mathcal{X}, \theta) - \log p(\theta) \}
$$

Với $p(\theta) = \mathcal{N}(0, b^2I)$, hàm mục tiêu trở thành

$$
    -\log p(\theta | \mathcal{X}, \mathcal{Y}) = \frac{1}{2\sigma^2}(y - \Phi \theta)^{\top} (y - \Phi \theta) + \frac{1}{2b^2}\theta^{\top}\theta + \text{const}
$$

Lấy đạo hàm theo $\theta$:

$$
    -\frac{d \log p(\theta | \mathcal{X}, \mathcal{Y})}{d \theta} = \frac{1}{\sigma^2}(\theta^{\top}\Phi^{\top}\Phi - y^{\top}\Phi) + \frac{1}{b^2}\theta^{\top}
$$

Đặt gradient này bằng $0^{\top}$ và giải phương trình ta thu được

$$
    \theta_{MAP} = \left( \Phi^{\top} \Phi + \frac{\sigma^2}{b^2}I \right)^{-1} \Phi^{\top}y
$$

$\theta_{MAP}$ khác $\theta_{MLE}$ ở chỗ có thêm hạng tử $\frac{\sigma^2}{b^2}I$ bên trong ma trận cần nghịch đảo. Nó vô cùng quan trọng để đảm bảo rằng ma trận $\left( \Phi^{\top} \Phi + \frac{\sigma^2}{b^2}I \right)$ luôn là ma trận đối xứng và xác định dương chặt (strictly positive definite). Điều này đồng nghĩa với việc ma trận này luôn luôn có thể khả nghịch (tồn tại nghịch đảo), và bài toán luôn có một nghiệm duy nhất.

**Ý nghĩa:** Đại lượng $\frac{\sigma^2}{b^2}$ hoạt động như một regularizer. Nó kìm hãm không cho các tham số $\theta$ bùng nổ quá lớn để tránh tình trạng overfitting vào các điểm nhiễu.
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260312012818.png)

Tuy vậy, phương pháp này vẫn chỉ là ước lượng điểm và không phải là một giải pháp tổng quát hoàn hảo để chống lại overfitting. Để giải quyết triệt để hơn, người ta sử dụng Hồi quy Tuyến tính Bayes.

## MAP Estimation as Regularization

Thay vì sử dụng xác suất và đặt một phân phối tiền nghiệm (prior distribution) lên các tham số như MAP, trong học máy truyền thống, người ta thường chống lại hiện tượng overfitting bằng cách cộng thêm một hạng tử phạt (penalty term) trực tiếp vào hàm mất mát (regularized least squares - RLS):

$$
    L(\theta) = ||y - \Phi \theta||^2_2 + \lambda||\theta||^2_2
$$

Từ hàm log-likelihood của bài toán MAP ta cực tiểu hóa

$$
    \frac{1}{2\sigma^2} ||y - \Phi \theta||^2_2 + \frac{1}{2b^2}||\theta||^2_2
$$

Nhân toàn bộ biểu thức trên với $2\sigma^2$ ta thu được hàm regularized least squares trong đó

$$
    \lambda = \frac{\sigma^2}{b^2}
$$

Cực tiểu hóa hàm mất mát trên cho ra nghiệm

$$
    \theta_{RLS} = (\Phi^{\top} \Phi + \lambda I)^{-1}\Phi^{\top}y
$$

Nghiệm $\theta_{RLS}$ này giống hệt với $\theta_{MAP}$. Trong thống kê, phương pháp sử dụng chuẩn $L_2$ (euclid) để chính quy hóa này còn được gọi là Hồi quy Ridge (Ridge Regression).

Trong thực tế, ta có thể dùng chuẩn $L_p$ (p-norm) cho bất kỳ bộ regularizer. Khi dùng $L_1$ bộ regularizer trở thành $\lambda||\theta||_1 = \lambda \sum |\theta_d|$ và phương pháp này được gọi là **LASSO**.

TLDR: Dù là Ước lượng Hợp lý Cực đại (MLE) hay Ước lượng MAP / Chính quy hóa, cả hai phương pháp đều chỉ sinh ra các ước lượng điểm (point estimates). Điều này có nghĩa là chúng chỉ tìm ra một bộ giá trị $\theta^*$ duy nhất, tối ưu nhất.

# Bayesian Linear Regression

Hồi quy Tuyến tính Bayes đẩy ý tưởng sử dụng phân phối tiền nghiệm của tham số đi xa hơn một bước: Phương pháp này hoàn toàn không cố gắng tính toán hay tìm kiếm một ước lượng điểm nào cho các tham số. Thay vì chốt một giá trị cụ thể, nó tính toán và sử dụng toàn bộ phân phối hậu nghiệm (full posterior distribution) của các tham số khi thực hiện việc dự đoán.

## Model

Trong hồi quy tuyến tính Bayes, ta xem xét model

- prior
  $$
      p(\theta) = \mathcal{N}(m_0, S_0)
  $$
- likelihood
  $$
      p(y | x, \theta) = \mathcal{N}(y | \phi^{\top}(x)\theta, \sigma^2)
  $$

Ta đặt một phân phối Gauss tiền nghiệm lên $\theta$: $p(\theta) = \mathcal{N}(m_0, S_0)$ và điều này biến $\theta$ thành một vector biến ngẫu nhiên, trong đó

- $m_0$ là vector trung bình, đại diện cho giá trị dự kiến ban đầu của $\theta$ trước khi thấy dữ liệu.
- $S_0$ là ma trận hiệp phương sai, biểu diễn mức độ không chắc chắn của chúng ta về niềm tin ban đầu đó.
- $\phi(x)$ là vector đặc trưng thu được sau khi áp dụng phép biến đổi (có thể là phi tuyến) lên đầu vào $x$.
- Đầu ra $y$ được phân phối quanh giá trị dự đoán $\theta^{\top}(x)\theta$ với một phương sai nhiễu đo lường là $\sigma^2$.

Một mô hình xác suất được coi là đầy đủ khi nó mô tả được joint distribution của tất cả các biến ngẫu nhiên trong hệ thống – bao gồm cả biến quan sát được ($y$) và biến chưa quan sát/ẩn ($\theta$)

$$
    p(y, \theta | x) = p(y | x, \theta)p(\theta)
$$

## Prior Predictions

Cách tiếp cận của phương pháp Bayes là tính trung bình trên tất cả các thiết lập tham số khả thi thay vì chỉ chọn ra một bộ tham số duy nhất.

Mục này tập trung vào việc thực hiện dự đoán này chỉ dựa tiền nghiệm mà chưa hề quan sát bất kỳ dữ liệu huấn luyện nào.

Để đưa ra dự đoán $y_*$ tại một điểm dữ liệu kiểm tra (test input) $x_*$, ta sử dụng quy tắc tính tổng xác suất để tích phân (loại bỏ) hoàn toàn tham số $\theta$

$$
    p(y_*|x_*) = \int p(y_*|x_*, \theta)p(\theta)d\theta = \mathbb{E}_{\theta}[p(y_*|x_*, \theta)]
$$

Phương trình này cho thấy kết quả dự đoán là một kỳ vọng của các dự đoán đối với mọi giá trị khả thi của $\theta$.

Bằng cách áp dụng các tính chất của biến đổi affine trên biến ngẫu nhiên Gauss, phân phối dự đoán thu được là

$$
     p(y_*|x_*)= \mathcal{N}(\phi^{\top}(x_*)m_0, \phi^{\top}(x_*)S_0\phi(x_*) + \sigma^2)
$$

Phương sai của phân phối dự đoán này rất quan trọng vì nó tách biệt rõ ràng hai nguồn gốc của sự không chắc chắn (uncertainty):

- $\phi^{\top}(x_*)S_0\phi(x_*)$: ): Thể hiện sự không chắc chắn xuất phát từ chính các tham số $\theta$.
- $\sigma^2$: Thể hiện sự không chắc chắn do nhiễu đo lường (measurement noise) của quá trình quan sát sinh ra.

Đôi khi ta không muốn dự đoán mục tiêu quan sát chứa nhiễu $y_*$ mà chỉ muốn dự đoán $f(x_*) = \phi^{\top}(x_*)\theta$, ta chỉ cần loại bỏ nhiễu ở phương trình trên:

$$
     p(f(x_*))= \mathcal{N}(\phi^{\top}(x_*)m_0, \phi^{\top}(x_*)S_0\phi(x_*))
$$

Phân phối trên các hàm (Distribution over Functions) là một hệ quả trực quan và mạnh mẽ của Hồi quy Tuyến tính Bayes. Thay vì chỉ hình dung xác suất áp dụng cho các con số hoặc vector (như tham số θ), khái niệm này cho phép chúng ta hình dung một không gian mà mỗi "mẫu" (sample) rút ra từ phân phối đó là một hàm số (một đường cong hoặc đường thẳng) hoàn chỉnh (lười viết vì buồn ngủ)... sẽ làm sau

## Posterior Distribution

Thay vì tìm một điểm ước lượng duy nhất, Hồi quy Tuyến tính Bayes sử dụng Định lý Bayes để tính toán toàn bộ phân phối hậu nghiệm (posterior distribution) của tham số $\theta$

$$
    p(\theta | \mathcal{X}, \mathcal{Y}) = \frac{p(\mathcal{Y} | \mathcal{X}, \theta) p(\theta)}{p(\mathcal{Y} | \mathcal{X})}
$$

Hàm likelihood là phân phối Gauss $\mathcal{N}(y | \Phi \theta, \sigma^2 I)$ và tiền nghiệm của là phân phối Gauss $\mathcal{N}(\theta | m_0, S_0)$. Do tính chất liên hợp (conjugacy), phân phối hậu nghiệm thu được cũng sẽ là một phân phối Gauss có dạng dạng đóng (closed form)

$$
    p(\theta | \mathcal{X}, \mathcal{Y})= \mathcal{N}(\theta | m_N, S_N)
$$

với các tham số được cập nhật sau khi quan sát $N$ điểm dữ liệu như sau:

- Hiệp phương sai hậu nghiệm (Posterior covariance): $S_N = (S_{0}^{-1} + \sigma^{-2} \Phi^{\top} \Phi)^{-1}$
- Trung bình hậu nghiệm (Posterior mean): $m_N = S_N(S_{0}^{-1}m_0 + \sigma^{-2}\Phi^{\top}y)$.

Chứng minh: dùng kỹ thuật Completing the Squares (tự đọc thêm ở sách XSTK MIT để biết kiến thức nền hoặc sách này có giải sơ qua).

**Nhận xét:** Một hệ quả toán học trực tiếp có thể thấy từ các công thức trên là trung bình hậu nghiệm $m_N$ hoàn toàn trùng khớp với ước lượng $\theta_{MAP}$. Tuy vậy vẫn có sự khác biệt khi hồi quy tuyến tính Bayes thêm ma trận hiệp phương sai $S_N$ biểu thị sự không chắc chắn của toàn bộ không gian tham số sau khi học từ dữ liệu, cho phép chúng ta không phải đặt cược toàn bộ niềm tin vào một bộ tham số $\theta$ duy nhất.

## Posterior Predictions

Để dự đoán giá trị mục tiêu $y_*$ tại điểm $x_*$ ta lấy tích phân như phần trước:

$$
    p(y_*|\mathcal{X}, \mathcal{Y}, x_*) = \int p(y_*|x_*, \theta)p(\theta |\mathcal{X}, \mathcal{Y})d\theta = \mathbb{E}_{\theta |\mathcal{X}, \mathcal{Y}}[p(y_*|x_*, \theta)]
$$

Và phân phối dự đoán hậu nghiệm trên cũng là một phân phối Gauss dạng đóng:

$$
     p(y_*|\mathcal{X}, \mathcal{Y}, x_*)= \mathcal{N}(y_* | \phi^{\top}(x_*)m_N, \phi^{\top}(x_*)S_N\phi(x_*) + \sigma^2)
$$

Hai đại lượng của phân phối này mang ý nghĩa quan trọng:

- Predictive mean $\phi^{\top}(x_*)m_N$: Đây là giá trị kỳ vọng mà mô hình dự đoán. Giá trị này hoàn toàn trùng khớp với dự đoán nếu ta chỉ sử dụng ước lượng điểm MAP.
- Predictive variance $\phi^{\top}(x_*)S_N\phi(x_*) + \sigma^2$: Đây là điểm tạo nên sức mạnh thực sự của phương pháp Bayes. Độ không chắc chắn của dự đoán là tổng của hai thành phần độc lập
  - $\sigma^2$: : Sự không chắc chắn do nhiễu đo lường nội tại của hệ thống.
  - $\phi^{\top}(x_*)S_N\phi(x_*)$: Sự không chắc chắn xuất phát từ chính các tham số $\theta$. Đặc biệt, thành phần này phụ thuộc trực tiếp vào vị trí của đầu vào kiểm tra $x_*$.

## Computing the Marginal Likelihood

Thay vì chỉ tìm một bộ tham số tốt nhất, Marginal Likelihood đánh giá xem toàn bộ mô hình (cùng với niềm tin tiền nghiệm của chúng ta) giải thích dữ liệu huấn luyện tốt đến mức nào. Đại lượng này tự động tích hợp nguyên lý Occam's razor, giúp trừng phạt các mô hình quá phức tạp và ngăn chặn tình trạng overfitting.
Hàm Marginal Likelihood dùng tích phân để tính để loại bỏ hoàn toàm $\theta$:

$$
\begin{align}
    p(\mathcal{Y} | \mathcal{X}) &= \int p(\mathcal{Y} | \mathcal{X}, \theta) p(\theta) d\theta = \mathbb{E}_{\theta}[p(\mathcal{Y} | \mathcal{X}, \theta)] \\
    &= \int \mathcal{N}(y | \mathcal{X}\theta, \sigma^2 I) \mathcal{N}(\theta | m_0, S_0)d\theta
\end{align}
$$

### 2 bước tính toán Marginal Likelihood:

1. Xác định dạng của phân phối (Marginal Likelihood là phân phối Gauss).
2. Tính Trung bình (Mean) và Ma trận Hiệp phương sai (Covariance)
   Phương trình tạo ra dữ liệu: $y = X\theta + \epsilon$ với $\epsilon \sim \mathcal{N}(0, \sigma^2 I)$ là vector nhiễu độc lập.
   \_ Tính mean
   $$
        \mathbb{E}[\mathcal{Y} | \mathcal{X}] = \mathbb{E}_{\theta, \epsilon}[X\theta + \epsilon] = X\mathbb{E}[\theta] = Xm_0
   $$
   \_ Tính covariance
   $$
    \begin{align}
        Cov[\mathcal{Y} | \mathcal{X}] &= Cov_{\theta, \epsilon}[X\theta + \epsilon] = Cov_{\theta}[X\theta] + \sigma^2 I \\
        &= XCov_{\theta}[\theta]X^{\top} + \sigma^2 I = XS_0X^{\top} + \sigma^2 I
    \end{align}
   $$

Kết hợp 2 điều trên, ta được công thức dạng đóng cho Marginal Likelihood:

$$
    p(\mathcal{Y} | \mathcal{X}) = \mathcal{N}(y | Xm_0, XS_0X^{\top} + \sigma^2 I)
$$

Công thức của Marginal Likelihood nhìn cực kỳ giống với công thức của Phân phối dự đoán hậu nghiệm (Posterior Predictive Distribution) vì

- Marginal Likelihood bản chất là việc dự đoán các nhãn dữ liệu huấn luyện $y$ dựa trên thông tin tiền nghiệm (do đó nó dùng ma trận đầu vào $X$ và các tham số tiền nghiệm $m_0, S_0$).
- Phân phối dự đoán dùng để dự đoán nhãn dữ liệu kiểm tra mới $y_*$ dựa trên thông tin hậu nghiệm (do đó nó dùng vector đầu vào mới $x_*$ và các tham số hậu nghiệm $m_N, S_N$).

## Maximum Likelihood as Orthogonal Projection

Một mô hình có dạng

$$
    y = x\theta + \epsilon, \quad \epsilon \sim \mathcal{N}(0, \sigma^2)
$$

trong đó tham số $\theta$ là độ dốc của đường thẳng.

Ta biết được nghiệm của bài toán trên chính là

$$
    \theta_{MLE} = (X^{\top}X)^{-1}X^{\top}y
$$

với $X$ là vector chứa các đầu vào và $y$ là vector chứa các mục tiêu quan sát được.

Mục tiêu thực sự của việc tìm $\theta$ là để tái tạo/dự đoán lại các giá trị mục tiêu trên tập huấn luyện. Giá trị dự đoán (hay tái tạo) được tính bằng

$$
    X\theta_{MLE} = X(X^{\top}X)^{-1}X^{\top}y
$$

Ta nhận thấy rằng biểu thức $X(X^{\top}X)^{-1}X^{\top}$ thực chất là ma trận chiếu. Vector $X\theta_{MLE}$ chính là phép chiếu trực giao của vector quan sát $y$ (chứa nhiễu) xuống không gian con một chiều được sinh ra bởi $X$. Giá trị $\theta_{MLE}$ đóng vai trò là tọa độ của hình chiếu đó trong không gian con.

Điều này đúng khi mở rộng cho Feature Space. việc tìm MLE lúc này chính là thực hiện một phép chiếu trực giao vector dữ liệu $y$ (thuộc không gian $\mathbb{R}^N$) xuống một không gian con $K$ chiều.

$$
        y \approx \Phi \theta_{MLE} = \Phi(\Phi^{\top} \Phi)^{-1} \Phi^{\top}y
$$

Trường hợp đặc biệt khi các hàm đặc trưng $\phi_k$ tạo thành một cơ sở trực chuẩn (orthonormal basis). Khi này, các cột của $\Phi$ là trực chuẩn thì ma trận $\Phi^{\top} \Phi$ sẽ trở thành ma trận đơn vị $I$. Nhờ đó công thức của phép chiếu (nghiệm MLE) được rút gọn:

$$
    \Phi(\Phi^{\top} \Phi)^{-1} \Phi^{\top}y = \Phi \Phi^{\top}y = \left( \sum_{k = 1}^{K} \phi_k \phi_k^{\top} \right)y
$$

**Ý nghĩa:** Khi sử dụng cơ sở trực chuẩn, phép chiếu tổng thể phức tạp được phân rã thành tổng của các phép chiếu độc lập lên từng vector cơ sở $\phi_k$. Việc này loại bỏ hoàn toàn sự phụ thuộc (coupling) lẫn nhau giữa các đặc trưng. Đây là lý do tại sao trong xử lý tín hiệu, người ta rất ưa chuộng các hàm cơ sở trực giao như Wavelet hay Fourier. Nếu các hàm cơ sở ban đầu chưa trực giao, ta có thể dùng quy trình Gram-Schmidt để trực giao hóa chúng.

# Further Reading

## Mô hình Tuyến tính Tổng quát (GLMs)

Hồi quy tuyến tính có thể được mở rộng để xử lý các loại dữ liệu không có phân phối Gauss (ví dụ: dữ liệu phân loại dùng phân phối Bernoulli, hoặc dữ liệu đếm dùng phân phối Binomial/Poisson). Sự mở rộng này được thực hiện bằng cách kết hợp mô hình tuyến tính với một hàm trơn, phi tuyến gọi là hàm kích hoạt (activation function).

## Deep Neural Networks

Các GLMs chính là những khối xây dựng nền tảng tạo nên Deep Neural Networks. Mặc dù mạng nơ-ron có tính biểu đạt cao hơn hẳn hồi quy tuyến tính, nhưng việc ước lượng tham số của chúng lại vấp phải rào cản là bài toán tối ưu hóa không lồi (non-convex optimization).

## Gaussian Processes

Dựa trên khái niệm kernel trick, chúng ta có thể tính toán tích vô hướng trong các không gian vô hạn chiều. Quy trình Gauss là một mô hình có quan hệ mật thiết với hồi quy tuyến tính Bayes, cho phép thực hiện suy luận trực tiếp trên không gian các hàm số.

## Tiền nghiệm thưa (Sparsity Priors) và Chọn biến

Trong các bài toán thiếu dữ liệu trầm trọng, việc dùng tiền nghiệm Gauss truyền thống không còn tối ưu. Thay vào đó, sử dụng các tiền nghiệm phi Gauss (như tiền nghiệm Laplace) sẽ giúp ép nhiều tham số về 0 (tạo ra tính thưa), từ đó đóng vai trò như một bộ lựa chọn biến số (variable selection) tương đương với phương pháp LASSO.
