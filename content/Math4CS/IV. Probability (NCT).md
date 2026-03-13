# 16. Events and Probability Spaces

## 16.3 Strange Dice

Trong cuộc sống, chúng ta quen với tính bắc cầu của các con số. Do đó ta cũng vô thức áp dụng nó với xác suất. Chúng ta nghĩ rằng nếu A "mạnh" hơn B, và B "mạnh" hơn C, thì A phải là "mạnh nhất" và C là "yếu nhất". Nhưng xác suất không hoạt động theo kiểu xếp hàng từ cao đến thấp như vậy. Để dễ hiểu nhất, hãy nghĩ về trò chơi Oẳn tù tì: Kéo thắng Bao. Bao thắng Búa. Búa thắng Kéo. Trong trò chơi này, không có cái nào là "mạnh nhất". Mỗi lựa chọn đều có một "khắc tinh" riêng.

Có một nghịch lí khác: A dễ thắng B hơn trong một lần tung, nhưng B lại dễ thắng A hơn trong hai lần tung. Khi bạn tung một con xúc xắc nhiều lần và cộng các mặt lại, bạn không chỉ đơn thuần là nhân xác suất lên, mà bạn đang tạo ra một phân phối xác suất mới. Trong 1 lần tung, A có thể thắng B. Nhưng khi tung 2 hoặc nhiều lần rồi cộng lại, sự ổn định của B bắt đầu có lợi thế. Tổng của B sẽ hội tụ về một con số trung bình ổn định, trong khi A vì có nhiều mặt thấp nên xác suất để "nổ" được 2 lần mặt cao là rất hiếm.

## 16.4 The Birthday Principle

Có 95 học sinh trong một lớp học. Xác suất để có ít nhất hai người trùng ngày sinh là bao nhiêu? So sánh 95 học sinh với 365 ngày trong năm, bạn có thể đoán xác suất nằm đâu đó khoảng $1/4$ — nhưng bạn đã nhầm: xác suất thực tế là hơn $0.9999$. Khi nghe câu hỏi "Xác suất để có người trùng ngày sinh", bộ não chúng ta thường vô thức tự đóng vai nhân vật chính. Bạn sẽ nghĩ: "Xác suất để có ai đó trùng ngày sinh với TÔI là bao nhiêu?". Nhưng vấn đề là đề bài hỏi "bất kỳ ai trùng với bất kỳ ai", chứ không phải "trùng với bạn".

> [!INFO]
> Nếu có $d$ ngày và $n \approx \sqrt{2d}$ người, xác suất trùng là khoảng 0.632 (63.2%).

Sau đây là các ứng dụng của nguyên lí trên:

- Khi bạn lưu trữ dữ liệu vào một bảng băm có kích thước $d$, mỗi mục dữ liệu được băm thành một địa chỉ. Bài toán ngày sinh cho thấy rằng: chỉ cần bạn lưu số lượng mục bằng khoảng căn bậc hai của kích thước bảng ($n \approx \sqrt{d}$), các vụ "đụng độ" (hai dữ liệu khác nhau nhảy vào cùng một chỗ) sẽ xảy ra liên tục.
- Trong mã hóa (Cryptography), các hacker sử dụng nguyên lý này để tìm "va chạm mã băm". Nếu một chữ ký số dựa trên mã băm 128-bit, hacker không cần thử $2^{128}$ lần để tìm lỗi, mà chỉ cần khoảng $\sqrt{2^{128}} = 2^{64}$ lần — một con số nhỏ hơn rất, rất nhiều.

## 16.5 Set Theory and Probability

### 16.5.3 Uniform Probability Spaces

Một không gian xác suất hữu hạn (hay không gian mẫu) $S$ được gọi là đồng nhất (uniform) nếu xác suất $\text{P}[\omega]$ là như nhau cho mọi kết quả $\omega \in S$. Tức là các biến cố sơ cấp của nó đều có cùng khả năng xảy ra. Đây cũng là dạng không gian xác suất ta gặp ở THPT, khi bài toán tính xác suất có thể quy về bài toán đếm.

