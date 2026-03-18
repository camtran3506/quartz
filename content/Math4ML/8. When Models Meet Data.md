# When Model Meets Data

Vì lười và nhiều lý thuyết nên tôi đã notebooklmize nó.

## Data, Model & Learning

Câu hỏi cốt lõi của học máy là "Thế nào là một mô hình tốt?". Một nguyên tắc cốt lõi là mô hình tốt phải hoạt động hiệu quả trên những dữ liệu chưa từng thấy. Để đạt được điều này, một hệ thống học máy được xây dựng dựa trên ba thành phần chính:

### Dữ liệu dưới dạng Vector

Dữ liệu trong học máy được giả định là có thể đọc được bằng máy tính và được biểu diễn dưới định dạng số theo dạng bảng _(tabular format)_.

- Chuyển đổi định dạng: Các biến phân loại _(categorical variables)_ cần được chuyển đổi thành số.
  Ví dụ: Giới tính có thể được chuyển thành $0$ (Nam) và $1$ (Nữ), hoặc thành các giá trị $-1$ và $+1$. Một ví dụ khác là biến đổi mã bưu điện (chuỗi ký tự) thành tọa độ vĩ độ và kinh độ, hoặc lược bỏ các cột không mang thông tin như "Tên" để bảo vệ quyền riêng tư _(privacy)_.
- Lưu ý về chuẩn hóa _(Standardization_): Nếu không có thông tin gì thêm, dữ liệu nên được dịch chuyển và chia tỷ lệ sao cho chúng có trung bình thực nghiệm _(empirical mean)_ bằng $0$ và phương sai _(empirical variance)_ bằng $1$.
- Thuật ngữ định danh:
  - Mỗi hàng trong bảng dữ liệu đại diện cho một thực thể, được gọi là một ví dụ _(example)_ hoặc một điểm dữ liệu _(data point)_, ký hiệu là một vector $x^n \in \mathbb{R}^D$.
  - Mỗi cột đại diện cho một khía cạnh của dữ liệu, được gọi là đặc trưng _(feature)_, thuộc tính _(attribute_), hoặc biến đồng phương sai _(covariate)_.
  - Trong bài toán học có giám sát _(supervised learning)_, mỗi ví dụ $x_n$ đi kèm với một nhãn $y_n$ _(label)_. Nhãn này còn có nhiều tên gọi khác như mục tiêu _(target_), biến phản hồi _(response variable)_, hoặc chú thích _(annotation)_.

- Bản đồ đặc trưng _(Feature map)_: Việc biểu diễn dữ liệu dưới dạng vector cho phép áp dụng đại số tuyến tính. Ta có thể sử dụng hàm $\phi(\cdot)$ (gọi là bản đồ đặc trưng - _feature map_) để biến đổi các đầu vào $x_n$ lên một không gian nhiều chiều hơn, tạo ra các kết hợp phi tuyến tính của các đặc trưng ban đầu giúp bài toán học trở nên dễ dàng hơn.

### Mô hình dưới dạng Hàm số

- Bộ dự đoán (_Predictor_): Là một hàm số nhận một ví dụ đầu vào (vector các đặc trưng) và tạo ra một đầu ra. Đối với đầu ra là một số thực vô hướng, hàm số này được viết là $f: \mathbb{R}^D \to \mathbb{R}$
- Hàm tuyến tính (_Linear functions_): Tài liệu tập trung vào trường hợp đặc biệt là các hàm tuyến tính, có dạng $f(x) = \theta^{\top}x + \theta_0$ với $\theta$ và $\theta_0$ là các tham số chưa biết (_parameters_).
  **Lưu ý:** Việc giới hạn ở các hàm tuyến tính tạo ra một sự cân bằng tuyệt vời giữa tính tổng quát của bài toán (vẫn giải quyết được nhiều vấn đề) và lượng kiến thức toán học nền tảng cần thiết.

### Mô hình dưới dạng Phân phối Xác suất

Thay vì chỉ xem bộ dự đoán là một hàm số đơn lẻ, ta có thể sử dụng các mô hình xác suất (_probabilistic models_) để định lượng sự không chắc chắn (_uncertainty_).

