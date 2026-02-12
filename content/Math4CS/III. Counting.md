# 13. Sums and Asymptotics

Closed Form là một biểu thức toán học có thể tính toán được bằng một số lượng hữu hạn các phép tính cơ bản (như cộng, trừ, nhân, chia, lũy thừa). Nó không chứa các dấu ba chấm ($\dots$), không chứa ký hiệu tổng $\sum$ hay tích $\prod$ phụ thuộc vào một biến số chạy.

Ví dụ: Thay vì viết tổng cấp số nhân là $1 + x + x^2 + \dots + x^n$, ta viết dạng đóng của nó là $\frac{1-x^{n+1}}{1-x}$.

Closed Form giúp tính toán nhanh hơn, dễ dàng phân tích xu hướng (khi n tăng thì biểu thức tăng như nào), tính giới hạn.

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
