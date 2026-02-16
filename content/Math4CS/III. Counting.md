# 13. Sums and Asymptotics

Closed Form là một biểu thức toán học có thể tính toán được bằng một số lượng hữu hạn các phép tính cơ bản (như cộng, trừ, nhân, chia, lũy thừa). Nó không chứa các dấu ba chấm ($\dots$), không chứa ký hiệu tổng $\sum$ hay tích $\prod$ phụ thuộc vào một biến số chạy.

Ví dụ: Thay vì viết tổng cấp số nhân là $1 + x + x^2 + \dots + x^n$, ta viết dạng đóng của nó là $\frac{1-x^{n+1}}{1-x}$.

Closed Form giúp tính toán nhanh hơn, dễ dàng phân tích xu hướng (khi n tăng thì biểu thức tăng như nào), tính giới hạn. Trong các phần sau ta sẽ tập trung vào việc tìm công thức dạng đóng của một biểu thức.

## 13.1 The Value of an Annuity

Niên kim (annuity) là một loại công cụ tài chính mà bạn sẽ nhận được (hoặc phải trả) một số tiền cố định ($m$) vào đầu mỗi năm, kéo dài trong một số năm nhất định ($n$). Ví dụ: Tiền trúng độc đắc trả góp, tiền trả góp mua nhà (mortgage), hay các khoản vay sinh viên.

**Bối cảnh bài toán**: 1 triệu USD nhận ngay bây giờ VS 50k USD/năm

- **Kịch bản rõ ràng**: 1 triệu đô ngay lập tức vs. 50.000 đô/năm trong 20 năm (tổng cũng là 1 triệu đô). Ở đây, nhận 1 triệu đô ngay lập tức luôn tốt hơn vì bạn có toàn bộ tiền để đầu tư ngay.
- **Kịch bản khó khăn**: 500.000 đô ngay lập tức vs. 50.000 đô/năm trong 20 năm (tổng là 1 triệu đô). Lúc này, sự lựa chọn không còn dễ dàng vì bạn phải tính toán xem lãi suất đầu tư có đủ bù đắp cho việc nhận tiền chậm hay không.

Điểm mấu chốt của bài toán là **xác định giá trị hiện tại (Present Value)** của một dòng tiền trong tương lai.

### 13.1.1 The Future Value of Money

> [!INFO] Gọi $p$ là lãi suất
> **Giá trị tương lai (Future Value):** Nếu bạn có 10 USD hôm nay, sau 1 năm bạn sẽ có $10 \times (1+p)$. Sau 2 năm là $10 \times (1+p)^2$. Tương tự cho $n$ năm.
>
> **Giá trị hiện tại (Present Value):** Ngược lại, để có 10 USD vào năm sau, hôm nay bạn chỉ cần bỏ ra một khoản ít hơn là $10 / (1+p)$. Đây chính là giá trị của "10 USD tương lai" quy đổi về thời điểm hiện tại.

Một niên kim trả $m$ đô mỗi năm, kéo dài trong $n$ năm sẽ có tổng giá trị hiện tại được tính bằng cách cộng tất cả các khoản thanh toán đã được "chiết khấu":

- Khoản 1 (ngay bây giờ): Đáng giá $m$.
- Khoản 2 (sau 1 năm): Đáng giá $m / (1+p)$.
- Khoản $n$ (sau $n-1$ năm): Đáng giá $m / (1+p)^{n-1}$.

Tổng giá trị $V$ là:

$$V = m + \frac{m}{1+p} + \frac{m}{(1+p)^2} + \dots + \frac{m}{(1+p)^{n-1}}$$

Nếu ta đặt $x = 1/(1+p)$, biểu thức trên trở thành một tổng cấp số nhân quen thuộc:

$$V = m(1 + x + x^2 + \dots + x^{n-1})$$

Nó là một hằng đẳng thức quen thuộc. Còn một cách khác nữa để tính mà đa số mọi người quên, mình sẽ nhắc lại.

### 13.1.2 The Perturbation Method

Giả sử chúng ta có tổng $S$: $$S = 1 + x + x^2 + x^3 + \dots + x^n$$

Ta nhân cả hai vế của $S$ với $x$. $$xS = x + x^2 + x^3 + \dots + x^n + x^{n+1}$$

Khi lấy $S - xS$, ta được $$S - xS = 1 - x^{n+1}$$