- Dữ liệu trong thực tế thường chứa nhiễu (_noise_), do đó quan hệ dự đoán thường được mô hình hóa thành $y = f(x) + \epsilon$, với $\epsilon$ là nhiễu.
- Xác suất cung cấp ngôn ngữ chặt chẽ để thể hiện sự không chắc chắn đối với cả dữ liệu (thông qua hàm khả năng - _likelihood_) lẫn các tham số của mô hình (thông qua phân phối tiền nghiệm - _prior_, và hậu nghiệm - _posterior_).

## Learning is Finding Parameters

Mục tiêu cốt lõi của việc học là tìm ra một mô hình và các tham số của nó sao cho bộ dự đoán hoạt động tốt trên dữ liệu chưa từng thấy. Quá trình này được chia thành 3 giai đoạn thuật toán phân biệt:

### 1. Dự đoán hoặc suy luận (Prediction or inference)

Sử dụng bộ dự đoán đã được cố định tham số áp dụng lên dữ liệu kiểm tra (_test data_) mới. Trong các mô hình xác suất, giai đoạn này được gọi riêng là suy luận (_inference_).

**Lưu ý:** Thuật ngữ "inference" đôi khi gây nhầm lẫn vì một số tài liệu dùng nó để chỉ việc ước lượng tham số, thay vì dự đoán.

### 2. Huấn luyện hoặc ước lượng tham số (Training or parameter estimation)

Sử dụng dữ liệu huấn luyện (_training data_) để điều chỉnh mô hình. Có hai chiến lược chính:

- Tìm một ước lượng điểm (_point estimate_) tốt nhất thông qua các phương pháp tối ưu hóa số học (_hill-climbing_). Cách này liên quan đến việc cực tiểu hóa rủi ro thực nghiệm (_empirical risk minimization_) hoặc cực đại hóa khả năng (_maximum likelihood_).
- Sử dụng suy luận Bayes (_Bayesian inference_) đối với các mô hình xác suất.

### 3. Tinh chỉnh siêu tham số hoặc lựa chọn mô hình (Hyperparameter tuning or model selection)

Đưa ra các quyết định ở cấp độ cao về cấu trúc của bộ dự đoán (ví dụ: chọn số lượng thành phần hoặc loại phân phối xác suất).

**Ví dụ & Lưu ý:** Việc lựa chọn số lượng thành phần của một mô hình là một siêu tham số (_hyperparameter_). Sự khác biệt giữa tham số (_parameter_) và siêu tham số là tương đối: tham số thường là các biến được tối ưu hóa trực tiếp bằng thuật toán số học, trong khi siêu tham số là các biến cấp cao kiểm soát sự phân phối của các tham số đó và thường yêu cầu kỹ thuật tìm kiếm.

- Để đối phó với hiện tượng quá khớp (overfitting - mô hình chỉ học thuộc lòng dữ liệu huấn luyện), ta sử dụng kỹ thuật xác thực chéo (_cross-validation_) để mô phỏng hành vi của mô hình trên dữ liệu mới.
- Sự cân bằng giữa việc khớp sát dữ liệu huấn luyện và việc giữ cho mô hình đủ "đơn giản" được thực hiện thông qua kỹ thuật chính quy hóa (_regularization_) hoặc thêm vào một phân phối tiền nghiệm (_prior_).
- Lưu ý triết học: Trong triết học, quá trình suy luận để tìm ra lời giải thích tốt nhất (đơn giản nhưng khớp dữ liệu) này không phải là diễn dịch hay quy nạp, mà được gọi là suy luận giả định (_abduction - inference to the best explanation_).
- Đối với các mô hình phi xác suất, quá trình lựa chọn mô hình thường được thực hiện qua kỹ thuật xác thực chéo lồng nhau (_nested cross-validation_)

# Empirical Risk Minimization

Mục này trình bày về ý tưởng giảm thiểu rủi ro thực nghiệm, một nguyên lý cốt lõi cho phép ta định nghĩa "việc học" là gì đối với các mô hình phi xác suất. Quá trình này bao gồm 4 quyết định thiết kế chính:

## Hypothesis Class of Functions (Lớp hàm giả thuyết)

