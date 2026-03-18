![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260308213707.png)

# Optimization using Gradient Descent

Ta xem xét bài toán tìm nghiệm thực nhỏ nhất của một hàm

$$
    \underset{x}{\text{min}} f(x)
$$

với $f: \mathbb{R}^d \to \mathbb{R}$ là hàm mục tiêu, và giả sử tất cả các hàm đề cập trong chương này đều khả vi.
Nếu

$$
x_1 = x_0 - \gamma ((\nabla f)(x_0))^{\top}
$$

với step-size nhỏ $\gamma \geq 0$ thì $f(x_1) \leq f(x_0)$.
Quan sát này cho phép chúng ta định nghĩa một thuật toán gradient descent đơn giản: nếu muốn tìm local optimum $f(x_*)$, ta bắt đầu với $x_0$ bất kỳ ta dự đoán và lặp lại tính toán:

$$
x_{i + 1} = x_i - \gamma_i ((\nabla f)(x_i))^{\top}
$$

với step-size $\gamma_i$ phù hợp, dãy $f(x_0) \geq f(x_1) \geq ...$ hội tụ đến một local minimum.
Lưu ý: Gradient descent có thể khá chậm để đạt tới local minimum.

## Step-size (learning rate)

Việc chọn step-size rất quan trọng. Nếu step-size quá nhỏ, thì tốc độ đạt tới local minimum có thể chậm, nhưng nếu quá lớn thì gradient descent có thể không hội tụ được (thậm chí phân kỳ).

Chúng ta sẽ sử dụng phương pháp momentum để làm mượt mà sự biến động thất thường của quá trình gradient descent và làm giảm dao động.

Phương pháp này rescale step-size mỗi lần lặp, phụ thuộc vào tính chất địa phương của hàm số. Có 2 loại heuristic cơ bản:

- Khi giá trị hàm số tăng sau mỗi bước thay đổi độ dốc, step-size sẽ lớn. Hoàn tác bước này và giảm step-size.
- Khi giá trị hàm số giảm thì step có thể lớn hơn. Thử tăng step-size.

Mặc dù bước "hoàn tác" dường như được xem là lãng phí tài nguyên, nhưng cách này đảm bảo tính hội tụ đơn điệu.

## Gradient descent with Momentum

Phương pháp này thêm một thành phần để ghi lại những gì xảy ra ở lần lặp trước. Thành phần ghi nhớ này làm giảm biên độ dao động và làm mượt quá trình cập nhập gradient.

Phương pháp dựa trên Momentum ghi nhớ cập nhập $\Delta x_i$ sau mỗi lần lặp $i$ và xác định lần cập nhập tiếp theo là tổ hợp tuyến tính của gradient trước và hiện tại:

$$
x_{i + 1} = x_i - \gamma_i ((\nabla f)(x_i))^{\top} + \alpha \Delta x_i
$$

$$
\Delta x_i = x_i - x_{i - 1} = \alpha \Delta x_{i - 1} - \gamma_{i - 1} ((\nabla f)(x_{i - 1}))^{\top}
$$

Với $\alpha \in [0, 1]$. Đôi lúc chúng ta chỉ biết được gradient xấp xỉ và những trường hợp này thì thành phần momentum hữu ích vì nó làm trung bình hóa các ước lượng nhiễu (noisy estimate) khác nhau của gradient.

## Stochastic Gradient Descent (SGD)

Việc tính toán gradient có thể rất tốn thời gian. Tuy nhiên vẫn có cách để tìm xấp xỉ gần đúng của gradient đơn giản.

SGD là phương pháp tìm cực tiểu của hàm mục tiêu được viết dưới dạng tổng các hàm khả vi khác nhau.

Trong học máy, cho $n = 1, ..., N$ data points, ta tường coi hàm mục tiêu là tổng của các hàm mất mát $L_n$ dưới dạng toán học như sau:

$$
    L(\theta) = \sum_{n = 1}^{N}L_n(\theta)
$$

Với $\theta$ là vector tham số ta quan tâm.
Một phương pháp đơn giản là xây dựng hàm log-likelihood (không âm)

$$
    L(\theta) = -\sum_{n = 1}^{N}\text{log}p(y_n|x_n, \theta)
$$

Với $x_n \in \mathbb{R}^d$ là training inputs, $y_n$ là training targets và $\theta$ là các tham số mô hình hồi quy.
Việc cập nhập các vector theo công thức gradient descent tiêu chuẩn