Chuyển vế suy ra: $$ S = \frac{1 - x^{n+1}}{1 - x}$$

Đây là kết quả ;v quá đơn giản...

### 13.1.3 A Closed Form for the Annuity Value

Có công thức rồi thì ta thế vô và so sánh xem nên chọn phương án nào. Nhắc lại, đây là giá trị hiện tại của annuity.

Khi quảng cáo nói rằng bạn trúng 1 triệu đô, nhưng thực tế họ trả bạn 50.000 đô mỗi năm trong 20 năm. Thế vào công thức đã tính thì $V \approx 530.180$ USD. Vì các khoản thanh toán bị trì hoãn (deferred), giá trị thực sự của giải thưởng này ở thời điểm hiện tại chỉ hơn một nửa so với con số 1 triệu đô được quảng cáo.

=> Các nhà quảng cáo xổ số sử dụng sự thiếu hiểu biết về **giá trị thời gian của tiền bạc** để làm cho giải thưởng trông có vẻ hấp dẫn gấp đôi giá trị thực của nó. Trong tài chính, việc sở hữu tiền ngay lập tức luôn có lợi thế vượt trội so với việc nhận cùng số tiền đó nhưng chia nhỏ ra nhiều năm.

### 13.1.4 Infinite Geometric Series

Nếu nhận 50k USD/năm, mãi mãi thì sao? Nghe có vẻ như vô hạn tiền, nhưng thật ra không phải (áp dụng tính lim nào).

> [!INFO]
> Nếu $|x| < 1$, thì tổng của dãy số vô hạn $1 + x + x^2 + \dots$ sẽ hội tụ về một con số cụ thể:$$\sum_{i=0}^{\infty} x^i = \frac{1}{1-x}$$

Cái này thì dễ chứng minh rồi. Khi cho n chạy đến vô cùng, ta có $V = m \times \frac{1+p}{p}$

Thay các con số vào thì $V = 50.000 \times \frac{1,08}{0,08} = \mathbf{675.000}$.

**Tại sao 1 triệu đô hôm nay lại thắng "vô hạn tiền" tương lai?**

Con số 675.000 đô thấp hơn nhiều so với 1 triệu đô. Để hiểu tại sao điều này hợp lý, hãy nhìn ngược lại:

- Nếu bạn có 1.000.000 đô trong ngân hàng với lãi suất 8%.
- Mỗi năm, tiền lãi sinh ra là: $1.000.000 \times 0,08 = \mathbf{80.000}$.
- Bạn có thể rút 80.000 đô này ra tiêu xài mãi mãi mà không bao giờ chạm vào số tiền gốc 1 triệu đô ban đầu.

Vậy ngoài số tiền 1tr USD, ta còn có 80k USD/năm, vậy là lợi hơn nhiều 50k USD/năm. Đương nhiên, có chuyện này là vì có lãi suất $p$ hàng năm, đây là bài toán khá thực tế.

### 13.1.6 Variations of Geometric Sums

Đôi khi bạn gặp một tổng mà các số hạng của nó là sự kết hợp giữa cấp số cộng và cấp số nhân, ví dụ: $$\sum_{i=1}^{n-1} i x^i = 1x^1 + 2x^2 + 3x^3 + \dots + (n-1)x^{n-1}$$

Ở đây, số hạng $i$ tăng dần theo kiểu cộng, còn $x^i$ tăng dần theo kiểu nhân. Tỷ số giữa các số hạng không cố định, nên ta không thể dùng công thức cấp số nhân thông thường.

Chắc bạn nghĩ ra rồi. **Ý tưởng**: Đạo hàm của $x^i$ chính là $i \cdot x^{i-1}$. Điều này cho phép chúng ta "lôi" chỉ số $i$ từ trên số mũ xuống làm hệ số.

Các bước thực hiện:

1. Bắt đầu từ công thức cấp số nhân đã biết:$$\sum_{i=0}^{n-1} x^i = \frac{1-x^n}{1-x}$$
2. Đạo hàm cả hai vế theo $x$:

- Vế trái trở thành: $\sum i x^{i-1}$.
- Vế phải được tính bằng quy tắc đạo hàm phân thức $\left(\frac{u}{v}\right)'$.

