# 21. Recurrences

## 21.3 Linear Recurrences

### 21.3.2 Solving Homogeneous Linear Recurrences

Hệ thức truy hồi tuyến tính thuần nhất có dạng: $f(n) = a_1f(n-1) + a_2f(n-2) + \dots + a_df(n-d)$

Với:

- Bậc (Order) $d$: Là số lượng các số hạng đứng trước cần thiết để tính số hạng hiện tại.
- Thuần nhất (Homogeneous): Hiểu đơn giản là phương trình này không chứa các hằng số đứng độc lập hoặc các hàm số của $n$ (như $+n$ hay $+1$).

![[V.01.png]]

Dễ hiểu nên thôi khỏi giải thích hê hê.

### 21.3.3 Solving General Linear Recurrences

Bước đầu tiên là thế $f(n) = x^n$ vào. Đây là một bước đoán, vì các hệ thức tuyến tính có xu hướng tăng trưởng theo quy luật lũy thừa.

Khi đó chia cho $x^{n-d}$ ta tìm được phương trình đặc trưng: $$x^d - a_1x^{d-1} - a_2x^{d-2} - \dots - a_d = 0$$ (Bậc của phương trình đúng bằng bậc của hệ thức truy hồi ($d$))

Sau khi giải phương trình đặc trưng, các nghiệm (gốc) sẽ quyết định hình dáng của công thức đóng:

- Trường hợp nghiệm đơn (Non-repeated roots): Nếu bạn tìm được một nghiệm $r$, thì $r^n$ là một thành phần của lời giải.
- Trường hợp nghiệm lặp (Repeated roots): Đây là điểm mới quan trọng. Nếu một nghiệm $r$ xuất hiện $k$ lần (bội $k$), chúng ta không thể chỉ dùng $r^n$ vì sẽ thiếu nghiệm. Thay vào đó, chúng ta "nhân thêm $n$" để tạo ra các nghiệm độc lập tuyến tính: $r^n, n \cdot r^n, n^2 \cdot r^n, \dots, n^{k-1} \cdot r^n$

> [!INFO]
> Lúc học VMO toi có học cái này rồi thì phải, mỗi tội là không nhớ, nên giờ ghi lại vậy

Sau đó ứng dụng định lí mới chụp hình to đùng ở trên thì công thức tổng quát là linear combinations của đống nghiệm mình vừa mới tìm ra trong bước giải phương trình đặc trưng. Chỉ còn tìm hệ số thôi đúng không? Lúc này ta thay vô các trường hợp cơ sở vô rồi giải hệ phương trình để tìm.

### 21.3.3 Solving General Linear Recurrences

Lấy hệ thức truy hồi tuyến tính thuần nhất rồi cộng thêm một hàm $g(n)$ nào đó ta được hệ thức truy hồi tuyến tính tổng quát, còn giải như nào tra mạng nha...

## 21.4 Divide-and-Conquer Recurrences

Hệ thức truy hồi chia để trị có dạng: $$T(n) = \sum_{i=1}^{k} a_i T(b_i n) + g(n)$$

- $T(n)$: Tổng thời gian (hoặc chi phí) để hoàn thành một dự án quy mô $n$.
- $a_i$ (Số lượng cấp dưới): Bạn chia dự án lớn thành $k$ loại công việc khác nhau. $a_i$ là số lượng công việc loại $i$ mà bạn giao đi.
- $b_i n$ (Quy mô công việc con): Mỗi công việc con chỉ có quy mô bằng một phần ($b_i$) so với dự án gốc (với $0 < b_i < 1$).
- $g(n)$ (Chi phí quản lý): Đây là thời gian bạn bỏ ra để chia việc và quan trọng nhất là gộp các kết quả từ cấp dưới lại thành sản phẩm cuối cùng.

### 21.4.1 The Akra-Bazzi Formula

![[V.02.png]]

### 21.4.2 Two Technical Issues

Trong các hệ thức truy hồi tuyến tính (như Fibonacci), thay đổi điều kiện biên ($f(0), f(1)$) sẽ làm thay đổi hoàn toàn các hằng số trong công thức cuối cùng. Nhưng với hệ thức Chia để trị, các ký pháp như $\Theta(n \log n)$ chỉ quan tâm đến tốc độ tăng trưởng. Do đó, kết quả tiệm cận của Akra-Bazzi luôn đúng bất kể bạn bắt đầu với con số nào ở điều kiện biên.

Khó nói, ví dụ, Merge Sort sẽ chia 15 thành $\lceil 15/2 \rceil = 8$ và $\lfloor 15/2 \rfloor = 7$. Các hàm làm tròn này không có tác dụng trong công thức của Akra-Bazzi. Bạn có thể tự tin loại bỏ tất cả các ký hiệu $\lceil \rceil$ và $\lfloor \rfloor$ khi giải hệ thức truy hồi để tìm độ phức tạp thuật toán mà không sợ làm sai lệch kết quả cuối cùng.

### 21.4.3 The Akra-Bazzi Theorem

:v Lười chụp định lí quá, thôi thì, lướt đến trang 885 đọc nha. Đoạn văn khẳng định rằng Akra-Bazzi không chỉ là một công thức tính toán, mà còn là một công cụ trừu tượng hóa mạnh mẽ. Nó cho phép các nhà khoa học máy tính:

- Làm việc trên tập số thực thay vì bị gò bó trong số nguyên.
- Tự tin bỏ qua các chi tiết vụn vặt như làm tròn số, vì định lý đã chứng minh rằng những "sai số" này sẽ bị triệt tiêu trong bức tranh tổng thể của tốc độ tăng trưởng tiệm cận.

### 21.4.4 The Master Theorem

![[V.03.png]]

Là trường hợp đặc biệt của cái định lí khủng bố ở mục trước. Học trong môn CS112 ở UIT.

## 21.5 A Feel for Recurrences

Dựa trên các recurrences đã nhắc qua ở chương này, ta rút ra các nhận xét sau:

- Việc làm cho bài toán con nhỏ đi bao nhiêu lần quan trọng hơn rất nhiều so với việc bạn làm thêm bao nhiêu bước ở mỗi tầng đệ quy. Vì nó ảnh hưởng đến thời gian thực thi rất nhiều. (So sánh giữa Tower of Hanoi vs Merge Sort) Cả hai loại hệ thức tuyến tính đều rất nhạy cảm với số lượng bài toán con.
- Điều kiện biên ($T_0, T_1, \dots$) hầu như không quan trọng với hệ thức chia để trị và đối với hệ thức tuyến tính thì thường bị chi phối bởi hàm mũ có cơ số lớn nhất (vì nếu nó khiến số hạng này về 0, sẽ làm biến động mạnh độ phức tạp).
- Nếu thu nhỏ bài toán bằng phép trừ thì solution là hàm mũ phức tạp, nếu thu nhỏ bài toán bằng phép chia thì sol là polynomial (Thumb rule gì gì đó)

Oh shiet thật sự đã xong huhu. Right now its 00:15 AM, 17.03.2026.