$$
    \theta_{i + 1} = \theta_i - \gamma_i(\nabla L(\theta_i))^{\top} = \theta_i - \gamma_i \sum_{n = 1}^{N} (\nabla L_n(\theta_i))^{\top}
$$

với step-size phù hợp $\gamma_i$ cần ước đánh giá tính toán rất nhiều, đặc biệt ở hàm tổng. Thay vì vậy, ta chỉ cần lựa chọn một tập con nhỏ hơn để tính tổng (ngẫu nhiên). Insight của việc này là ta chỉ cần một ước lượng không chệch (unbiased) của gradient để gradient descent hội tụ. Do đó bất kỳ ước lượng thực nghiệm khách quan nào về giá trị kỳ vọng cũng đảm bảo sự hội tụ cho gradient descent.

Tại sao chúng ta lại sử dụng xấp xỉ gradient? Một nguyên nhân lớn là do hằng số thực thi trong thực tế (như giới hạn của CPU & GPU). Kích thước mini-batch lớn sẽ đảm bảo ước lượng chính xác hơn, giảm phương sai trong quá trình cập nhập tham số. Ngoài ra mini-batch lớn giúp việc tính toán ma trận tốt hơn và tối ưu hơn trong triển khai. Việc giảm phương sai dẫn đến hội tụ ổn định hơn nhưng mỗi phép tính đạo hàm sẽ tốn kém hơn.

Ngược lại, kích thước mini-batch nhỏ dễ để ước lượng. Việc này làm nhiễu (noise) trong việc ước lượng gradient sẽ tránh được các điểm local optima khó chịu. Trong học máy, mục tiêu cần thiết không phải là tính toán đạo hàm chính xác để ước lượng cực tiểu địa phương của hàm mục tiêu mà là cải thiện hiệu suất tổng thể, do đó phương pháp này được sử dụng rộng rãi, và rất hiệu quả trong các vấn đề học máy quy mô lớn (large-scale) như huấn luyện deep neural networks trên hàng triệu ảnh, topic models, học tăng cường hoặc model Gaussian process quy mô lớn.

# Tối ưu hóa có ràng buộc và nhân tử Lagrange

Chúng ta quan tâm đến việc tối ưu hóa hàm mục tiêu có điều kiện:

$$
    \underset{x}{\text{min}} f(x)
$$

và

$$
    g_i(x) \leq 0 \quad \forall i = 1, ..., m
$$

Xét hàm

$$
J(x) = f(x) + \sum_{i = 1}^{m} l(g_i(x))
$$

trong đó $l(z)$ là hàm vô hạn bước (infinite step function)

$$
    l(z) =
    \begin{cases}
        0, \quad z \leq 0 \\
       \infty, \quad \text{otherwise}
    \end{cases}
$$

cách này sẽ đánh một giá trị vô hạn (infinity penalty) nếu như ràng buộc không được thỏa mãn. Tuy nhiên hàm $l(z)$ này khó để tối ưu. Thay vào đó nhân tử Lagrange sử dụng hàm tuyến tính thay vì hàm vô hạn bước:

$$
    \begin{align}
    L(\lambda, x) &= f(x) + \sum_{i = 1}^{m}\lambda_i g_i(x) \\
    &= f(x) + \lambda^{\top}g(x)
    \end{align}
$$

Dòng thứ 2, ta chuyển $g_i(x)$ thành vector $g(x)$, và các nhân tử Lagrange thành vector $\lambda \in \mathbb{R}^{d}$.

Bài toán này thể hiện tính đối ngẫu Lagrange. Ta chuyển việc tối ưu hóa bộ giá trị $x$ sang tối ưu hóa bằng bộ giá trị $\lambda$.

Thiết lập tính đối ngẫu yếu (weak duality), ta có:

$$
    \underset{x}{\text{min}} \underset{\lambda \geq 0}{\text{max}} L(x, \lambda) \geq \underset{\lambda \geq 0}{\text{max}} \underset{x}{\text{min}} L(x, \lambda)
$$

trong đó LHS là bài toán gốc cần tối ưu, còn RHS có phần bên trong $\underset{x}{\text{min}} L(x, \lambda)$ là hàm đối ngẫu $D(\lambda)$. Ta cần giải quyết bài toán đối ngẫu $\underset{\lambda \geq 0}{\text{max}} D(\lambda)$.

Bất đẳng thức trên cho thấy: giá trị cực đại của bài toán đối ngẫu luôn là cận dưới so với giá trị cực tiểu của bài toán gốc.

## Định lý KKT (out of the textbook)