3. Điều chỉnh số mũ: Sau khi đạo hàm, ta có tổng của $i x^{i-1}$. Để đưa về dạng $i x^i$ như ban đầu, ta chỉ cần nhân thêm $x$ vào cả hai vế.

![[III.01.png]]

Khi một tổng có cấu trúc phức tạp nhưng gợi nhớ đến một công thức cơ bản, ta có thể sử dụng các phép toán giải tích (đạo hàm hoặc nguyên hàm) để biến đổi công thức đã biết thành công thức mới. Nếu thấy $i$ xuất hiện làm hệ số ($i x^i$), hãy nghĩ đến Đạo hàm. Nếu thấy $i$ nằm ở mẫu số ($x^i / i$), hãy nghĩ đến Nguyên hàm.

Nếu $|x| < 1$, khi cho số hạng $n$ tiến đến vô cùng: $$\sum_{i=1}^{\infty} i x^i = \frac{x}{(1-x)^2}$$

Giả sử bạn có một khoản đầu tư mà mỗi năm số tiền nhận được tăng thêm $m$ đô la:

- Năm 1: Nhận $1m$
- Năm 2: Nhận $2m$
- Năm 3: Nhận $3m$
- Năm n: Nhận $nm$

Cứ thế, mãi mãi. Nghe có vẻ vô hạn tiền, nhưng: $$V = \frac{m}{(1+p)^1} + \frac{2m}{(1+p)^2} + \frac{3m}{(1+p)^3} + \dots$$

Sử dụng định lí trên với $x = \frac{1}{1+p}$, ta tính được dạng đóng: $$V = m \cdot \frac{1+p}{p^2}$$

Ta thấy rằng với sự xuất hiện của lãi suất $p$, thì số tiền nhận được lại dồn về một con số hữu hạn. Bởi vì tăng trưởng số tiền ở đây tăng theo cấp số cộng, còn sự sụt giảm theo lãi suất lại tăng theo cấp số nhân. Giá trị của đồng tiền trong tương lai xa bị bào mòn bởi lãi suất nhanh đến mức sự tăng thêm của số tiền không đủ để bù đắp.

## 13.2 Sums of Powers

Phần này giới thiệu về một phương pháp...đoán hệ số. Khi bạn tính tổng của một dãy số mà mỗi số hạng là một đa thức bậc $k$, thì kết quả thường sẽ là một đa thức bậc $k+1$.

Ví dụ: Tổng của $i^2$ (bậc 2) nên kết quả dự đoán sẽ là một đa thức bậc 3 có dạng $$S_n = an^3 + bn^2 + cn + d$$

Vậy để tìm ra closed form của công thức trên ta đi tìm hệ số a, b, c, d bằng cách thay các $n$ vào, tạo thành hệ phương trình.

Phương pháp này rất nhanh, nhưng nó có thể sai, và công thức tìm được sau cùng thường phải được chứng minh lại dựa trên quy nạp, thì mới khẳng định nó đúng với mọi $n$ được.

## 13.3 Approximating Sums

Lỡ như khó quá thì sao, không đoán được cũng không tính toán tường minh được. Thì ta buộc phải xấp xỉ. Sau đây giới thiệu phương pháp xấp xỉ bằng tích phân (nghe quen ha, đó giờ có xấp xỉ diện tích một hình bằng tích phân rồi đó). Thay vì tìm một con số chính xác, ta sẽ tìm một khoảng giá trị [Thấp, Cao] mà tổng $S$ chắc chắn nằm trong đó.

![[III.02.png]]

Nhắc lại khái niệm hàm tăng, tăng ngặt, giảm, giảm ngặt. Phương pháp này áp dụng được miễn là hàm đó đơn điệu. Chứng minh xem trong sách nha, lười note quá ;v

## 13.4 Hanging Out Over the Edge

### 13.4.1 Formalizing the Problem

Phần này giới thiệu bài toán chồng sách, nghiêng ra khỏi mặt bàn sao cho sách không rơi (bài toán quen thuộc). Để một chồng sách không bị đổ, nguyên tắc vật lý cơ bản là: **Trọng tâm của tất cả các cuốn sách phía trên phải nằm trên diện tích tiếp xúc của cuốn sách ngay bên dưới nó.**

![[III.03.png]]

Giả sử ta đã có một chồng $n$ cuốn sách ổn định với độ nhô tối đa là $B_n$. Bây giờ ta đặt chồng này lên trên cuốn sách thứ $n+1$. Để cả hệ thống mới ($n+1$ cuốn) đạt độ nhô tối đa $B_{n+1}$:

- Ta đặt trọng tâm của $n$ cuốn phía trên ngay sát mép của cuốn thứ $n+1$.
- Lúc này, độ nhô mới $B_{n+1}$ sẽ bằng: (Khoảng cách từ trọng tâm hệ $n$ cuốn đến mép cuốn $n+1$) + (Khoảng cách mà cuốn $n+1$ nhô ra so với bàn).

Theo công thức tính trọng tâm vật lý, khi thêm 1 cuốn sách vào dưới cùng, trọng tâm của cả hệ thống sẽ dịch chuyển một khoảng là: $$\Delta = \frac{1}{2(n+1)}$$.

Do đó ta có công thức truy hồi: $$B_{n+1} = B_n + \frac{1}{2(n+1)}$$.

Công thức tổng quát là: $B_n = \frac{1}{2} \sum_{i=1}^{n} \frac{1}{i}$.

Trong đó, biểu thức $\sum_{i=1}^{n} \frac{1}{i}$ chính là Số Harmonic thứ $n$ ($H_n$).

### 13.4.2 Harmonic Numbers

Không có closed form đơn giản cho $H_n$, do đó ta phải xấp xỉ. Ta có: $\ln(n) + \frac{1}{n} \le H_n \le \ln(n) + 1$.

Mặt khác, các nhà toán học đã tìm ra một công thức xấp xỉ cực kỳ chính xác cho $H_n$: $$H_n \approx \ln(n) + \gamma + \frac{1}{2n}$$

Trong đó $\gamma \approx 0.577215...$ được gọi là Hằng số Euler-Mascheroni. Công thức này cho thấy $H_n$ và $\ln(n)$ thực chất "tăng trưởng" cùng tốc độ, chúng chỉ lệch nhau một hằng số nhỏ.

Vậy, $$B_n \approx \frac{\ln(n)}{2}$$.

Mặc dù hàm $\ln(n)$ sẽ tiến đến vô cùng khi $n \to \infty$ (nghĩa là bạn có thể nhô ra bao xa tùy thích), nhưng tốc độ tăng trưởng của nó cực kỳ chậm.

**Extending Further Past the End of the Table**

Chúng ta mặc định rằng cuốn sách trên cùng phải là cuốn nhô ra xa nhất. Tuy nhiên, với 2 cuốn sách, bạn cũng có thể xếp sao cho cuốn dưới nhô ra xa hơn cuốn trên, nhưng tổng độ nhô so với mép bàn vẫn đạt mức tối đa là $3/4$ (tương đương $B_2 = 1/2 + 1/4$).

![[III.04.png]]

Bạn có thể lấy một chồng $n$ cuốn đang xếp kiểu tối ưu, rồi chỉ việc tráo đổi 2 cuốn trên cùng theo cách mới. Lúc này, cuốn thứ 2 từ trên xuống sẽ là cuốn vươn xa nhất, nhưng tổng độ nhô của cả chồng sách so với mép bàn vẫn không đổi.

Nếu bạn chỉ xếp theo kiểu "một cuốn đè lên một cuốn" (đơn cột), thì con số $\frac{H_n}{2}$ là giới hạn tuyệt đối. Toán học chứng minh rằng chỉ tồn tại đúng 2 kiểu sắp xếp để chạm được mốc tối đa này (như đã phân tích). Nếu ta mở rộng không gian thiết kế sang cấu trúc đa luồng (kim tự tháp ngược), giới hạn toán học sẽ được đẩy lên một tầm cao mới ($\sqrt[3]{n}$). Đây là một minh chứng tuyệt vời cho việc tối ưu hóa cấu trúc trong kỹ thuật và xây dựng.

### 13.4.3 Asymptotic Equality

Ai học qua giải tích ở đại học thì chắc gặp kí hiệu này rồi.

![[III.05.png]]

Ý nghĩa: Khi $x$ cực lớn, giá trị của $f(x)$ và $g(x)$ gần như bằng nhau. Các sai số hoặc các số hạng bậc thấp trở nên không đáng kể so với giá trị khổng lồ của số hạng dẫn đầu.