Khi có một tập dũ liệu gồm $N$ bộ $x_n \in \mathbb{R}^D$ tương ứng với các nhãn $y_n \in \mathbb{R}$ trong bài toán supvervised learning, ta cần ước lượng bộ predictor $f(\cdot, \theta): \mathbb{R}^d \to \mathbb{R}$ được tham số hóa bởi $\theta$. Mục tiêu là tìm ra $\theta^*$ tốt để fit tốt với data, hay

$$
    f(x_n, \theta^*) \approx y_n \quad \forall n = 1,...,N
$$

Ta ký hiệu $\hat{y} = f(x_n, \theta^*)$.
**Ví dụ:** trong hồi quy tuyến tính bình phương tối thiểu, predictor được viết dưới dạng một hàm tuyến tính thu gọn: $f(x_n, \theta) = \theta^{\top}x_n$.

## Loss Function for Training (Hàm mất mát cho huấn luyện)

Để định nghĩa một model fit tốt với dữ liệu, ta cần một thước đo, đó là hàm mất mát (loss function) được ký hiệu $l(y_n, \hat{y}_n)$ (nhận vào nhãn thực tế $y_n$ và dự đoán $\hat{y}_n$ và trả về error là một số không âm).

Giả định rằng các ví dụ trong tập training set là độc lập và phân phối đồng nhất (independent and identically distributed), ta có thể đánh giá rủi ro thực nghiệm trên toàn bộ model bằng công thức:

$$
    R_{\text{emp}}(f, X, y)= \frac{1}{N}\sum_{n = 1}^{N}l(y_n, \hat{y}_n)
$$

Chiến lược cho "việc học" này được gọi là empirical risk minimization.

**Ví dụ:** Trong bài toán hồi quy, ta thường dùng $l(y_n, \hat{y}_n)= (y_n - \hat{y}_n)^2$. Khi đó việc giảm thiểu rủi ro thực nghiệm trở thành bài toán tối ưu hóa: $\underset{\theta \in \mathbb{R}^D}{\text{min}} \frac{1}{N} \mid \mid y - X\theta \mid \mid^2$.

**Lưu ý:** Mục đích của việc training không chỉ là hoạt động tốt trên tập training set mà trên cả những data chưa từng thấy. Rủi ro này được gọi là rủi ro kỳ vọng (hay population risk) ký hiệu là $R_{\text{true}}(f) = \mathbb{E}_{x, y}[l(y, f(x))]$. Có 2 bài toán nảy sinh từ việc cực tiểu hóa expected risk:

- Nên thay đổi quy trình training thế nào để hiệu quả tổng quát tốt hơn?
- Làm sao để ước lượng expected risk từ bộ dữ liệu hữu hạn?

## Regularization to Reduce Overfitting

Để tránh tình trạng overfit, ta thêm vào một hạng tử penalty nhằm kìm hãm thuật toán tối ưu, không cho phép nó chọn một bộ predictor quá linh hoạt.

**Ví dụ:** Regularized Least Squares: bổ sung thêm hạng tử penalty $||\theta||^2$ vào hàm mục tiêu $\underset{\theta \in \mathbb{R}^D}{\text{min}} \frac{1}{N} \mid \mid y - X\theta \mid \mid^2 + \lambda||\theta||^2$. Trong đó $\lambda$ được gọi là regularization parameter và $||\theta||^2$ được gọi là regularizer. Việc này giúp ép các giá trị của $\theta$ gần về gốc tọa độ hơn, ngăn hiện tượng overfitting.

## Cross-Validation to Assess the Generalization Performance

Vì dữ liệu có hạn, ta nên tìm cách chia bộ data một cách khéo léo để vừa có đủ dữ liệu huấn luyện, vừa đánh giá được độ chính xác của model.

- Validation set ($\mathcal{V}$): một tập con của data huấn luyện giữ lại để đánh giá model.
- cross-validation K lần: chia nhỏ bộ dữ liệu thành $K$ phần, lấy $K - 1$ phần ($f^{(k)})$ để làm training set và tập còn lại là validation set. Quá trình này được lặp lại $K$ lần và lấy trung bình hiệu suất của $K$ lần chạy:
  $$
      \mathbb{E}[R(f, \mathcal{V})] \approx \frac{1}{K}\sum_{k = 1}^{K} R(f^{(k)}, \mathcal{V}^{(k)})
  $$