Bài toán tối ưu tổng quát

$$
    \underset{x}{\text{min}} f(x)
$$

với ràng buộc

$$
    g_i(x) \leq 0, \quad i = 1,...,m \\
    h_j(x) = 0, \quad j = 1,...,n
$$

$g_i(x)$ và $h_j(x)$ lần lượt là ràng buộc cho bất đẳng thức và đẳng thức.

Ta xây dựng hàm Lagrange

$$
    L(x, \lambda, \mu) = f(x) + \sum_{i = 1}^{m}\lambda_i g_i(x) + \sum_{j = 1}^{n}\mu_j h_j(x)
$$

trong đó $\lambda_i$ là nhân tử cho bất đẳng thức, $\mu_j$ là nhân tử cho đẳng thức.

Nếu $x^*$ là nghiệm tối ưu và thỏa điều kiện thì tồn tại $\lambda^*, \mu^*$ sao cho

1. $$\nabla_xL(x^*, \lambda^*, \mu^*) = 0$$
2. $$ g*i(x^*) \leq 0 \\ h*j(x^*) = 0$$
3. $$\lambda_i^* \geq 0$$
4. $$\lambda_i^*g_i(x^*) = 0$$
   Đọc thêm: [KKT](https://www.cs.cmu.edu/~ggordon/10725-F12/slides/16-kkt.pdf) [KKT 2012](https://www.math.ntnu.no/emner/TMA4180/2013v/HEKnotes/kkttheoremv2012.pdf)

# Convex Optimization

Một tập $\mathcal{C}$ được gọi là một tập lồi (convex set) nếu $\forall x, y \in \mathcal{C}$ và mọi $\theta$ vô hướng thỏa $0 \leq \theta \leq 1$ ta có

$$
    \theta x + (1 - \theta)y \in \mathcal{C}
$$

Hàm $f: \mathbb{R}^d \to \mathbb{R}$ có miền là tập lồi. Hàm $f$ là hàm lồi nếu $\forall x, y \in \mathbb{D}_f, 0 \leq \theta \leq 1$ ta có

$$
    f(\theta x + (1 - \theta)y) \leq \theta f(x) + (1 - \theta)f(y)
$$

Nếu $f(x)$ khả vi thì nó lồi khi

$$
    f(y) \geq f(x) + \nabla_xf(x)^{\top}(y - x)
$$

Nếu biết $f(x)$ khả vi 2 lần thì tồn tại ma trận Hessian với mọi giá trị trong miền của $x$. Khi đó $f(x)$ lồi khi và chỉ khi $\nabla_{x}^{2}f(x)$ là bán xác định dương.

Dễ thấy nếu $f_1(x), f_2(x)$ đều lồi thì $\alpha f_1(x) + \beta f_2(x)$ cũng là hàm lồi.

Nói chung, một bài toán tối ưu hóa có ràng buộc được gọi là tối ưu hóa lồi nếu

$$
    \underset{x}{\text{min}}f(x) \\
$$

với điều kiện

$$
    g_i(x) \leq 0, \quad \forall i = 1,..., m \\
    h_j(x) = 0, \quad \forall j = 1,...,n
$$

trong đó $f(x)$ và $g_i(x)$ là các hàm lồi, tập các $h_j(x) = 0$ là tập lồi.

Phần tiếp theo sẽ nói về 2 lớp bài toán tối ưu lồi phồ biến.

## Linear Programming

Giả sử trong trường hợp đặc biệt, tất cả các hàm ta xét trên đều là tuyến tính

$$
    \underset{x \in \mathbb{R}^d}{\text{min}} \quad c^{\top}x \quad (1)
$$

với điều kiện

$$
    Ax \leq b, \quad A \in \mathbb{R}^{m \times d}, b \in \mathbb{R}^m
$$

đây được gọi là bài toán lập trình tuyến tính có $d$ biến và $m$ ràng buộc tuyến tính. Hàm Lagrange được cho bởi

$$
    L(x, \lambda) = c^{\top}x + \lambda^{\top}(Ax - b)
$$

trong đó, $\lambda \in \mathbb{R}^m$ là vector nhân tử Lagrange không âm. Sắp xếp lại thành phần theo $x$ ta được công thức:

$$
    L(x, \lambda) = (c + A^{\top}\lambda)x - \lambda^{\top}b
$$

Đạo hàm theo $x$ lấy giá trị $0$ ta có

$$
    c + A^{\top}\lambda = 0
$$

Do đó, $D(\lambda) = -\lambda^{\top}b$ và dẫn đến bài toán tối ưu đối ngẫu là:

$$
    \underset{\lambda \in \mathbb{R}^m}{\text{max}} - b^{\top} \lambda \quad (2)
$$

với điều kiện

$$
    c + A^{\top}\lambda = 0 \\
    \lambda \geq 0
$$

Ta lựa chọn giải bài toán gốc $(1)$ hoặc bài toán đối ngẫu $(2)$ tùy vào $m$ hay $d$ lớn hơn.

## Quadratic programming

Xem xét các hàm bậc 2 lồi với ràng buộc tuyến tính:

$$
    \underset{x \in \mathbb{R}^d}{\text{min}} \quad \frac{1}{2}x^{\top}Qx+ c^{\top}x
$$

với điều kiện

$$
    Ax \leq b \quad A \in \mathbb{R}^{m \times d}, b \in \mathbb{R}^m, c \in \mathbb{R}^d
$$

Hàm đối xứng lập phương $Q \in \mathbb{R}^{d \times d}$ xác định dương, và do đó hàm mục tiêu là lồi. Đây được gọi là Quadratic programming.
Biến đổi linh tinh như trên, ta được vấn đề đối ngẫu:

$$
    \underset{\lambda \in \mathbb{R}^m}{\text{max}} \quad -\frac{1}{2}(c + A^{\top} \lambda)^{\top}Q^{-1}(c + A^{\top}\lambda) - \lambda^{\top}b
$$

với điều kiện

$$
    \lambda \geq 0
$$

## Legendre–Fenchel Transform and Convex Conjugate

Một tính chất thú vị của tập lồi là nó có thể mô tả tương đương với các siêu phẳng đỡ. Một siêu phẳng được gọi là siêu phẳng đỡ là siêu phẳng chạm vào tập lồi và toàn bộ tập nằm về một phía của nó. Các supporting hyperplane thực chất là tiếp tuyến (tangent) của hàm tại điểm đó và tiếp tuyến của hàm tại $x_0$ được xác định bởi gradient của hàm tại điểm đó.

_TLDR: Do tập lồi có thể mô tả bằng các tiếp tuyến, nên hàm lồi cũng có thể được mô tả thông qua gradient của nó. Ý tưởng này được chuẩn hóa bởi phép biến đổi Legendre (Legendre transform)._

Legendre–Fenchel transform là một phép biến đổi từ hàm lồi khả vi sang hàm mới phụ thuộc vào gradient của hàm đó. Nó áp dụng lên toàn bộ hàm $f(x)$ chứ không chỉ lên biến $x$ hay tại 1 điểm của $f(x)$.

Legendre–Fenchel transform còn được gọi là convex conjugate, có liên hệ chặt chẽ với lý thuyết đối ngẫu (duality) trong tối ưu hóa.

Convex conjugate của một hàm $f: \mathbb{R}^D \to \mathbb{R}$ là hàm $f*$ được định nghĩa bởi

$$
    f*(s) = \underset{x \in \mathbb{R}^D}{\text{sup}} \quad (\langle s, x \rangle - f(x))
$$

Định nghĩa trên không yêu cầu hàm $f$ phải là hàm lồi hay khả vi.

Ý nghĩa: ban đầu $f(x)$ mô tả hàm theo vị trí $x$, sau Legendre transform thì $f*(s)$ mô tả hàm theo độ dốc $s$.

Tính chất:

- Dù $f(x)$ không lồi thì $f*(s)$ luôn lồi.

### Legendre transform cổ điển

Là trường hợp đặc biệt của Legendre-Fenchel transform, ta không cần tìm **supremum** với trường hợp hàm khả vi lồi.

Trường hợp đặc biệt đối với một hàm khả vi lồi thì tại điểm $x_0$, tiếp tuyến chạm vào $f(x_0)$ do đó

$$
    f(x_0) = sx_0 + c
$$

Trong đó $s = \frac{df}{dx}$.

Ta muốn biểu diễn hàm lồi $f(x)$ theo gradient $\nabla_xf(x)$ của nó, và $s = \nabla_xf(x_0).$ Sắp xếp lại biểu thức để nhận được giá trị $-c$

$$
    -c = sx_0 - f(x_0)
$$

$-c$ thay đổi theo $x_0$, đó là lý do có thể xem nó như là hàm của $s$:

$$
    f*(s) = sx_0 - f(x_0)
$$

Hàm liên hợp lồi có tính chất đẹp:

- Áp dụng Legendre transform một lần nữa ta được hàm ban đầu.