### 16.5.4 Infinite Probability Spaces

Các không gian xác suất vô hạn khá phổ biến. Ví dụ, hai người chơi luân phiên tung một đồng xu công bằng. Ai tung được mặt ngửa (H) đầu tiên sẽ thắng, và quá trình tung đồng xu này là vô hạn. Biến cố 'người chơi thứ nhất thắng' chứa vô số các kết quả, nhưng chúng ta vẫn có thể tính tổng xác suất của chúng:

$$
P[\text{người 1 thắng}] = \frac{1}{2} + \frac{1}{8} + \frac{1}{32} + \frac{1}{128} + \dots = \frac{1}{2} \sum_{n=0}^{\infty} \left(\frac{1}{4}\right)^n = \frac{1}{2} \left( \frac{1}{1 - 1/4} \right) = \frac{2}{3}
$$

Để xác minh đây là một không gian xác suất, ta chỉ cần kiểm tra xem tất cả xác suất có không âm và tổng của chúng có bằng 1 hay không. Áp dụng công thức tổng cấp số nhân lùi vô hạn, ta thấy tổng đúng bằng 1.

Việc tung đồng xu ra mặt sấp mãi mãi là có thể, nhưng xác suất của nó là 0 vì khi số lần tung $n$ tiến tới vô cùng, $(1/2)^n$ tiến tới 0. Trong các không gian xác suất đếm được, các kết quả có xác suất bằng 0 không ảnh hưởng đến tính toán và thường bị bỏ qua.

# 17. Conditional Probability

## 17.4 Why Tree Diagrams Work?

### 17.4.5 Philosophy of Probability

Mục này thảo luận về một trong những chủ đề thú vị và gây tranh cãi nhất trong toán học: **Bản chất của xác suất là gì?** Ta sẽ thảo luận về 3 góc nhìn

1. Góc nhìn "Tất yếu" (Deterministic): Xác suất chỉ áp dụng cho những thứ có tính ngẫu nhiên. Ví dụ, một số cụ thể hoặc là số nguyên tố, hoặc là hợp số. Không có sự ngẫu nhiên nào ở đây cả. Gán một xác suất (ví dụ 0.5 hay 10%) cho việc một số có phải là số nguyên tố hay không là vô nghĩa. Nó giống như việc hỏi "Xác suất để $2+2=4$ là bao nhiêu?".

2. Góc nhìn Bayes (Bayesianism): Xác suất không phải là đặc tính của vật thể, mà là mức độ tin tưởng của một cá nhân dựa trên thông tin họ có. Ví dụ, nếu bạn không biết số $N$ là gì, dựa trên Định lý Số nguyên tố, bạn tin là $1/5.000.000$. Nhưng nếu bạn biết tác giả cố tình chọn một số nguyên tố để làm ví dụ, bạn có thể tin là $50/50$. Điểm mạnh là cho phép cập nhật niềm tin khi có dữ liệu mới. Điểm yếu là mang tính chủ quan, mỗi người có một mức độ tin tưởng riêng.

3. Góc nhìn Tần suất (Frequentism): Xác suất chỉ có ý nghĩa khi ta nói về một quá trình có thể lặp lại nhiều lần (như tung đồng xu). Xác suất là tỉ lệ số lần sự kiện xảy ra trên tổng số lần thử khi số lần thử tiến đến vô hạn. Một người theo trường phái tần suất sẽ không nói "Xác suất số $N$ là số nguyên tố là 99%". Thay vào đó, họ sẽ nói: "Tôi đã dùng một thuật toán kiểm tra. Thuật toán này có đặc điểm là: nếu số đó là hợp số, nó sẽ phát hiện ra với tỉ lệ 75%. Sau 1000 lần thử mà nó vẫn không bảo là hợp số, thì khả năng thuật toán này sai là cực kỳ thấp ($1/4^{1000}$)." (Chỗ này t không hiểu lắm ;v giống mấy bài tính xác suất có điều kiện hay gặp ở THPT)