**Lưu ý:** Cách này xấp xỉ tốt rủi ro tổng quát hóa kỳ vọng (expected generalization error) nhưng chi phí tính toán cao do phải train model $K$ lần. Tuy nhiên ta có thể huấn luyện song song $K$ lần trên các máy chủ độc lập.

# Parameter Estimation

## Maximum Likelihood Estimation (MLE)

Ý tưởng của MLE là định nghĩa một hàm các tham số giúp chúng ta tìm được model fit tốt với data. MLE tập trung vào hàm likelihood (hay hàm logarit âm). Ví dụ với tham số $\theta$ thì

$$
    \mathcal{L}_x(\theta) = \log p(x | \theta)
$$

Nhờ tính độc lập và phân phối đồng nhất, hàm likelihood của toàn bộ tập dữ liệu có thể biểu diễn dưới dạng tích các hàm likelihood trên từng điểm đơn lẻ. Do đó, hàm log-likelihood sẽ biến hàm likelihood từ tích thành tổng và giúp việc đạo hàm trở nên dễ dàng hơn. Ngoài ra logarit hóa hàm likelihood tránh việc tràn số dưới (numerical underflow). (Tham khảo thêm chương Bayesian Statistics trong sách MIT).

## Maximum A Posteriori Estimation (MAP)

MLE có thể dẫn đến hiện tượng overfitting, đặc biệt khi dữ liệu nhỏ. Để khắc phục, ta đưa thêm các giả định về việc các tham số nên nằm ở đâu trước khi quan sát dữ liệu.

Áp dụng định lý Bayes:

$$
    p(\theta | x) = \frac{p(x | \theta)p(\theta)}{p(x)}
$$

trong đó

- $p(x | \theta)$ là hàm likelihood
- $p(\theta)$ là prior
- $p(\theta | x)$ là posterior

Vì $p(x)$ là hằng số, nên đôi khi cũng có thể viết thành:

$$
    p(\theta | x) \propto p(x | \theta)p(\theta)
$$

## Model Fitting

Khi huấn luyện model $\mathcal{M}_{\theta}$ để tiệm cận gần nhất với $\mathcal{M}^*$ (vốn là một ẩn số), ta sẽ gặp 3 trạng thái sau:

### Overfitting

Xảy ra khi lớp model được tham số hóa quá phong phú/phức tạp so với mô hình thực tế. Nó có quá nhiều tham số tự do, dẫn đến việc model "học vẹt" luôn cả các nhiễu (noise) trong tập huấn luyện. Kết quả là model hoạt động hoàn hảo trên tập huấn luyện nhưng thất bại thảm hại khi dự đoán dữ liệu mới. MLE trên tập dữ liệu nhỏ rất hay gặp tình trạng này.

### Underfitting

Xảy ra khi lớp model $\mathcal{M}_{\theta}$ không đủ tính biểu đạt (quá đơn giản) để nắm bắt được quy luật thực sự của tập dữ liệu sinh ra từ $\mathcal{M}^*$. Model này sẽ có sai số lớn trên cả tập huấn luyện và tập kiểm tra.

### Fitting well

Không bị overfitting hay underfitting, vừa vặn để mô tả tập dữ liệu và khả năng tổng quát hóa cao trên dữ liệu mới.
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260311181601.png)

# Mô hình xác suất và suy luận

## Mô hình xác suất

Mô hình xác suất biểu diễn các khía cạnh không chắc chắn của một thí nghiệm dưới dạng các phân phối xác suất. Lợi ích của chúng là cung cấp một bộ công cụ thống nhất và nhất quán từ lý thuyết xác suất để mô hình hóa, suy luận, dự đoán và lựa chọn mô hình.

## Suy luận Bayes (đọc trong sách XSTK MIT đi)

## Latent-Variable Models (mô hình biến tiềm ẩn)

Trong thực tế, việc đưa thêm các biến tiềm ẩn (latent variables) ký hiệu là $z$ (bên cạnh các tham số $\theta$) vào mô hình thường mang lại nhiều lợi ích