Theo định nghĩa, $H_n \sim \ln(n) + C$ với bất kỳ hằng số $C$ nào cũng đều đúng. Tại sao? Vì khi $n \to \infty$, thì $\frac{\ln(n) + C}{\ln(n)}$ luôn tiến về $1$. Hằng số $C$ trở nên quá nhỏ so với sự tăng trưởng của $\ln(n)$.

Nếu bạn muốn khẳng định hằng số Euler $\gamma$ là số hạng quan trọng thứ hai, bạn phải viết: $$(H_n - \ln(n)) \sim \gamma$$ (Nghĩa là sau khi loại bỏ số hạng dẫn đầu, phần còn lại sẽ tương đương tiệm cận với $\gamma$).

## 13.5 Products

Ta không cần xây dựng thêm phương pháp tìm closed form cho tích, vì có thể chuyển một tích sang tổng bằng logarit. Sau khi tìm closed form ở dạng tổng rồi thì ta mũ ngược lại về biểu thức ban đầu.

![[III.06.png]]

### 13.5.1 Stirling’s Formula

![[III.07.png]]

![[III.08.png]]

Ba đặc điểm quan trọng cần lưu ý:

- Vì sai số $\epsilon(n)$ luôn dương, nên giá trị thực của $n!$ luôn lớn hơn biểu thức xấp xỉ cơ bản.
- Khi $n$ tiến đến vô cùng, tỷ lệ giữa $n!$ và công thức này tiến về 1 ($n! \sim \dots$). Đây là một điều kỳ diệu vì giai thừa (một khái niệm rời rạc) lại liên quan mật thiết đến các hằng số liên tục ($\pi, e$).
- Ngay cả với $n$ nhỏ, công thức này đã rất chính xác.

## 13.6 Double Trouble

Để tính tổng của một tổng thì, tính bên trong trước (thế closed form trước), rồi tính tổng bên ngoài

![[III.09.png]]

Nếu tổng bên trong không có closed form, thì ta **đảo thứ tự lấy tổng**. Ví dụ, tổng của $n$ số Harmonic đầu tiên được viết là:

$$\sum_{k=1}^{n} H_k = \sum_{k=1}^{n} \sum_{j=1}^{k} \frac{1}{j}$$

Hãy tưởng tượng các cặp $(k, j)$ này trên một cái bảng. Cột là $j$, dòng là $k$:

- Khi $k=1$: $j$ chạy từ 1 đến 1 $\rightarrow$ ta có ô $(1, 1)$.
- Khi $k=2$: $j$ chạy từ 1 đến 2 $\rightarrow$ ta có ô $(2, 1), (2, 2)$.
- Khi $k=3$: $j$ chạy từ 1 đến 3 $\rightarrow$ ta có ô $(3, 1), (3, 2), (3, 3)$.

Các cặp này tạo thành một hình tam giác. Cách tính ban đầu là cộng theo từng hàng rồi mới cộng tổng các hàng lại. Thay vì tính theo hàng, ta sẽ tính theo từng cột $j$ trước:

- Giá trị nhỏ nhất của $j$ là 1.
- Giá trị lớn nhất của $j$ là $n$.
- Với một cột $j$ cố định, các giá trị của $k$ sẽ bắt đầu từ đâu? Nhìn vào bảng, ta thấy $k$ luôn lớn hơn hoặc bằng $j$. Vậy $k$ chạy từ $j$ đến $n$.

Lúc này, biểu thức được viết lại thành:

$$\sum_{j=1}^{n} \sum_{k=j}^{n} \frac{1}{j}$$

![[III.10.png]]

Bây giờ việc tính toán trở nên dễ dàng hơn nhiều vì số hạng $\frac{1}{j}$ không phụ thuộc vào biến $k$ của tổng bên trong. Ta đưa $\frac{1}{j}$ ra ngoài tổng trong, sau đó tính tổng bên trong là $\sum_{k=j}^{n} 1$ đơn giản là đếm xem có bao nhiêu số từ $j$ đến $n$. Số lượng đó là: $(n - j + 1)$.

![[III.11.png]]

## 13.7 Asymptotic Notation (Kí hiệu tiệm cận)

Kí hiệu tiệm cận dùng để thể hiện hành vi của một hàm số $f(n)$ khi $n$ trở nên lớn. Ví dụ, kí hiệu tiệm cận $\sim$ là một quan hệ nhị phân chỉ ra rằng hai hàm số tăng trưởng với tốc độ như nhau. Còn có các kí hiệu khác sẽ được giới thiệu.