> [!INFO] Simpson's Paradox
> Đừng bao giờ giả định rằng sự tương quan (correlation) giữa hai sự việc đồng nghĩa với việc cái này gây ra cái kia (causation).

## 17.8 Mutual Independence

> [!INFO]
> Một tập hợp các biến cố $A_1, A_2, \dots, A_n$ được gọi là độc lập tương hỗ (mutually independent) nếu với mọi tập con của các biến cố này, xác suất của giao các biến cố đó bằng tích các xác suất của từng biến cố riêng lẻ.

![[IV.01.png]]

### 17.8.1 Pairwise Independence

> [!INFO]
> A set A1, A2, . . . , of events is k-way independent iff every set of k of these events is mutually independent. The set is pairwise independent iff it is 2-way independent.

# 18. Random Variables

## 18.3 Distribution Functions

### 18.3.3 The Numbers Game

Bài toán: Tìm cách thắng với xác suất > 50% trong trò chơi đoán phong bì nào chứa số lớn hơn (chứa số nguyên $L, H$ phân biệt từ 0-100), khi chỉ được xem trước một phong bì.

Giải pháp: Chọn một "ngưỡng" ngẫu nhiên $x$. Nếu số trong phong bì $> x$, đoán đó là số lớn; nếu $< x$, đoán số còn lại lớn hơn.

- Nếu $x$ rơi vào giữa $L$ và $H$: Thắng 100%.
- Nếu $x$ nằm ngoài: Thắng 50%.

Do luôn có xác suất $x$ nằm giữa $L$ và $H$, tỉ lệ thắng cuối cùng sẽ là $50\% + \epsilon$ (luôn lớn hơn 50%).

## 18.4 Great Expectations

### 18.4.6 Mean Time to Failure

Bài toán: Tính thời gian (số giờ) trung bình (kỳ vọng) cho đến khi một hệ thống gặp sự cố, biết rằng tại mỗi giờ, hệ thống có xác suất hỏng cố định là $p$.

Sau 1 giờ đầu tiên, có hai kịch bản:

- Sập luôn (Xác suất $p$): Bạn mất đúng 1 giờ.
- Không sập (Xác suất $1-p$): Bạn đã tiêu tốn 1 giờ, nhưng vì xác suất sập ở mỗi giờ là như nhau, nên tại thời điểm này, chương trình của bạn "như mới". Thời gian bạn cần chờ tiếp theo tính từ lúc này chính bằng thời gian kỳ vọng ban đầu ($Ex[C]$). Vậy tổng thời gian là $1 + Ex[C]$.

Phép toán $Ex[C] = p(1) + (1-p)(1 + Ex[C])$ thực chất là việc gom tất cả các khả năng vô hạn (sập ở giờ thứ 1, thứ 2, thứ 3... đến vô tận) vào một công thức đệ quy duy nhất. Kết quả cuối cùng là $Ex[C] = 1/p$.

> [!INFO]
> Nếu một sự cố có xác suất xảy ra là $p$ mỗi giờ, thì trung bình bạn sẽ phải đợi $1/p$ giờ để thấy nó xảy ra.

Đây còn được gọi là Geometric Distribution.

### 18.4.7 Expected Returns in Gambling Games

Bài toán: Phân tích lý do một trò chơi cá cược có vẻ công bằng ($Ex=0$) lại khiến người chơi thua lỗ nặng nề trong thực tế.

Tóm lược giải pháp: Sự sai lệch nằm ở giả định về tính độc lập của các lựa chọn. Khi hai đối thủ cấu kết để luôn đưa ra các dự đoán trái ngược nhau, họ đã triệt tiêu kịch bản "người chơi thắng trọn giải thưởng" và đảm bảo rằng luôn có ít nhất một người trong nhóm của họ được chia phần. Sự thay đổi trong cấu trúc xác suất này biến một trò chơi hòa vốn thành một trò chơi có kỳ vọng âm ($-0.5\$$ mỗi ván). Do đó người chơi còn lại bị lỗ.