- Chúng không trực tiếp tham số hóa mô hình, mà dùng để mô tả quá trình sinh dữ liệu, giúp mô hình dễ diễn giải hơn, đơn giản hóa cấu trúc mô hình, và tạo ra các cấu trúc phong phú với ít tham số hơn.
- Quá trình sinh dữ liệu: Với dữ liệu $x$, tham số $\theta$ và biến tiềm ẩn $z$, ta có phân phối có điều kiện $p(x | z, \theta)$. Vì $z$ là tiềm ẩn, ta đặt một phân phối tiền nghiệm $p(z)$ lên chúng.
- 2 bước học mô hình:
  - Tính likelihood: Loại bỏ $z$ bằng cách tính tích phân $p(x | \theta) = \int p(x | z, \theta)p(z)dz$
  - Sử dụng likelihood vừa tính được để MLE, MAP hoặc suy luận Bayes.
- Hậu nghiệm của biến tiềm ẩn: việc tính tích phân theo cả $\theta$ và $z$ thường không khả thi. Do dó một đại lượng dễ tính toán hơn là hậu nghiệm của biến tiềm ẩn được lấy điều kiện dựa trên các tham số mô hình cố định:
  $$
      p(z | \mathcal{X}, \theta) = \frac{p(\mathcal{X} |z, \theta)p(z)}{p(\mathcal{X} | \theta)}
  $$
  với $\mathcal{X}$ là data set.

# Directed Graphical Models

Mô hình đồ thị có hướng cung cấp một ngôn ngữ đồ thị để biểu diễn các mô hình xác suất một cách nhỏ gọn và súc tích, cho phép ta nhận diện trực quan các mối quan hệ phụ thuộc giữa các biến ngẫu nhiên. Mô hình đồ thị biểu diễn trực quan cách joint distribution của tất cả các biến ngẫu nhiên có thể được phân rã thành tích của các nhân tử nhỏ hơn. Mô hình đồ thị có hướng còn được gọi là mạng Bayes (Bayesian networks).

Trong một mô hình đồ thị, các nút (nodes) đại diện cho các biến ngẫu nhiên, còn các cạnh (edges) đại diện cho các quan hệ xác suất (ví dụ: xác suất có điều kiện) giữa các biến đó.

## Graph Semantics (ngữ nghĩa của đồ thị)

### Định nghĩa

![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260311185238.png)
Các mũi tên từ node $a$ sang node $b$ biểu thị phân phối của $b$ phụ thuộc vào $a$, tức là chứa thành phần $p(b | a)$.

Ví dụ: từ hình (a), ta có thể suy luận $p(a, b, c) = p(c | a, b)p(b | a)p(a)$. Thành phần $c$ được suy luận từ $a$ và $b$.

Ta có thể xây dựng đồ thị bằng cách:

- Tạo node cho tất cả biến ngẫu nhiên
- Thêm các cạnh có hướng ứng với sự phụ thuộc giữa các biến ngẫu nhiên.

Một cách tổng quát, joint distribution $p(x_1, ..., x_K)$ được cho bởi công thức:

$$
    p(x_1,...,x_n) = \prod_{k = 1}^{K}p(x_k | Pa_k)
$$

$Pa_k$ nghĩa là cha của node $x_k$, là các node có cạnh hướng mũi tên tới $x_k$.

### Các ký hiệu khác

Trong một thí nghiệm tung đồng xu $N$ lần với cùng một xác suất $\mu$, thay vì vẽ $N$ nút $x_1,...,x_N$ lặp đi lặp lại cùng phụ thuộc vào $\mu$, ta có thể gom chúng lại bằng một khung hình chữ nhật (plate). Khung này biểu thị rằng mọi thứ bên trong nó được lặp lại $N$ lần, giúp mô hình trở nên cực kỳ gọn gàng.

Siêu tiền nghiệm (Hyperprior): Đồ thị cũng cho phép ta dễ dàng thêm một tầng phân phối tiền nghiệm thứ hai (đặt lên trên các tham số của tầng tiền nghiệm thứ nhất), gọi là các siêu tiền nghiệm (hyperpriors).
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260311190139.png)