### 13.7.1 Little O

![[III.12.png]]

Khi $n$ đủ lớn, $f$ trở nên không đáng kể so với $g$.

Một số bổ đề quen thuộc:

- $x^a = o(x^b)$ với mọi hằng số không âm $a < b$
- $\log x = o(x^\epsilon)$ với mọi $\epsilon > 0$ (vì $\log x < x$ với mọi $x > 1$)
- $x^b = o(a^x)$ với bất kỳ $a, b \in \mathbb{R}$ thỏa mãn $a > 1$

### 13.7.2 Big O

Big O là ký hiệu tiệm cận được sử dụng thường xuyên nhất. Nó được dùng để đưa ra một chặn trên (upper bound) về sự tăng trưởng của một hàm số, chẳng hạn như thời gian chạy của một thuật toán. Có một định nghĩa chuẩn về Big O, nhưng chúng ta sẽ bắt đầu với một định nghĩa thay thế giúp làm rõ vài tính chất cơ bản của nó.

![[III.13.png]]

Ta sử dụng khái niệm giới hạn trên (limit superior - lim sup) thay vì chỉ dùng giới hạn (limit). Giới hạn thông thường và giới hạn trên là như nhau **khi giới hạn đó tồn tại**, và ta cần dùng giới hạn trên cho các trường hợp **không tính được giới hạn**.

Một số bổ đề:

- Nếu $f = o(g)$ hoặc $f \sim g$, thì $f = O(g)$ (điều ngược lại thì không đúng)
- Nếu $f = o(g)$, thì không thể có chuyện $g = O(f)$

Một cách diễn đạt khác tương đương và phổ biến hơn của Big O mà không đề cập đến lim sup là

![[III.14.png]]

Định nghĩa này nhìn có vẻ khá phức tạp, nhưng ý tưởng lại rất đơn giản: $f(x) = O(g(x))$ có nghĩa là $f(x)$ nhỏ hơn hoặc bằng $g(x)$ khi $x$ đủ lớn.

Big O đặc biệt hữu ích khi mô tả thời gian chạy của một thuật toán, cho phép chúng ta thảo luận về tốc độ của thuật toán mà không cần bận tâm đến các hệ số hằng số hay các số hạng bậc thấp (vốn có thể thay đổi tùy theo từng loại máy tính).

### 13.7.3 Theta

Giúp chúng ta xác định chính xác tốc độ tăng trưởng của một hàm số bằng cách "kẹp" nó ở cả hai đầu (trên và dưới). $\Theta$ mạnh hơn $O$ lớn rất nhiều:

- $O(g)$: Giống như dấu $\le$ (chặn trên). Nếu thuật toán của bạn chạy $O(n^2)$, nó có thể chạy cực nhanh như $O(n)$ cũng được, vì $n$ vẫn nằm dưới $n^2$.
- $\Theta(g)$: Giống như dấu $\approx$ (xấp xỉ chính xác). Nếu thuật toán là $\Theta(n^2)$, nó chắc chắn tăng trưởng theo bậc bình phương. Nó không thể nhanh hơn như $n$ và cũng không thể chậm hơn như $n^3$.

![[III.15.png]]

Theta làm nổi bật tốc độ tăng trưởng và triệt tiêu các hệ số gây nhiễu cũng như các số hạng bậc thấp. Ví dụ, chỉ cần biết thời gian chạy của một thuật toán là $\Theta(n^3)$ đã là rất hữu ích, bởi vì nếu $n$ tăng gấp đôi, chúng ta có thể dự đoán rằng thời gian chạy nhìn chung sẽ tăng lên tối đa là 8 lần đối với $n$ đủ lớn. Theo cách này, Theta bảo tồn thông tin về khả năng mở rộng (scalability) của một thuật toán hoặc hệ thống.

### 13.7.4 Pitfalls with Asymptotic Notation

Một số sai lầm thường gặp.

**The Exponential Fiasco (Thảm họa hàm mũ)**

Đây là nhận định sai: $4^x = O(2^x)$. Nó tăng trưởng theo bình phương của $2^x$, chứ không phải gấp đôi. **Trong hàm mũ, một sự thay đổi nhỏ ở cơ số sẽ dẫn đến sự bùng nổ khổng lồ ở kết quả**. Vậy nên, nhận định đúng là $4^x = (2^2)^x = (2^x)^2$.