Bài toán: Làm thế nào để có lợi nhuận dương trong một trò chơi xổ số mà nhà cái đã lấy mất 50% tiền cược?

Tóm lược giải pháp: Giáo sư Chernoff nhận ra rằng tâm lý đám đông khiến nhiều người chọn trùng các dãy số giống nhau (như ngày tháng), dẫn đến việc giải thưởng bị chia nhỏ khi trúng. Bằng cách áp dụng Phân phối đều (Uniform Distribution) để chọn những dãy số mà con người ít khi nghĩ tới, Chernoff đảm bảo rằng nếu ông thắng, ông sẽ không phải chia sẻ giải thưởng với ai. Điều này làm thay đổi giá trị kỳ vọng từ lỗ 50% thành lãi 7%, biến một trò chơi may rủi thành một cơ hội đầu tư có lãi dựa trên việc khai thác sai lầm trong hành vi của đám đông.

## 18.5 Linearity of Expectation

Thông thường trong xác suất, hầu hết các phép toán đều trở nên cực kỳ rắc rối nếu các biến phụ thuộc lẫn nhau. Nhưng với Kỳ vọng (Expectation), công thức sau luôn luôn đúng:

$$
Ex[X_1 + X_2 + \dots + X_n] = Ex[X_1] + Ex[X_2] + \dots + Ex[X_n]
$$

Dù cho $X_1$ có ảnh hưởng đến $X_2$, hay chúng có mối quan hệ lắt léo đến thế nào, bạn chỉ cần tính kỳ vọng của từng cái rồi cộng lại là xong.

### 18.5.2 Sums of Indicator Random Variables

![[IV.02.png]]

Để chứng minh định lý này, các nhà toán học dùng một thủ thuật:

1. Đặt $X_i$ là biến chỉ thị cho biến cố $A_i$ ($X_i=1$ nếu $A_i$ xảy ra, ngược lại $X_i=0$).
2. Tổng số biến cố xảy ra chính là $X = X_1 + X_2 + \dots + X_n$.
3. Theo tính chất tuyến tính của kỳ vọng: $$Ex[X] = Ex[X_1] + Ex[X_2] + \dots + Ex[X_n]$$
4. Mà ta đã biết $Ex[X_i] = Pr[A_i]$. Vậy nên $Ex[X] = \sum Pr[A_i]$.

### 18.5.4 The Coupon Collector Problem

Bài toán: Tính số lần thử trung bình (kỳ vọng) để thu thập đủ $n$ loại vật phẩm khác nhau khi mỗi lần thử cho ra một kết quả ngẫu nhiên đồng nhất.

Bí quyết để giải bài toán này không phải là nhìn vào toàn bộ quá trình thu thập, mà là chia nó thành các giai đoạn (stages) dựa trên số lượng sản phẩm bạn đang sở hữu:

1. Giai đoạn $X_k$: Là số bữa ăn bạn phải mua để có thêm được chiếc xe mới thứ $k+1$, khi bạn đã có sẵn $k$ loại xe khác nhau.
2. Xác suất thành công: Khi đã có $k$ loại, xác suất để lần mua tới trúng một loại xe mới là $p = \frac{n-k}{n}$ (vì còn $n-k$ loại bạn chưa có).
3. Kỳ vọng của mỗi giai đoạn: Theo quy tắc "Thời gian trung bình đến khi hỏng" ($1/p$) mà bạn đã học ở phần trước, số bữa ăn trung bình cần ở giai đoạn này là $Ex[X_k] = \frac{n}{n-k}$.
4. Tổng hợp: Nhờ tính tuyến tính, ta chỉ cần cộng kỳ vọng của tất cả các giai đoạn lại.

### 18.5.6 A Gambling Paradox

