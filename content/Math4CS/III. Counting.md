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