**Constant Confusion (Nhầm lẫn về hằng số)**

Mọi hằng số đều là $O(1)$. Nhưng sai lầm xuất hiện khi ta áp dụng điều này vào một tổng. Đây là nhận định sai: $\sum_{i=1}^{n} i = O(n)$. Ở đây lập luận là: Vì mỗi số $i$ là $O(1)$, nên tổng của $n$ số $O(1)$ là $O(n)$.

Trong tổng này, $i$ không phải là hằng số. Nó chạy từ $1$ đến $n$. Khi $n$ tiến tới vô cùng, $i$ cũng tăng theo. Thực tế, tổng này là $n(n+1)/2$, tức là $\Theta(n^2)$, chứ không phải $O(n)$. **Bài học là đừng bao giờ cộng các $O(1)$ như thể chúng là những con số cố định.**

**Equality Blunder (Sai lầm về dấu bằng)**

Đây là lỗi phổ biến nhất. Ký hiệu $f = O(g)$ thực chất là một quan hệ một chiều, không phải là sự bằng nhau. Không bao giờ được viết ngược lại kiểu $O(f) = g$. Hãy coi dấu "=" ở đây như là "thuộc về" hoặc "là một".

Ví dụ: $$H_n = \ln(n) + \gamma + O\left(\frac{1}{n}\right)$$

Ý nghĩa đúng của nó là:

- Tồn tại một hàm số ẩn $f(n)$ nào đó sao cho $H_n = \ln(n) + \gamma + f(n)$.
- Và hàm số ẩn này thỏa mãn điều kiện $f(n) = O(1/n)$.

Nói cách khác, phần $O(1/n)$ chứa các sai số nhỏ mà chúng ta không cần viết chi tiết ra. Chúng ta chỉ cần biết rằng khi $n$ cực lớn, cái "sai số" này sẽ thu nhỏ lại với tốc độ ít nhất là bằng $1/n$.

**Operator Application Blunder (Lỗi áp dụng toán tử)**

Đừng mặc định rằng nếu $f$ tương đương với $g$ thì khi áp dụng bất kỳ hàm nào lên chúng, kết quả vẫn tương đương.

Ví dụ: $f \sim g$ không có nghĩa là $3^f = \Theta(3^g)$.

Nhưng có ngoại lệ: Nếu $f = \Theta(g)$ thì $\ln f \sim \ln g$ (trong những điều kiện nhất định).

### 13.7.5 Omega (Optional)

Đôi khi mọi người sử dụng sai ký hiệu Big O trong ngữ cảnh của một giới hạn dưới. Ví dụ, họ có thể nói: 'Thời gian chạy, $T(n)$, ít nhất là $O(n^2)$'. Đây là một sai lầm khác! Big O chỉ có thể được sử dụng cho các giới hạn trên. Cách đúng để diễn đạt giới hạn dưới sẽ là:$$n^2 = O(T(n))$$.

Giới hạn dưới cũng có thể được mô tả bằng một ký hiệu đặc biệt khác là 'Big Omega' ($\Omega$).

![[III.16.png]]

![[III.17.png]]

### Bảng Tổng Hợp Ký Hiệu Tiệm Cận

| Ký hiệu         | Ý nghĩa thực tế                                      | So sánh tương đương |
| :-------------- | :--------------------------------------------------- | :------------------ |
| $f = o(g)$      | $f$ tăng trưởng **chậm hơn hẳn** $g$.                | $f < g$             |
| $f = O(g)$      | $f$ tăng trưởng **không nhanh hơn** $g$ (Chặn trên). | $f \le g$           |
| $f = \Theta(g)$ | $f$ và $g$ tăng trưởng **cùng bậc** (Chặn chặt).     | $f \approx g$       |
| $f = \Omega(g)$ | $f$ tăng trưởng **không chậm hơn** $g$ (Chặn dưới).  | $f \ge g$           |
| $f = \omega(g)$ | $f$ tăng trưởng **nhanh hơn hẳn** $g$.               | $f > g$             |

# 14. Cardinality Rules

## 14.1 Counting One Thing by Counting Another

Cách trực tiếp nhất để đếm một tập hợp bằng cách đếm một tập hợp khác là tìm ra một song ánh (bijection) giữa chúng, bởi vì nếu tồn tại một song ánh giữa hai tập hợp, thì hai tập hợp đó có cùng kích thước. Đây là **Quy tắc Song ánh**.