Bài toán: Trong trò Roulette, do có các ô màu xanh, xác suất thắng cược (Đỏ/Đen) luôn nhỏ hơn $1/2$, dẫn đến giá trị kỳ vọng ($Ex$) của mỗi ván cược luôn là một số âm (người chơi lỗ).

Giải pháp ban đầu: Người chơi sử dụng chiến thuật Martingale – gấp đôi mức cược sau mỗi lần thua. Lý thuyết cho rằng vì sớm muộn gì bạn cũng sẽ thắng một ván, nên bạn chắc chắn sẽ thu về lợi nhuận ròng (ví dụ $10$). Điều này tạo ra một kỳ vọng dương ($Ex = +10$), trái ngược với bản chất của trò chơi.

Nghịch lý và Sự thật: Nghịch lý xuất hiện do việc **áp dụng sai tính tuyến tính của kỳ vọng cho một chuỗi vô hạn mà không thỏa mãn điều kiện hội tụ tuyệt đối** (vì mức cược tăng quá nhanh theo cấp số nhân). Thực tế, chiến thuật này chỉ thành công nếu bạn có nguồn vốn vô hạn. Với nguồn vốn hữu hạn và giới hạn bàn chơi, bạn sẽ đối mặt với rủi ro phá sản cực lớn chỉ để đổi lấy một khoản thắng nhỏ nhoi.

# 19. Deviation from the Mean

## 19.1 Markov’s Theorem

Định lý Markov đưa ra một ước lượng nhìn chung là 'thô' về xác suất một biến ngẫu nhiên nhận giá trị lớn hơn nhiều so với giá trị trung bình của nó.

![[IV.03.png]]

**Tại sao lại gọi là "Ước lượng thô" (Coarse estimate)?**

Ý tưởng đằng sau Định lý Markov có thể được giải thích bằng cách xem xét chỉ số thông minh (IQ). IQ được thiết kế để phép đo trung bình là 100. Điều này ngay lập tức ngụ ý rằng tối đa $1/3$ dân số có thể có IQ từ 300 trở lên, bởi vì nếu hơn một phần ba dân số có IQ 300, thì điểm trung bình sẽ phải lớn hơn $1/3 \times 300 = 100$. Vì vậy, xác suất để một người được chọn ngẫu nhiên có IQ từ 300 trở lên tối đa là $1/3$.

Cùng một logic đó, định lý Markov bảo: Tối đa 66.6% dân số có IQ trên 150. Nhưng thực tế chỉ có khoảng 0.1% dân số có IQ trên 150. Con số 66.6% "thô" đến mức gần như vô dụng trong đời sống hàng ngày. Tuy nhiên, nó lại cực kỳ giá trị trong toán học và lập trình vì nó luôn đúng cho mọi loại phân phối, miễn là biến số đó không âm.

Ta hiểu định lí Markov cho ta một chặn trên, nhưng không quá chặt.

### 19.1.2 Markov’s Theorem for Bounded Variables

Định lý Markov gốc yêu cầu biến số phải không âm ($X \ge 0$). Nhưng trong thực tế, nhiều biến số có một "sàn" (cận dưới) cao hơn 0 rất nhiều. Nếu bạn biết chắc chắn $R$ không bao giờ nhỏ hơn $b$, bạn có thể tạo ra một biến mới: $T = R - b$.

- Vì $R \ge b$ nên $T \ge 0$ $\rightarrow$ Thỏa mãn điều kiện của Markov.
- Kỳ vọng của biến mới là: $Ex[T] = Ex[R] - b$.
- Kết quả: Ngưỡng chặn mới sẽ "chặt" hơn (nhỏ hơn), giúp bạn có một ước lượng chính xác hơn về các giá trị cực lớn.

![[IV.04.png]]

## 19.2 Chebyshev’s Theorem

Đoạn văn bắt đầu bằng một mẹo cực kỳ thông minh: Thay vì áp dụng Markov trực tiếp cho biến $R$, hãy áp dụng nó cho $|R|^z$. Vì $|R|^z$ luôn không âm với mọi số thực $z$, thỏa mãn điều kiện tiên quyết của Markov. Mặt khác, $[|R|^z \ge x^z]$ tương đương với $[|R| \ge x]

