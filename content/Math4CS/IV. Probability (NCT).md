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