## Conditional Independence and d-Separation (Độc lập có điều kiện và phân tách d)

Mô hình đồ thị có hướng cho phép chúng ta tìm ra các tính chất độc lập có điều kiện (conditional independence) của phân phối đồng thời chỉ bằng cách nhìn vào cấu trúc của đồ thị. Công cụ cốt lõi để làm việc này là khái niệm phân tách d (d-separation).

Giả sử có một đồ thị có hướng với $\mathcal{A}, \mathcal{B}, \mathcal{C}$ là các node tùy ý. Định nghĩa "$\mathcal{A}$ độc lập với $\mathcal{B}$ với điều kiện $\mathcal{C}$" được biểu diễn toán học như sau:

$$
    \mathcal{A} \perp\!\!\!\perp \mathcal{B} \mid \mathcal{C}
$$

Điều này có thể được suy luận trên đồ thị có hướng không chu trình (DAG) theo quy tắc:

- Xét tất cả các "đường đi" (trails - bỏ qua hướng của mũi tên) nối từ bất kỳ nút nào trong $\mathcal{A}$ đến bất kỳ nút nào trong $\mathcal{B}$.
- Một đường đi bị coi là bị chặn nếu nó đi qua một nút thỏa mãn một trong hai điều kiện sau:
  - Các mũi tên trên đường đi gặp nhau theo kiểu head-to-tail ($\rightarrow \circ \rightarrow$) hoặc tail-to-tail ($\leftarrow \circ \rightarrow$) tại nút đó, VÀ nút đó nằm trong tập $\mathcal{C}$ (nghĩa là biến này đã được quan sát/đã biết).
  - Các mũi tên gặp nhau theo kiểu head-to-head ($\rightarrow \circ \leftarrow$) tại nút đó, VÀ cả nút đó lẫn bất kỳ hậu duệ (descendants) nào của nó ĐỀU KHÔNG nằm trong tập $\mathcal{C}$ (chưa được quan sát).
- Kết luận: Nếu tất cả các đường đi từ $\mathcal{A}$ đến $\mathcal{B}$ đều bị chặn, ta nói $\mathcal{A}$ được phân tách d (d-seperated) khỏi $\mathcal{B}$ bởi $\mathcal{C}$. Khi đó, tính chất độc lập có điều kiện được thỏa mãn.

Việc nhận diện được tính độc lập có điều kiện thông qua đồ thị cho phép ta phân rã các biểu thức xác suất phức tạp thành các phần nhỏ hơn, giúp việc tính toán và tối ưu hóa dễ dàng hơn nhiều.
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260311191623.png)

# Model Selection

Phần này cung cấp các cơ chế thiết yếu để đánh giá xem một mô hình sẽ tổng quát hóa (generalize) như thế nào khi tiếp xúc với dữ liệu mới.
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260311193751.png)

## Nested Cross-Validation

Đây là phương pháp sử dụng hai cấp độ xác thực chéo (K-lần) lồng vào nhau để vừa chọn được mô hình tốt nhất, vừa đánh giá được hiệu suất tổng quát hóa của nó. Bao gồm:

- Vòng lặp trong (Inner level): Sử dụng một tập dữ liệu được gọi là tập xác thực (validation set) để ước lượng hiệu suất của các lựa chọn mô hình hoặc siêu tham số khác nhau. Mô hình có hiệu suất tốt nhất trên tập này sẽ được chọn. Vòng lặp này ước lượng giá trị kỳ vọng của error tổng quát bằng cách xấp xỉ sai số thực nghiệm trên tập xác thực:

  $$
      \mathbb{E}_{\mathcal{V}}[R(\mathcal{V} | M)] = \frac{1}{K}\sum_{k = 1}^{K}R(\mathcal{V}^{(k)} | M)
  $$

  trong đó $R(\mathcal{V}^{(k)}$ là rủi ro thực nghiệm trên tập xác thực $\mathcal{V}$ cho model $M$.

- Vòng lặp ngoài (Outer level): Mô hình tốt nhất (được chọn từ vòng lặp trong) sẽ được đánh giá hiệu suất tổng quát hóa trên một phần dữ liệu hoàn toàn tách biệt gọi là tập kiểm tra (test set).

Ưu điểm của phương pháp này là nó không chỉ xấp xỉ rủi ro tổng quát hóa kỳ vọng mà còn cung cấp các thống kê bậc cao như sai số chuẩn (standard error), giúp ta biết ước lượng trung bình của mình có độ không chắc chắn là bao nhiêu.
![Img](https://raw.githubusercontent.com/anhduc1526/marktext-image/master/imgyank-note-picgo-img-20260311194340.png)

## Bayesian Model Selection

Tất cả các phương pháp lựa chọn mô hình đều cố gắng tìm ra sự cân bằng (trade-off) giữa độ phức tạp của mô hình và mức độ khớp với dữ liệu. Mục tiêu là tìm ra mô hình đơn giản nhất nhưng vẫn giải thích tốt dữ liệu - nguyên lý này được gọi là Occam's razor. Các cơ chế và khái niệm cốt lõi cấu thành nên phương pháp này:

### 1. Automatic Occam's Razor

Khác với các phương pháp phải chủ động cộng thêm một hạng tử phạt (penalty term) để ép mô hình trở nên đơn giản, xác suất Bayes tự động tích hợp sự trừng phạt này vào quá trình tính toán.

- Mức độ một mô hình $M_i$ dự đoán được dữ liệu $D$ được đánh giá qua đại lượng evidence $p(D | M_i)$
- Bởi vì tổng xác suất của bằng chứng trên toàn bộ không gian các tập dữ liệu bắt buộc phải bằng $1$, một mô hình đơn giản ($M_1$) (chỉ có thể giải thích một lượng nhỏ các tập dữ liệu) sẽ dồn khối lượng xác suất rất cao cho những tập dữ liệu đó.
- Ngược lại, một mô hình phức tạp ($M_2$) (linh hoạt và có thể giải thích nhiều loại tập dữ liệu khác nhau) sẽ bị dàn mỏng xác suất ra toàn không gian.

TLDR: Nếu một mô hình đơn giản có thể dự đoán tốt cùng một tập dữ liệu, nó sẽ được gán xác suất cao hơn mô hình phức tạp kia.

### 2. Quá trình sinh dữ liệu phân cấp

Lựa chọn mô hình Bayes xem xét quá trình sinh ra dữ liệu theo từng cấp độ:

1. Chọn một mô hình $M_k$ từ tập các mô hình dựa trên phân phối tiền nghiệm của mô hình $p(M)$.
2. Lấy mẫu các tham số $\theta_k$ dựa trên phân phối tiền nghiệm của tham số tương ứng với mô hình đó $p(\theta_k | M_k)$.
3. Sinh ra dữ liệu $D$ thông qua hàm likelihood $P(D | \theta_k)$.

### 3. Đánh giá và Lựa chọn thông qua Marginal Likelihood

Để quyết định mô hình nào tốt nhất, ta áp dụng định lý Bayes để tính phân phối hậu nghiệm của mô hình (posterior distribution over models):

$$
    p(M_k | D) \propto p(M_k)p(D | M_k)
$$

Trong đó

$$
    p(D | M_k) = \int p(D | \theta_k)p(\theta_k | M_k)d\theta_k
$$

được gọi là Marginal Likelihood.

Để chọn ra mô hình tối ưu (dựa trên MAP), ta tìm mô hình tối đa hóa $p(M_k | D)$. Nếu ta giả định các mô hình ban đầu có xác suất tiền nghiệm bằng nhau (uniform prior), việc chọn mô hình tốt nhất tương đương với việc chọn mô hình có Marginal Likelihood lớn nhất.

**Lưu ý:** Sự khác biệt lớn nhất giúp Bayesian Model Selection tránh được tình trạng overfitting nằm ở cách sử dụng likelihood:

- Hàm Likelihood $p(D | \theta_k)$: Thường được dùng trong MLE, rất dễ dẫn đến quá khớp vì nó liên tục thay đổi tham số $\theta_k$ để cố gắng fit sát nhất với dữ liệu huấn luyện.
- Marginal Likelihood $p(D | M_k)$: Hoàn toàn không bị quá khớp vì các tham số $\theta_k$ đã được tích phân hóa và loại bỏ. Ta không còn tham số nào để fit dữ liệu nữa, và bản thân khả năng biên đã tự động cân bằng sự đánh đổi giữa độ phức tạp của mô hình và mức độ phù hợp với dữ liệu.

### 4. Nhân tử Bayes để so sánh mô hình

Khi so sánh hai mô hình $M_1$ và $M_2$ với cùng một tập dữ liệu $D$, ta có thể tính tỷ lệ của hai phân phối hậu nghiệm:

$$
    \frac{p(M_1 | D)}{p(M_2 | D)} = \frac{p(M_1)}{p(M_2)} \times \frac{p(D | M_1)}{p(D | M_2)}
$$

trong đó:

- Posterior odds: LHS
- Prior odds: tích tử đầu tiên của RHS
- Bayes factor: tích tử thứ hai của RHS

Nếu ta chọn tiền nghiệm đồng nhất (cho 2 mô hình xác suất ban đầu bằng nhau), thì Tỷ lệ hậu nghiệm chính là nhân tử Bayes (Bayes factor).

**_Nghịch lý Jeffreys-Lindley (Jeffreys-Lindley paradox):_** Định lý này phát biểu rằng "Nhân tử Bayes luôn thiên về mô hình đơn giản hơn, vì xác suất của dữ liệu dưới một mô hình phức tạp với một tiền nghiệm phân tán (diffuse prior) sẽ rất nhỏ".

**Lý do:** Đối với một mô hình phức tạp (có nhiều tham số tự do, linh hoạt), nó có khả năng dự đoán vô số các tập dữ liệu khác nhau. Do đó, nếu ta áp dụng một phân phối tiền nghiệm phân tán (diffuse prior - tức là tiền nghiệm không ưu tiên một giá trị cụ thể nào mà trải đều), thì xác suất phân bổ cho bất kỳ một tập dữ liệu $D$ cụ thể nào cũng sẽ trở nên rất nhỏ. Ngược lại, mô hình đơn giản chỉ dự đoán được một dải hẹp các tập dữ liệu, nên nếu dữ liệu $D$ rơi vào dải hẹp đó, xác suất khả năng biên của mô hình đơn giản sẽ cao hơn rất nhiều.

**Lưu ý:** Mặc dù nhân tử Bayes là công cụ so sánh rất tốt về mặt lý thuyết, việc tính Marginal Likelihood đòi hỏi phải tính tích phân phân phối của tham số, điều này thường là không khả thi về mặt giải tích (ngoại trừ khi dùng tiền nghiệm liên hợp - conjugate priors), do đó thường phải dùng các kỹ thuật xấp xỉ như Monte Carlo hay xấp xỉ số học.

### Further reading

Các quyết định high-level modeling (có thể coi là các siêu tham số) có ảnh hưởng quyết định đến hiệu suất của mô hình. Một số ví dụ điển hình về các lựa chọn này bao gồm:

- Hàm mục tiêu (objective function).
- Tham số chính quy hóa (regularization parameter).
- Lựa chọn các hàm cơ sở (basis functions) hoặc các tham số của nhân (kernel parameters).
- Lựa chọn phân phối tiền nghiệm (prior distribution).

Nếu chỉ tập trung vào MLE, chúng ta có thể sử dụng các phương pháp heuristic để lựa chọn mô hình nhằm ngăn chặn hiện tượng overfitting. Chúng được gọi chung là các tiêu chí thông tin (information criteria), và quy tắc là ta sẽ chọn mô hình mang lại giá trị tiêu chí lớn nhất.

- Tiêu chí thông tin Akaike (Akaike information criterion - AIC)
- Tiêu chí thông tin Bayes (Bayesian information criterion - BIC)

**Ý nghĩa:** BIC thường được sử dụng cho các phân phối thuộc họ mũ (exponential family distributions). Đặc điểm quan trọng nhất của BIC so với AIC là nó trừng phạt độ phức tạp của mô hình nặng tay hơn (do có nhân thêm logarit của kích thước tập dữ liệu $N$). Do đó, BIC có xu hướng ưu tiên chọn các mô hình đơn giản hơn so với AIC.