## 14.2 Counting Sequences

Quy tắc Song ánh cho phép chúng ta đếm một thứ thông qua việc đếm một thứ khác. Điều này gợi ý một chiến thuật tổng quát: hãy thật giỏi trong việc đếm chỉ một vài thứ nhất định, sau đó sử dụng song ánh để đếm tất cả những thứ còn lại! Cụ thể, chúng ta sẽ rèn luyện để thật giỏi trong việc đếm các dãy (sequences). Khi chúng ta muốn xác định kích thước của một tập hợp $T$ nào đó, chúng ta sẽ tìm một song ánh từ $T$ đến một tập hợp các dãy $S$. Sau đó, chúng ta sẽ sử dụng kỹ năng đếm dãy 'siêu cấp ninja' của mình để xác định $|S|$, điều này lập tức cho ta biết $|T|$.

## 14.4 The Division Rule

Một hàm số $k$-đối-1 ($k$-to-1 function) ánh xạ chính xác $k$ phần tử của tập miền xác định (domain) vào mỗi phần tử của tập đích (codomain). Ví dụ, hàm số ánh xạ mỗi chiếc tai với chủ sở hữu của nó là hàm 2-đối-1. Tương tự, hàm số ánh xạ mỗi ngón tay với chủ sở hữu là hàm 10-đối-1.

Quy tắc tổng quát là: Nếu $f: A \to B$ là một hàm số $k$-đối-1, thì $|A| = k \cdot |B|$."

Thay vì đếm trực tiếp tập hợp $A$ (thường là tập hợp rất lớn và khó đếm), chúng ta đếm tập hợp $B$ (nhỏ hơn và dễ kiểm soát hơn), sau đó nhân với hệ số $k$.

## 14.5 Counting Subsets

Nhắc lại tổ hợp chập $k$ của $n$ và bài toán chia kẹo Euler.

## 14.6 Sequences with Repetitions

Nhắc lại tổ hợp lặp và nhị thức Newton.

## 14.8 The Pigeonhole Principle

Một định nghĩa khá hàn lâm, nhưng đầy đủ.

![[III.18.png]]

Ở phần này có một ví dụ,, bài toán khá hay là **A Magic Trick**, mọi người có thể lướt đến trang đó tìm hiểu thêm.

## 14.9 Inclusion-Exclusion

![[III.19.png]]

## 14.10 Combinatorial Proofs

### 14.10.2 Giving a Combinatorial Proof

> [!INFO] Basic outline for Combinatorial Proof
>
> - Định nghĩa tập hợp $S$: Xác định một nhóm các đối tượng cụ thể mà bạn muốn đếm
> - Đếm theo cách thứ nhất: Chứng minh rằng kích thước của tập hợp $S$ (ký hiệu là $|S|$) bằng $n$.
> - Đếm theo cách thứ hai: Chứng minh rằng cũng chính tập hợp $S$ đó, nếu nhìn dưới một góc độ khác, sẽ có kích thước bằng $m$.
> - Kết luận: Vì cả hai cách đều đếm cùng một tập hợp $S$, nên ta khẳng định $n = m$.

**Checking a Combinatorial Proof**

Trong trường hợp lập luận tổ hợp gây mơ hồ, ta có thể sử dụng thiết lập song ánh (bijection) để chứng minh sự tương ứng 1-1 giữa hai tập hợp khác nhau, hoặc quy đổi về đếm chuỗi (sequence counting) để đảm bảo tính chính xác và hệ thống cho chứng minh.

### 14.10.3 A Colorful Combinatorial Proof

Thay vì xây dựng những giả định phức tạp, các chứng minh tổ hợp hiệu quả thường tập trung vào việc định nghĩa tập hợp $S$ dựa trên các cấu trúc toán học cơ bản như chuỗi (sequences) hoặc tập hợp con (sets). Chìa khóa nằm ở khả năng lựa chọn tập hợp $S$ một cách khôn ngoan, trong đó vế đơn giản hơn của đẳng thức thường đóng vai trò là "kim chỉ nam" định hình bản chất của đối tượng cần đếm. Điểm ưu việt của phương pháp này là không cần đến các phép biến đổi đại số nặng nề.

# 15. Generating Functions