**Tại sao $[|R|^z \ge x^z]$ lại tương đương với $[|R| \ge x]$?**

Với $x > 0$ và $z > 0$, hàm số $f(t) = t^z$ là một hàm số luôn tăng khi $t \ge 0$. Vì $|R|$ và $x$ đều là các số không âm, nên nếu $|R|$ lớn hơn $x$, thì chắc chắn $|R|^z$ cũng sẽ lớn hơn $x^z$, và ngược lại. Hai sự kiện này là một, chúng xảy ra cùng lúc và có cùng xác suất.

Từ đó ta có bổ đề sau:

![[IV.05.png]]

Khi ta chọn $z = 2$ trong công thức trên, chúng ta có một đại lượng quan trọng nhất nhì trong thống kê: Phương sai ($\text{Var}[R]$). Định nghĩa: $\text{Var}[R] = Ex[(R - Ex[R])^2]$

Sử dụng Phương sai, Định lý Chebyshev cho ta một ngưỡng chặn cực kỳ mạnh mẽ:

$$
Pr[|R - Ex[R]| \geq x] \leq \frac{\text{Var}[R]}{x^2}
$$

Nghĩa là: Xác suất để một giá trị nằm cách xa trung bình một khoảng $x$ sẽ tỉ lệ nghịch với bình phương của $x$. Nếu Phương sai nhỏ (dữ liệu tập trung), xác suất "văng xa" sẽ cực kỳ thấp.

### 19.2.1 Variance in Two Gambling Games

Chúng ta có hai trò chơi với cùng kỳ vọng là $1$ nhưng khác phương sai ($2$ và $2,004,002$). Sau 10 ván chơi A, bạn kỳ vọng lãi $10$ USD. Trường hợp đen đủi nhất, bạn chỉ mất khoảng $10$ USD. Sau 10 ván chơi B, bạn cũng kỳ vọng lãi $10$ USD. Nhưng nếu rơi vào chuỗi đen đủi (phần đuôi của phân phối), bạn có thể bay sạch hơn $20,000$ USD! (vì phương sai lớn).

Phương sai chính là thước đo của độ bất định. Cùng một mức lợi nhuận trung bình, nhưng hệ thống nào có phương sai cao hơn thì hệ thống đó "nguy hiểm" hơn. Điều này chứng minh rằng Giá trị kỳ vọng chỉ cho thấy cái nhìn dài hạn, còn Phương sai mới là thứ phản ánh rủi ro ngắn hạn và mức độ sai lệch thực tế.

### 19.2.2 Standard Deviation

Đoạn văn đưa ra một hệ quả cực kỳ quan trọng (Corollary 19.2.6). Nếu chúng ta đặt khoảng cách $x$ bằng $c$ lần độ lệch chuẩn ($x = c\sigma_R$), ta có:

$$Pr(|R - Ex[R]| \geq c\sigma_R) \leq \frac{1}{c^2}$$

Nó cho bạn biết xác suất dữ liệu "văng" ra ngoài phạm vi $c$ bước chân (mỗi bước dài $\sigma$):

- Nếu đi xa 2 bước ($\sigma$): Xác suất nằm ngoài vùng này tối đa là $1/2^2 = 25\%$.
- Nếu đi xa 3 bước ($\sigma$): Xác suất nằm ngoài vùng này tối đa là $1/3^2 \approx 11\%$.

Điều này khẳng định rằng: Dữ liệu hầu như luôn "túm tụm" lại trong một vùng có kích thước tỉ lệ với $\sigma$ quanh giá trị trung bình. $\sigma$ càng nhỏ, dữ liệu càng tập trung; $\sigma$ càng lớn, dữ liệu càng loãng.

![[IV.06.png]]

## 19.3 Properties of Variance
