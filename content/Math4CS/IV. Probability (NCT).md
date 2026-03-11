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

## 18.3 Distribution
