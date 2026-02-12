# 8. Number Theory

## 8.2 The Greatest Common Divisor (GCD)

### 8.2.2 The Pulverizer

> [!INFO]
> Ước chung lớn nhất của hai số $a$ và $b$ luôn có thể biểu diễn dưới dạng tổ hợp tuyến tính của $a$ và $b$:
> $$\gcd(a, b) = sa + tb$$

> [!INFO]
> An integer is a linear combination of a and b iff it is a multiple of $\gcd(a,b)$

Với iff viết tắt cho "tương đương"

Có một cách thường dùng để tính GCD là **thuật toán Euclid**. Cùng với nó là **Pulverizer**, ý tưởng giống Euclid nhưng ghi lại linear combination của a và b ở từng bước.

![[II.03.png]]

## 8.3 Prime Mysteries

![[II.04.png]]

![[II.05.png]]

Từ công thức $\pi(x) \approx \frac{x}{\ln x}$, ta có thể suy ra: Nếu bạn chọn ngẫu nhiên một số nguyên trong khoảng từ $1$ đến $x$, xác suất để số đó là số nguyên tố là khoảng: $$\frac{1}{\ln x}$$

## 8.4 The Fundamental Theorem of Arithmetic

> [!INFO] Fundamental Theorem of Arithmetic
> Every positive integer is a product of a unique weakly decreasing sequence of primes.
>
> For example, 75237393 is the product of the weakly decreasing sequence of primes 23; 17; 17; 11; 7; 7; 7; 3; and no other weakly decreasing sequence of primes will give 75237393.

## 8.5 Alan Turing

### 8.5.1 Turing’s Code (Version 1.0)

Trước khi mã hóa thì ta phải số hóa thông điệp trước. Tức là chuyển text thành number.

Ví dụ: Chữ "victory" được ghép lại thành một con số khổng lồ: 22090320151825.

Trong mã của Turing, thông điệp $m$ phải là một số nguyên tố. Nếu số $m$ sau khi đổi từ chữ sang số không phải là số nguyên tố, ta sẽ thêm vài chữ số vào đuôi (padding) cho đến khi tìm được một số nguyên tố.

=> **Prime Number Theorem nói rằng số nguyên tố không quá hiếm.** Vì vậy, ta không cần phải thử quá nhiều lần; chỉ cần thêm vài chữ số (như số 13 trong ví dụ) là xác suất tìm được số nguyên tố là rất cao.

![[II.07.png]]

**Kiểm tra tính nguyên tố (Primality Testing)**

Câu hỏi đặt ra là: "Làm sao để chắc chắn $m$ và $k$ là số nguyên tố?". Nếu bạn chọn đại một số cực lớn (ví dụ có 500 chữ số), làm sao bạn biết nó là số nguyên tố hay là hợp số?

Tác giả nhấn mạnh rằng việc kiểm tra một số có phải nguyên tố hay không thực ra "dễ" hơn nhiều so với việc phân tích nó ra thành thừa số. Hiện nay, chúng ta có các thuật toán như **Miller-Rabin (thuật toán xác suất cực nhanh)** hoặc **AKS (thuật toán đa thức chắc chắn)**.

**Tại sao quân Phát xít lại "bó tay"? (Độ an toàn)**

Hệ thống này dựa trên một thứ gọi là **Hàm một chiều (One-way function)**: Bạn có $m$ và $k$ (hai số nguyên tố cực lớn). Việc nhân chúng lại để tạo ra $m_b = m \times k$ là cực kỳ nhanh chóng, ngay cả với máy tính yếu. Kẻ địch chỉ có $m_b$. Để tìm lại thông điệp $m$, chúng buộc phải phân tích thừa số nguyên tố (factorize) số $m_b$.

Như đã đề cập ở phần trước, chưa ai tìm ra một thuật toán chạy trong "thời gian đa thức" để phân tích một số là tích của hai số nguyên tố lớn.

### 8.5.2 Breaking Turing’s Code (Version 1.0)

Khi bạn gửi hai tin nhắn $m_1$ và $m_2$ với cùng một khóa $k$:

Tin nhắn 1: $m_{c1} = m_1 \times k$

Tin nhắn 2: $m_{c2} = m_2 \times k$

Quân Phát xít (kẻ tấn công) bây giờ có hai con số $m_{c1}$ và $m_{c2}$. Chúng không cần phải phân tích thừa số nguyên tố (bài toán khó) nữa. Thay vào đó, chúng chỉ cần tìm Ước chung lớn nhất (GCD). Theo tính chất của GCD: $$gcd(m_{c1}, m_{c2}) = gcd(m_1 \cdot k, m_2 \cdot k) = k \cdot gcd(m_1, m_2)$$. Vì $m_1$ và $m_2$ là các số nguyên tố khác nhau (theo quy định của mã Turing), nên $gcd(m_1, m_2) = 1$.

Kết quả là: $$gcd(m_{c1}, m_{c2}) = k$$

## 8.8 Turing’s Code (Version 2.0)

![[II.08.png]]

Vì m_hat lúc này là một số dư trong khoảng 0 đến n, nên ta không thể tính m bằng cách lấy m_hat chia cho k được.

## 8.9 Multiplicative Inverses and Cancelling

![[II.09.png]]

Ở đây đang nói đến nghịch đảo modulo. Vì 2.8 = 16 mà chia dư cho 15 được 1 nên gọi 8 là nghịch đảo của 2.

### 8.9.1 Relative Primality

> [!INFO]
> Bổ đề 1: Nếu $k$ thuộc $[0..n)$ và nguyên tố cùng nhau với $n$, thì $k$ luôn có số nghịch đảo trong tập $\mathbb{Z}_n$
>
> Bổ đề 2: Nếu $i$ và $j$ đều là số nghịch đảo của $k$ trong $\mathbb{Z}_n$, thì $i = j$

Vành $\mathbb{Z}_n$ là một cấu trúc cơ bản trong toán học, chứa các số dư có thể có khi thực hiện phép chia một số nguyên bất kỳ cho $n$.

Trong vành $\mathbb{Z}_n$ thì dấu = đại diện cho dấu modulo (chia dư) nha. Phần chứng minh Bổ đề 1 thì ý tưởng dựa trên $\gcd(k,n)$ = linear combination của k và n.

Khi $p$ là số nguyên tố, vành $\mathbb{Z}_p$ trở thành một Trường (Field). Đặc điểm tuyệt vời nhất của nó là:

- Mọi số khác $0$ đều có nghịch đảo
- Nếu $a \cdot b = 0$, thì chắc chắn $a = 0$ hoặc $b = 0$.

Khi $n$ là hợp số (ví dụ $n = 6, 15, 20$), $\mathbb{Z}_n$ chỉ là một vành.

- Chỉ những số nào "nguyên tố cùng nhau" với $n$ ($\gcd(a, n) = 1$) mới có nghịch đảo.
- Hai số khác $0$ nhân với nhau lại có thể bằng $0$!

### 8.9.2 Cancellation

Trong số thực hay số hữu tỉ, nếu bạn có $t \cdot r = t \cdot s$ và $t \neq 0$, bạn hiển nhiên suy ra $r = s$. Nhưng trong $\mathbb{Z}_n$, bạn không thể làm điều tương tự.

![[II.12.png]]

Bạn chỉ có thể triệt tiêu $t$ trong phương trình $t \cdot r = t \cdot s \pmod n$ nếu và chỉ nếu $t$ có nghịch đảo modulo $n$ (tức là $\gcd(t, n) = 1$).

![[II.13.png]]

### 8.9.3 Decrypting (Version 2.0)

![[II.14.png]]

### 8.9.4 Breaking Turing’s Code (Version 2.0)

Đối với mã Turing Version 2.0, giả sử quân Phát xít thu thập được:

- $m$: Bản rõ (nội dung tin nhắn gốc).
- $\hat{m}$ (trong sách viết là $mb$): Bản mã tương ứng.
- $n$: Số modulo công khai.

Để tìm $k$, quân Phát xít chỉ cần "loại bỏ" $m$ khỏi vế phải. Trong số học thông thường, ta sẽ chia cho $m$. Trong vành $\mathbb{Z}_n$, chúng sử dụng công cụ gọi là The Pulverizer (Thuật toán Euclid mở rộng) để tìm số nghịch đảo của $m$. Sau khi tìm xong thì decrypt một cách bình thường như trên.

**Tác giả nhận định Version 2.0 là "vô giá trị".** Một hệ thống mật mã thực tế phải đảm bảo rằng dù kẻ tấn công có biết hàng ngàn cặp $(m, \hat{m})$, chúng vẫn không thể tìm ra khóa $k$ trong thời gian cho phép. Một khi $k$ bị lộ, toàn bộ các tin nhắn trong quá khứ và tương lai (sử dụng cùng khóa $k$) đều bị giải mã hoàn toàn.

## 8.10 Euler’s Theorem

![[II.15.png]]

![[II.16.png]]

Trong vành $\mathbb{Z}_n$, nghịch đảo của $k$ chính là $k^{\phi(n)-1}$. Đây là một ứng dụng thực tế giúp tìm số nghịch đảo mà không cần The Pulverizer.

![[II.17.png]]

### 8.10.1 Computing Euler's Phi Function

![[II.18.png]]

![[II.19.png]]

![[II.20.png]]

Các bạn để ý thấy các phần này toàn chụp định nghĩa và định lí các thứ, thì nó vậy đó huheo. Về chứng minh thì nếu ai đã từng học qua chương trình THPT cho chuyên toán thì chắc đều biết rồi nên mình nhắc lại thôi.

## 8.11 RSA Public Key Encryption

Khác với mã Turing (nơi người gửi và nhận phải gặp nhau lén lút để trao đổi khóa $k$), RSA cho phép giao dịch an toàn mà không cần gặp mặt trước:

- **Public Key (Khóa công khai):** Được phân phối rộng rãi. Ai cũng có thể dùng nó để mã hóa tin nhắn gửi cho bạn.
- **Private Key (Khóa bí mật):** Bạn giữ riêng cho mình. Chỉ có khóa này mới giải mã được những gì đã mã hóa bằng khóa công khai tương ứng.

Như bạn đã nhận thấy ở mã Turing Ver 2.0, việc chỉ nhân $m \cdot k \pmod n$ rất dễ bị bẻ gãy. RSA đã nâng cấp phép toán này:

- **Mã hóa:** Thay vì nhân, RSA nâng tin nhắn lên một lũy thừa bí mật.
- **Modulo:** RSA không hoạt động trên số nguyên tố $p$, mà hoạt động trên số $n = p \cdot q$ (tích của hai số nguyên tố khổng lồ).

Đoạn văn khẳng định Định lý Euler là trung tâm để hiểu RSA. Lý do là:

- RSA cần một cách để "đảo ngược" phép lũy thừa mà không cần thực hiện phép chia (vì trong $\mathbb{Z}_n$ không có phép chia thông thường).
- Nếu tin nhắn $m$ nguyên tố cùng nhau với $n$ ($\gcd(m, n) = 1$), Định lý Euler $m^{\phi(n)} \equiv 1 \pmod n$ giúp chúng ta tìm ra một số mũ $d$ sao cho khi nâng bản mã lên lũy thừa $d$, ta quay lại được tin nhắn gốc $m$.

![[II.21.png]]

Sự bảo mật của hệ thống RSA không dựa trên một chứng minh toán học tuyệt đối rằng nó "không thể bị phá vỡ", mà dựa trên một giả thuyết về độ khó của việc tính toán và sự bền bỉ của nó trước thời gian. Cốt lõi bảo mật của RSA nằm ở giả thuyết rằng việc phân tích một số nguyên thành tích của hai số nguyên tố lớn (mỗi số dài hàng trăm chữ số) là một việc "khó khăn đến tuyệt vọng".

## 8.12 What has SAT got to do with it?

Mối đe dọa lớn nhất đối với RSA không đến từ các phép thử trực tiếp mà đến từ khả năng chuyển đổi bài toán phân tích số thành bài toán logic (SAT) thông qua các mạch kỹ thuật số.

- **Mạch kiểm tra tích (Product Checker):** Chúng ta có thể xây dựng một mạch điện sử dụng các cổng logic (AND, OR, NOT) để kiểm tra xem liệu $i \cdot j = k$. Mạch này chỉ yêu cầu số lượng cổng logic tỉ lệ thuận với $n^2$.
- **Chuyển đổi sang Logic:** Mọi mạch điện kỹ thuật số đều có thể được mô tả bằng các công thức logic có kích thước tương đương. Do đó, việc tìm các giá trị đầu vào cho mạch chính là giải bài toán SAT.

Nếu tồn tại một bộ giải SAT (SAT Solver) hiệu quả, việc phân tích thừa số một số $m$ khổng lồ sẽ được thực hiện qua $n$ lần thử như sau:

1. **Cố định giá trị mục tiêu:** Thiết lập đầu vào $k$ của mạch bằng đúng giá trị $m$ cần phân tích.
2. **Dò tìm từng bit của thừa số:**

- Thử đặt bit đầu tiên của thừa số $i$ là $1$.
- Sử dụng máy giải SAT để kiểm tra xem có tồn tại các giá trị bit còn lại của $i$ và $j$ để thỏa mãn mạch điện không.
- Nếu máy giải SAT trả về "Có", ta giữ bit đó là $1$; nếu không, ta đặt nó là $0$.

3. **Lặp lại:** Tiếp tục thực hiện tương tự cho đến bit cuối cùng của $i$. Sau $n$ bước, chúng ta tìm ra thừa số $i$ hoàn chỉnh.

**Nếu bài toán SAT có thể được giải trong thời gian đa thức (Polynomial time), thì bài toán phân tích thừa số nguyên tố cũng có thể được giải trong thời gian đa thức.**

# 9. Directed graphs & Partial Orders

## 9.3 Adjacency Matrices

Đây là khái niệm ma trận kề mà các bạn đã gặp trong môn DSA, ở phần đồ thị á, để biểu diễn giữa 2 đỉnh có kề hay không. Nếu có kề thì c_ij = 1, không kề thì nó = 0. Ta mở rộng khái niệm này ra một chút.

![[II.22.png]]

Mỗi ô ở hàng $u$, cột $v$ (ký hiệu là $C_{uv}$) cho bạn biết có bao nhiêu cách để đi từ đỉnh $u$ đến đỉnh $v$ trong đúng $k$ bước.

- Độ dài $k=1$: Chính là Ma trận kề (Adjacency Matrix - $A_G$). Nếu có cạnh nối trực tiếp từ $u$ đến $v$, giá trị là 1 (có 1 bước đi), nếu không là 0.
- Độ dài $k=0$: Chính là Ma trận đơn vị ($I$). Bạn chỉ có thể ở yên tại chỗ (từ $u$ đến chính nó) trong 0 bước. Vì vậy, các ô trên đường chéo chính là 1, các ô khác là 0.

![[II.23.png]]

Định lý này nói rằng: Nếu bạn nhân ma trận đếm bước đi độ dài $k$ ($C$) với ma trận đếm bước đi độ dài $m$ ($D$), kết quả sẽ là ma trận đếm bước đi độ dài $k + m$.

Từ định lý này, chúng ta có một quy tắc cực kỳ hữu ích: **Lũy thừa của ma trận kề cho biết số bước đi.**

![[II.24.png]]

### 9.3.1 Shortest Paths

Ý tưởng rất đơn giản: Để tìm khoảng cách giữa đỉnh $u$ và đỉnh $v$, bạn cứ lũy thừa ma trận kề $A_G$ lên dần dần ($A^1, A^2, A^3, \dots$) và "canh chừng" (watching). Đến khi nhận thấy ô $(u, v) > 0$ lần đầu tiên thì khoảng cách ngắn nhất đúng bằng số mũ của ma trận.

Trong một đồ thị có $n$ đỉnh, một đường đi ngắn nhất (không đi vòng lại) chỉ có thể có tối đa là $n-1$ cạnh. Nếu bạn đã tính đến $A^{n-1}$ mà ô $(u, v)$ vẫn bằng 0, thì kết luận luôn: **Không có đường đi nào nối giữa $u$ và $v$ cả**.

Ý tưởng này là nền tảng cho **Đồ thị có trọng số** (Weighted Graphs) và các thuật toán tối ưu khác **(BFS cho đồ thị không trọng số, hoặc Dijkstra/Floyd-Warshall cho đồ thị có trọng số.)**

## 9.4 Walk Relations

Phần này bàn về việc, xác định giữa 2 đỉnh xem liệu có một đường đi nào từ đỉnh u sang đỉnh v hay không.

![[II.25.png]]

### 9.4.1 Composition of Relations

Nhớ rằng, một đồ thị có hướng $G$ trên tập đỉnh $V$ thực chất chỉ là một tập hợp các cặp $(a, b)$ mà trong đó có một mũi tên đi từ $a$ đến $b$. Hay nói cách khác là quan hệ hai ngôi.

![[II.26.png]]

Để đi từ $a$ đến $c$, bạn phải tìm được một "trạm trung chuyển" $b$ sao cho $a$ đến được $b$ và $b$ đến được $c$.

Bây giờ, thay vì $R$ và $S$, chúng ta lấy $G$ hợp thành với chính nó ($G \circ G$, ký hiệu là $G^2$):

- $a G^2 c$ có nghĩa là: Có một đỉnh $b$ sao cho $a \to b$ và $b \to c$.
- $a \to b \to c$ chính là một bước đi độ dài 2.

![[II.27.png]]

![[II.28.png]]

$G^0$ là Quan hệ đồng nhất (Identity relation): Nghĩa là mỗi đỉnh tự kết nối với chính nó.

Định nghĩa $G^*$ là quan hệ bước đi: "$u$ có thể đến được $v$". Để điều này đúng, thì: Bạn có thể đến trong 0 bước (đứng yên tại chỗ: $G^0$) HOẶC bạn đến trong đúng 1 bước ($G^1$) HOẶC bạn đến trong đúng 2 bước ($G^2$)...

**Kĩ thuật Repeated Squaring**

Hãy gọi $R = G \cup G^0$. Quan hệ $R$ có nghĩa là: "Đi được từ $u$ đến $v$ trong 0 HOẶC 1 bước".

khi chúng ta hợp thành $R$ với chính nó ($R^2$):

- $R^2 = (G \cup G^0) \circ (G \cup G^0)$
- Theo tính chất phân phối, nó bao gồm: $G^0 \circ G^0 = G^0$ (0 bước) ; $G^0 \circ G = G^1$ (1 bước) ; $G \circ G^0 = G^1$ (1 bước) ; $G \circ G = G^2$ (2 bước)
- Vậy $R^2 = G^0 \cup G^1 \cup G^2$ (Nghĩa là: đi được trong **tối đa** 2 bước).

Tương tự như vậy, $R^{n-1}$ sẽ là tất cả các đường đi có độ dài **tối đa** $n-1$ bước.

## 9.5 Directed Acyclic Graphs & Scheduling

> [!INFO]
> A directed acyclic graph (DAG) is a directed graph with no cycles.

DAG là "xương sống" của nhiều hệ thống:

- **Lập lịch công việc (Task Scheduling):** Nếu bạn có 10 việc cần làm trên một máy tính có nhiều chip xử lý, DAG sẽ cho bạn biết việc nào có thể làm song song, việc nào phải đợi việc kia xong (Concurrency control).
- **Quản lý mã nguồn:** Các công cụ như Make, Gradle hay Bazel dùng DAG để biết phần nào của code cần biên dịch trước.
- **Excel:** Khi bạn đặt công thức ô C1 = A1 + B1, Excel tạo ra một DAG để biết phải tính ô nào trước khi dữ liệu thay đổi.

### 9.5.1 Scheduling

> [!INFO]
> A **topological sort** of a finite DAG is a list of all the vertices such that each vertex v appears earlier in the list than every other vertex reachable from
> v.

> [!INFO]
> An vertex v of a DAG, D, is minimum iff every other vertex is reachable from v.
> A vertex v is minimal iff v is not reachable from any other vertex.

**Cách tạo một sắp xếp Topo:**

- Tìm các phần tử Minimal
- Chọn một trong số đó, giả sử là $u$
- Loại bỏ $u$ và các cạnh nối nó ra khỏi đồ thị
- Trong những đỉnh $v$ mà $u \to v$, ta tìm các phần tử Minimal mới
- Tiếp tục cho đến khi chọn được hết các đỉnh

> [!INFO]
> Every finite DAG has a topological sort.

Còn nhiều cách sắp xếp Topo khác nhưng đây là cách thường dùng.

### 9.5.2 Parallel Task Scheduling

> [!INFO]
> Two vertices in a DAG are comparable when one of them is reachable from the other. A chain in a DAG is a set of vertices such that any two of them are comparable. A vertex in a chain that is reachable from all other vertices in the chain is called a maximum element of the chain. A finite chain is said to end at its maximum element.

Nếu việc A và việc B "có thể so sánh", nghĩa là chúng có quan hệ phụ thuộc. Bạn không thể làm chúng cùng lúc; việc này phải đợi việc kia xong. Nếu hai việc không thể so sánh, bạn có thể làm chúng song song.

Tất cả các việc trong chuỗi này phải được thực hiện theo một thứ tự duy nhất, việc nọ nối tiếp việc kia. **Đỉnh lớn nhất (Maximum element):** Là việc cuối cùng của chuỗi, chỉ được làm khi tất cả các việc khác trong chuỗi đã xong.

**Critical Path**

Chính là chuỗi có độ dài lớn nhất (có nhiều đỉnh nhất) trong đồ thị. Dù bạn có bao nhiêu bộ vi xử lý đi chăng nữa, thời gian tối thiểu để hoàn thành toàn bộ dự án luôn bằng số bước trong chuỗi dài nhất này.

Bởi vì các công việc trong một chuỗi buộc phải làm tuần tự. Nếu chuỗi dài nhất có 5 việc, bạn không bao giờ có thể hoàn thành dự án trong 4 bước, vì ít nhất 5 việc đó phải chiếm 5 mốc thời gian khác nhau.

Bạn luôn có thể lập một lịch trình để hoàn thành mọi việc trong đúng t bước (với t là độ dài chuỗi dài nhất). Ở mỗi bước, hãy làm tất cả các việc đang là "Minimal" (việc không cần điều kiện gì thêm).

Dưới đây là các định nghĩa toán học.

> [!INFO]
> A partition of a set A is a set of nonempty subsets of A called the blocks of the partition, such that every element of A is in exactly one block.

Phân hoạch tức là chia ra thành các tập hợp riêng rẽ nhau, không có phần tử nào cùng thuộc 2 tập hợp trong một phân hoạch.

Trong đồ thị DAG, lập lịch song song là việc bạn chia các công việc vào các "khung giờ" (các khối $A_0, A_1, A_2, \dots$)

> [!INFO]
> A largest chain ending at an element a is called a critical path to a, and the number of elements less than a in the chain is called the depth of a.

Đây là cách lập lịch nhanh nhất có thể (với giả định bạn có vô hạn máy tính/nhân lực): Việc gì có độ sâu bằng $k$ thì hãy làm nó ngay ở bước thứ $k$. Nó giống hệt cách mình giải thích trước đó, chỉ khác góc nhìn thôi. Hiểu rằng độ sâu $k$ này có nghĩa là cần làm $k$ việc trước rồi mới tới $a$.

### 9.5.3 Dilworth’s Lemma (Optional)

> [!INFO]
> An antichain in a DAG is a set of vertices such that no two elements in the set are comparable—no walk exists between any two different vertices in the set.

> [!INFO]
> In a DAG, $D$, if the size of the largest chain is $t$, then $V(D)$ can be partitioned into t antichains.

![[II.29.png]]

## 9.6 Partial Orders

Gọi là quan hệ thứ tự một phần, nhưng chắc bạn quên nên mình nhắc lại.

### 9.6.1 The Properties of the Walk Relation in DAGs

> [!INFO]
> A binary relation, $R$, on a set, $A$, is **transitive** iff $(a R b) AND (b R c) \implies a R c$ for every $a, b, c \in A$.
>
> A binary relation, $R$, on a set, $A$, is **reflexive** iff $a R a$ for all $a \in A$
>
> A binary relation, $R$, on a set, $A$, is **irreflexive** iff $NOT(a R a)$ for all $a \in A$

### 9.6.2 Strict Partial Orders

> [!INFO]
> A relation that is transitive and irreflexive is called a strict partial order.

For example, the less-than order, <, on numbers is a strict partial order.

> [!INFO]
> A binary relation, $R$, on a set, $A$, is **asymmetric** iff $(a R b) \implies NOT(b R a)$ for all $a, b \in A$

Quan hệ thứ tự một phần (Strict Partial Order) quan tâm đến việc: "A có đứng trước C hay không?". Nó không quan tâm bạn đi đến đó bằng 1 bước hay 10 bước. Do đó **nhiều DAG có thể tạo ra cùng một quan hệ thứ tự một phần.**
=> Tìm một DAG có ít cạnh nhất để biểu diễn một quan hệ thứ tự, bỏ hết các cạnh thừa.

### 9.6.3 Weak Partial Orders

> [!INFO]
> A binary relation, $R$, on a set, $A$, is **antisymmetric** iff $(a R b) \implies NOT(b R a)$ for all $a \neq b \in A$
>
> A binary relation on a set is a weak partial order iff it is transitive, reflexive and antisymmetric

Hoặc ta có thể định nghĩa thông qua Strict Partial Orders như sau:

![[II.37.png]]

For example, "nhỏ hơn hoặc bằng", on numbers is a weak partial order.

## 9.7 Representing Partial Orders by Set Containment

![[II.38.png]]

Nếu $a$ có quan hệ với $a'$ trong thế giới này, thì bản sao của chúng là $f(a)$ và $f(a')$ cũng phải có quan hệ tương ứng trong thế giới kia.

**Làm sao để biến một thứ tự bất kỳ thành quan hệ tập con?** Hãy đại diện mỗi phần tử $a$ bằng tập hợp của tất cả những kẻ đứng trước nó (bao gồm cả chính nó).

$$a \to \{b \in A \mid b \preceq a\}$$

Ví dụ:

- Số 3 được đại diện bởi tập các số chia hết cho nó trong tập đã cho: $\{1, 3\}$.
- Số 12 được đại diện bởi tập: $\{1, 3, 4, 6, 12\}$.
- Vì $3$ chia hết cho $12$, nên chắc chắn mọi số chia hết cho $3$ cũng phải chia hết cho $12$. Do đó:

$$\{1, 3\} \subseteq \{1, 3, 4, 6, 12\}$$

![[II.39.png]]

## 9.8 Linear Orders

Thứ tự Tuyến tính (Linear Order), hay còn gọi là Thứ tự Toàn phần (Total Order). Một quan hệ thứ tự một phần được gọi là tuyến tính nếu: **Mọi cặp phần tử khác nhau đều có thể so sánh được.** Đối với Partial Order thì có tồn tại các phần tử mà không so sánh với nhau được.

Ví dụ: Quan hệ tập con ($\subseteq$) là một phần, quan hệ < là toàn phần

## 9.9 Product Orders

**Tích của các quan hệ (Product of Relations)**—một cách để kết hợp hai hệ thống thứ tự cũ thành một hệ thống mới phức tạp hơn.

Cặp $(a_1, a_2)$ có quan hệ với cặp $(b_1, b_2)$ khi và chỉ khi cả hai điều kiện sau đều đúng:

- $a_1$ có quan hệ với $b_1$ trong hệ thống thứ nhất ($R_1$).
- $a_2$ có quan hệ với $b_2$ trong hệ thống thứ hai ($R_2$).

Nếu $R_1$ và $R_2$ là các Thứ tự một phần (Partial Orders), thì tích của chúng cũng là một thứ tự một phần. Tích của hai thứ tự tuyến tính KHÔNG nhất thiết là thứ tự tuyến tính.

> [!INFO]
> Khá giống tích Descartes (hoặc Cartesian) giữa 2 tập hợp ha ;v

## 9.10 Equivalence Relations

> [!INFO]
> A relation is an equivalence relation if it is reflexive, symmetric and transitive

Ví dụ về quan hệ tương đương cũng nhiều, nhưng đây là một ví dụ khá tổng quát, tạo ra quan hệ dựa trên một hàm số.

![[II.41.png]]

Hai phần tử $a$ và $a'$ có quan hệ với nhau khi và chỉ khi kết quả của chúng qua hàm $f$ là như nhau.
=> **Một quan hệ là quan hệ tương đương khi và chỉ khi nó có thể được biểu diễn dưới dạng $\equiv_f$ của một hàm số nào đó.**

### 9.10.1 Equivalence Classes

Mình sẽ không chụp định nghĩa vào đây mà so sánh nó với một khái niệm đã làm quen từ trước: **phân hoạch của tập hợp**. **Quan hệ tương đương và Phân hoạch thực chất là hai cách nhìn cho cùng một vấn đề.**

**Phân hoạch $\to$ Quan hệ tương đương:** Nếu bạn chủ động chia một tập hợp thành các khối (blocks) không chồng lấn, thì việc "ở chung một khối" nghiễm nhiên là một quan hệ tương đương.

**Quan hệ tương đương $\to$ Phân hoạch:** Nếu bạn có một quan hệ tương đương, các lớp tương đương của nó sẽ tự động "cắt" tập hợp của bạn thành các khối hoàn hảo.

Ví dụ: Bạn có một túi bi nhiều màu. Nếu quan hệ tương đương là "có cùng màu", thì lớp tương đương của một viên bi Xanh chính là tập hợp tất cả các viên bi Xanh trong túi đó.

# 10. Communication Networks (Optional)

Việc thiết kế mạng được chuyển đổi sang ngôn ngữ đồ thị có hướng (digraphs) để tính toán. Ta cần nắm các khái niệm sau:

- **Gói tin (Packet):** Đơn vị dữ liệu kích thước cố định (ví dụ 256 hoặc 4096 bytes).
- **Điểm đầu cuối (Terminal):** Nơi bắt đầu (Source) và kết thúc (Destination) của gói tin.
- **Bộ chuyển mạch (Switches):** Nút trung gian điều hướng gói tin từ cạnh vào đến cạnh ra.
- **Bài toán Định tuyến (Routing Problem):** Một hoán vị $\pi$ xác định gói tin từ đầu vào $i$ phải tới đầu ra $\pi(i)$.
- **Phương án Định tuyến ($P$):** Tập hợp các đường đi cụ thể giải quyết hoán vị $\pi$.
- **Độ trễ:** Số lượng dây dẫn (cạnh) mà gói tin phải đi qua.
- **Đường kính (Diameter):** Chiều dài của đường đi ngắn nhất giữa cặp đầu vào - đầu ra xa nhau nhất. Đại diện cho độ trễ trong trường hợp xấu nhất.
- **Độ trễ mạng (Latency):** Là chiều dài của đường đi dài nhất trong một phương án định tuyến tối ưu nhất. Trong cấu trúc cây, Latency thường bằng Diameter vì đường đi là duy nhất.
- **Sự tắc nghẽn (Congestion):** Số lượng đường đi tối đa cùng chạy qua một Switch đơn lẻ trong một phương án định tuyến. Congestion càng cao, gói tin càng dễ bị chậm trễ tại các switch bị quá tải.

## 10.3 Network Diameter

Một cách để giảm đường kính của một mạng lưới là sử dụng các bộ chuyển mạch (switches) lớn hơn. Tuy nhiên, điều này không mang lại nhiều hiệu quả. Việc sử dụng một bộ chuyển mạch $N \times N$ sẽ chỉ che giấu bài toán thiết kế mạng ban đầu bên trong bộ chuyển mạch trừu tượng này. Cuối cùng, chúng ta sẽ phải thiết kế cấu trúc bên trong của bộ chuyển mạch quái vật đó bằng các thành phần đơn giản hơn, và thế là chúng ta lại quay trở về vạch xuất phát. Vì vậy, thách thức trong việc thiết kế một mạng truyền thông là tìm ra cách để đạt được chức năng của một bộ chuyển mạch $N \times N$ bằng cách sử dụng các thiết bị cơ bản, kích thước cố định, chẳng hạn như bộ chuyển mạch $3 \times 3$.

## 10.4 Switch Count

Một mục tiêu khác trong việc thiết kế mạng truyền thông là sử dụng càng ít bộ chuyển mạch (switches) càng tốt. Số lượng bộ chuyển mạch trong một cây nhị phân hoàn chỉnh là $2N - 1$, đây là mức gần như tốt nhất có thể đạt được đối với các bộ chuyển mạch $3 \times 3$.

## 10.6 Congestion

Cây nhị phân hoàn chỉnh có một nhược điểm chí tử: bộ chuyển mạch gốc (root switch) là một nút thắt cổ chai. Ở điều kiện tốt nhất, bộ chuyển mạch này phải xử lý tất cả các gói tin đi từ nửa trái sang nửa phải và ngược lại. Trong trường hợp xấu nhất, nếu bộ chuyển mạch này hỏng, mạng lưới sẽ bị chia cắt thành hai phần có kích thước bằng nhau.

Bằng cách mở rộng khái niệm tắc nghẽn cho mạng lưới, chúng ta cũng có thể phân biệt giữa mạng 'tốt' và 'xấu' liên quan đến các vấn đề thắt nút. Đối với mỗi bài toán định tuyến $\pi$, chúng ta giả định một phương án định tuyến được chọn để tối ưu hóa sự tắc nghẽn (tức là có sự tắc nghẽn tối thiểu). Khi đó, mức độ tắc nghẽn lớn nhất mà một bộ chuyển mạch phải chịu đựng sẽ là mức tắc nghẽn tối đa trong số các định tuyến tối ưu này. **Mức tắc nghẽn 'maximin' này được gọi là sự tắc nghẽn của mạng**.

## 10.7 2-D Array

![[II.42.png]]

The diameter of an array with $N$ inputs and outputs is $2N$, which is much worse than the diameter of $2 \log N + 2$ in the complete binary tree. But we get something in exchange: **replacing a complete binary tree with an array almost eliminates congestion**.

## 10.8 Butterfly

**Butterfly Network** giữ được đường kính ngắn gần như cây nhị phân, nhưng lại phân tán luồng dữ liệu tốt hơn để tránh tắc nghẽn cực đoan. Tuy nhiên, nó không hội tụ được những đặc tính tốt nhất của mỗi loại mạng, mà đúng hơn, nó là một sự thỏa hiệp nằm đâu đó ở giữa hai loại mạng này.

Ta định nghĩa theo kiểu đệ quy:

- **Trường hợp cơ sở ($F_1$):** Là mạng nhỏ nhất với 2 đầu vào và 2 đầu ra. Các switch được nối chéo nhau tạo thành hình chữ X (giống cánh bướm).
- **Bước dựng ($F_{n+1}$):** Để tạo ra một mạng lớn hơn, người ta lấy hai mạng nhỏ ($F_n$) và đặt thêm một hàng switch mới ở phía trước. Mỗi switch mới sẽ nối với một switch tương ứng ở mạng $F_n$ phía trên và một ở mạng $F_n$ phía dưới. **Chính cách nối "chéo" này giúp dữ liệu từ bất kỳ đầu vào nào cũng có thể tìm đường sang bất kỳ đầu ra nào mà không nhất thiết phải đi qua một "nút gốc" duy nhất.**

![[II.43.png]]

![[II.44.png]]

Đây là thuật toán Routing, cũng được định nghĩa theo kiểu đệ quy

- **Trường hợp cơ sở ($F_1$):** Chỉ có 2 đầu vào và 2 đầu ra. Đường đi là hiển nhiên.
- **Bước đệ quy ($F_{n+1}$):** Khi gói tin đang ở một switch đầu vào của mạng lớn ($F_{n+1}$): Nếu đích đến (output) nằm ở nhóm phía trên (top copy), gói tin sẽ nhảy vào cổng kết nối với mạng $F_n$ phía trên. Nếu đích đến nằm ở nhóm phía dưới (bottom copy), gói tin sẽ nhảy vào mạng $F_n$ phía dưới. Sau khi đã vào được mạng $F_n$ tương ứng, quy trình này lặp lại cho đến khi gói tin chạm đích.

Một đặc điểm quan trọng là: **Giữa bất kỳ đầu vào $i$ và đầu ra $j$ nào, chỉ tồn tại duy nhất một con đường**.

## 10.9 Beneš Network

Ý tưởng của Beneš cực kỳ đơn giản: **Ghép hai mạng Butterfly lại với nhau theo kiểu đối lưng (back-to-back).** Nếu mạng Butterfly chỉ cho phép dữ liệu đi theo một hướng đệ quy duy nhất, thì mạng Benes tạo ra một cấu trúc đối xứng.

Đây là định nghĩa đệ quy:

- **Trường hợp cơ sở ($B_1$):** Giống hệt $F_1$ (Butterfly cấp 1)
- **Bước dựng ($B_{n+1}$):** Được tạo ra từ hai mạng $B_n$ nhỏ hơn. Thêm một cột switch mới ở phía trước (đầu vào). Thêm một cột switch mới ở phía sau (đầu ra). Mỗi switch mới ở đầu vào nối với hai mạng $B_n$ bên trong, và mỗi switch mới ở đầu ra cũng nhận tín hiệu từ hai mạng $B_n$ đó.

![[II.45.png]]

Đến đây, chúng ta đã có một cái nhìn toàn cảnh về sự tiến hóa của các mô hình mạng:

![[II.46.png]]

# 11. Simple Graphs

Phần này bàn về đồ thị vô hướng, bổ đề bắt tay,...

## 11.4 Isomorphism

Một đồ thị có thể được vẽ theo nhiều cách: co giãn, bẻ cong các cạnh, hoặc đặt tên đỉnh khác nhau (đỉnh $A$ thay vì đỉnh $1$). Tuy nhiên, nếu "cấu trúc kết nối" của chúng là một, thì chúng được gọi là đẳng cấu.

![[II.47.png]]

Tác giả nhấn mạnh rằng đẳng cấu là một quan hệ tương đương (equivalence relation), nghĩa là nó hội đủ 3 tính chất: Phản xạ, Đối xứng, Bắc cầu.

> [!INFO]
> Thật ra định nghĩa về đẳng cấu đã có ở mục 9.7, cụ thể là định nghĩa 9.7.1. Chỉ là ở mục này ta áp dụng nó một cách trực quan hơn.

Nếu $G$ và $H$ đẳng cấu, chúng bắt buộc phải có chung các đặc điểm sau:

- Cùng số lượng đỉnh và số lượng cạnh.
- Cùng bậc của các đỉnh (ví dụ: nếu $G$ có 2 đỉnh bậc 3, thì $H$ cũng phải có 2 đỉnh bậc 3).
- Có cùng các cấu trúc con (ví dụ: nếu $G$ có một chu trình tam giác, $H$ cũng phải có).

Nếu bạn tìm thấy một tính chất mà $G$ có nhưng $H$ không có (ví dụ số cạnh khác nhau), bạn có thể kết luận ngay lập tức: chúng không đẳng cấu.

Tác giả đưa ra hai ứng dụng thực tế rất thú vị:

- **Hóa học (Chemistry):** Giúp tìm kiếm các phân tử trong cơ sở dữ liệu. Hai công thức hóa học trông có vẻ khác nhau trên giấy nhưng thực tế lại là cùng một loại phân tử dựa trên các liên kết nguyên tử.
- **Bảo mật & Mã hóa (Cryptography):** Việc xác định hai đồ thị lớn có đẳng cấu hay không là một bài toán cực kỳ khó về mặt tính toán (chưa có thuật toán thời gian đa thức hiệu quả cho mọi trường hợp). Sự "khó nhằn" này chính là cơ sở để xây dựng các giao thức xác thực và mã hóa an toàn.

> [!INFO]
> "Lý thuyết đồ thị thực chất là nghiên cứu về các tính chất được bảo toàn bởi sự đẳng cấu." Khi ta nói "Đồ thị đầy đủ $K_n$ có $n$ đỉnh", ta không quan tâm đó là đỉnh $A, B, C$ hay $1, 2, 3$. Ta đang nói về một "gia đình" các đồ thị có cùng cấu trúc đẳng cấu.

## 11.5 Bipartite Graphs & Matchings

Tức là bạn có thể chia các đỉnh thành 2 tập hợp, mà mỗi đỉnh trong mỗi tập hợp sẽ không nối nhau, vì vậy chỉ có cạnh từ đỉnh tập A đến đỉnh tập B thôi. Trực quan thì tưởng tượng nó giống như hình ảnh ánh xạ vv.

![[II.48.png]]

![[II.49.png]]

### 11.5.1 The Bipartite Matching Problem

**Bối cảnh bài toán:** Số lượng phụ nữ nhiều hơn số lượng nam giới. Không thể có chuyện mọi phụ nữ đều lấy chồng, do đó ta tập trung vào việc tìm vợ cho mọi đàn ông sao cho mỗi người đàn ông đều được ghép đôi với một người phụ nữ mà anh ta thích.

Để giải quyết bài toán này, chúng ta sử dụng một đồ thị hai phía. Một cạnh tồn tại giữa người đàn ông $A$ và người phụ nữ $B$ nếu $A$ thích $B$. Trong mô hình này, mối quan hệ "thích" không nhất thiết phải đến từ hai phía. Chúng ta hiện chỉ ưu tiên điều kiện "người đàn ông thích người vợ của mình".

> [!INFO]
> **Một Matching** (Ghép cặp) hoàn hảo cho phía nam giới được định nghĩa là một sự phân công thỏa mãn 3 điều kiện:
>
> - Mọi người đàn ông đều có vợ
> - Không ai chung vợ
> - Người đàn ông phải được ghép đôi với người phụ nữ mà anh ta thực sự thích

**The Matching Condition**

> [!INFO] Hall's Matching Theorem
> Mọi tập hợp con gồm các người đàn ông bất kỳ phải yêu thích một tập hợp phụ nữ có số lượng lớn hơn hoặc bằng số lượng đàn ông đó.
>
> Hãy gọi $S$ là một nhóm đàn ông bất kỳ, và $N(S)$ là tập hợp tất cả những người phụ nữ mà ít nhất một người trong nhóm $S$ thích. Điều kiện này yêu cầu: $$\lvert S \rvert \le \lvert N(S) \rvert$$

Nếu điều kiện trên không thỏa mãn, chắc chắn không có cách nào ghép cặp được. Điều này khá dễ hiểu. Đây mới là phần gây kinh ngạc. Hall chứng minh rằng chỉ cần điều kiện trên được đảm bảo cho mọi tập con của nam giới, thì chắc chắn sẽ tồn tại ít nhất một phương án ghép cặp hoàn hảo. Do đó **Matching Condition là điều kiện cần và đủ**.

![[II.50.png]]

Phép chứng minh Định lý trên đưa ra một thuật toán để tìm một phép ghép cặp trong đồ thị hai phía, mặc dù đó không hiệu quả cho lắm. Tuy nhiên, các thuật toán hiệu quả để tìm phép ghép cặp trong đồ thị hai phía thực sự tồn tại. Vì vậy, nếu một bài toán có thể được quy dẫn về việc tìm một phép ghép cặp, thì bài toán đó về cơ bản đã được giải quyết dưới góc độ tính toán.

**An Easy Matching Condition**

Định lý Hall yêu cầu ta kiểm tra mọi tập hợp con của nam giới. Việc kiểm tra thủ công hay dùng máy tính yếu để quét sạch các tập con này là bất khả thi. Vì vậy, chúng ta cần những dấu hiệu nhận biết nhanh hơn dựa trên **Bậc của đỉnh (Degree)**.

![[II.51.png]]

![[II.52.png]]

Nếu xem tập nam giới là L(G) thì matching covers L(G) tương đương với bài toán ta xét nãy giờ.

Một đồ thị là chính quy (regular) nếu mọi đỉnh đều có bậc bằng nhau (ví dụ: tất cả đều có bậc bằng 3). Mọi đồ thị hai phía chính quy đều có một phép ghép cặp hoàn hảo (perfect matching), là phép ghép cặp mà tất cả các đỉnh ở cả hai phía $L$ và $R$ đều được ghép đôi, không sót một ai.

## 11.6 The Stable Marriage Problem

**Bối cảnh bài toán:** Cũng là ghép đôi, nhưng lần này kèm theo trọng số và số nam = số nữ. Các con số cạnh tên mỗi người thể hiện thứ tự ưu tiên của họ. Số 1 tức là họ thích người này nhất, tương tự cho số 2, 3...cho đến n. Họ sẽ xếp hạng mức độ ưu tiên của mình.

![[II.53.png]]

Một cặp đôi (ví dụ: Brad và Angelina) được gọi là Rogue Couple khi cả hai không cưới nhau, nhưng lại thích nhau hơn người bạn đời hiện tại của mình. Như trên ảnh. Brad và Angelina sẽ có xu hướng "rời bỏ" cuộc hôn nhân hiện tại để đến với nhau. Đây chính là yếu tố gây ra sự **không ổn định**.

> [!INFO]
> Một hệ thống hôn nhân được gọi là ổn định khi không tồn tại bất kỳ một "Rogue Couple" nào.

Trong ví dụ trên, nếu cho Brad cưới Angelina thì Jennifer phải cưới Billy Bob. Dù Jennifer hay Billy Bob có thể "không hạnh phúc" và muốn tìm người khác, nhưng họ không thể rủ rê được ai. Do đó, **sự ổn định** không có nghĩa là tất cả mọi người đều lấy được người mình yêu nhất, mà có nghĩa là không có hai người nào "đồng lòng" phản bội cuộc hôn nhân hiện tại để đến với nhau.

Trong bài toán Nam - Nữ (đồ thị lưỡng phân), toán học chứng minh được rằng **luôn luôn tồn tại ít nhất một cách ghép đôi ổn định**. Khi chúng ta bỏ đi ranh giới giới tính (không còn là đồ thị lưỡng phân), và nó thành **bài toán Buddy Matching**, sự ổn định không còn được đảm bảo nữa.

### 11.6.1 The Mating Ritual

Đây là **Thuật toán Gale-Shapley**:

- Bước 1: Lấy một người đàn ông $m$ tự do. Gọi $w$ là người phụ nữ xếp hạng cao nhất trong danh sách của $m$ mà $m$ **chưa từng cầu hôn trước đó**.
- Bước 2: Nếu $w$ đang tự do: $(m, w)$ trở thành một cặp "đính hôn tạm thời". Nếu $w$ đang đính hôn với $m'$ và $w$ ưu tiên $m$ hơn $m'$ thì $m'$ trở lại trạng thái tự do và $(m, w)$ trở thành cặp đính hôn tạm thời mới. Nếu $w$ ưu tiên $m'$ hơn $m$ thì $m$ vẫn ở trạng thái tự do (bị từ chối).
- Bước 3: Những người $m$ bị từ chối thì sẽ gạch $w$ đã từ chối họ khỏi danh sách riêng (tức là vòng lặp sau sẽ cầu hôn người khác).
- Bước 4: Lặp lại thuật toán cho tới khi ghép đủ hết.

Kết thúc: Khi không còn người đàn ông nào tự do và có thể cầu hôn, tất cả các cặp đính hôn tạm thời trở thành hôn nhân chính thức.

Một số facts ta cần chứng minh, và sẽ chứng minh lần lượt ở các mục sau:

- The Ritual eventually reaches the termination condition.
- Everybody ends up married.
- The resulting marriages are stable.

### 11.6.2 There is a Marriage Day

Giả sử có $n$ nam và $n$ nữ, mỗi người đàn ông sẽ khởi đầu với một danh sách ưu tiên chứa đầy đủ $n$ người phụ nữ. Như vậy, tổng số mục (entries) trong tất cả các danh sách ưu tiên của nam giới là $n \times n = n^2$. Trong mỗi bước lặp của thuật toán (mỗi ngày của nghi lễ), nếu điều kiện dừng chưa được thỏa mãn, tức là vẫn còn ít nhất một người phụ nữ nhận được từ hai lời cầu hôn trở lên, thì ít nhất một người đàn ông sẽ bị từ chối. Theo quy tắc, người bị từ chối bắt buộc phải gạch tên người phụ nữ đó khỏi danh sách ưu tiên của mình. Vì các mục đã bị gạch sẽ không bao giờ được thêm lại, tổng số mục trong tất cả các danh sách ưu tiên là một đại lượng giảm ngặt sau mỗi bước lặp. Do đó thuật toán sẽ đạt trạng thái dừng.

### 11.6.3 They All Live Happily Ever After. . .

Dễ dàng nhận thấy rằng, **tiêu chuẩn của nữ chỉ tăng lên**. Bởi vì mỗi vòng lặp $w$ chỉ thay đổi cặp khi $m$ "tốt hơn". Đương nhiên nếu không có $m$ tốt hơn thì cặp đó vẫn giữ nguyên và ông $m$ đó không làm hành động gạch $w$ khỏi danh sách riêng.

Sử dụng tính chất này kèm phản chứng để chứng minh rằng: **Everybody ends up married** và **The resulting marriages are stable**. Phần chứng minh rất dễ, bạn có thể tự thực hành nha.

### 11.6.4 . . . Especially the Men

> [!INFO]
> While the Mating Ritual produces one stable matching, stable matchings need not be unique.

Chẳng hạn như khi đổi lại là bên tập nữ chủ động đi cầu hôn thì nó sẽ ra một kết quả stable matching khác. Stable không có nghĩa là Unique.

![[II.54.png]]

Bổ đề này bạn tự chứng minh nhe hê hê. Tóm lại là nếu $m$ bị $w$ nào đó từ chối thì họ không thể là một cặp trong bất kì stable matching nào. Tức là không phải feasible spouse như trên định nghĩa.

Mặc dù thuật toán mang lại cảm giác phụ nữ nắm quyền kiểm soát thông qua việc lựa chọn và từ chối, nhưng định lý 11.6.10 đã chứng minh một kết quả ngược lại: Thuật toán này tối ưu hóa lợi ích cho người cầu hôn và tối thiểu hóa lợi ích cho người nhận lời. Cụ thể, thuật toán đảm bảo mọi đàn ông đều cưới được "Bạn đời tối ưu" (Optimal Spouse) — người họ thích nhất trong số tất cả các lựa chọn có thể tạo ra một cuộc hôn nhân ổn định. Ngược lại, mọi phụ nữ đều kết thúc với "Bạn đời tệ nhất" (Pessimal Spouse) — người họ ít ưu tiên nhất trong số những đối tác khả thi về mặt toán học. Điều này xảy ra bởi vì đàn ông được chủ động "duyệt" danh sách từ trên xuống dưới và dừng lại ngay ở điểm cao nhất có thể; trong khi đó, phụ nữ phải chờ đợi và tiêu chuẩn của họ chỉ được nâng lên dựa trên sự ngẫu nhiên của những người đến cầu hôn. Vì vậy, trong lý thuyết ghép đôi, thực thể nắm quyền chủ động cầu hôn luôn giành được lợi thế tuyệt đối về chất lượng hôn nhân.

### 11.6.5 Applications

Trước khi có thuật toán này, việc phân bổ bác sĩ vào bệnh viện gặp phải những "khủng hoảng" nghiêm trọng. Các bệnh viện và sinh viên thường xuyên phá vỡ hợp đồng vì họ tìm thấy những lựa chọn khác tốt hơn. Thuật toán Gale-Shapley đã giải quyết vấn đề này hiệu quả đến mức nó được giữ nguyên gần như không thay đổi trong suốt hàng thập kỷ.

Ngày nay, nó còn được ứng dụng trong Dating Apps, ghép cặp hiến tạng, tuyển sinh đại học...

## 11.7 Coloring

### 11.7.1 An Exam Scheduling Problem

Đây là bài toán sắp xếp lịch thi sao cho **không có sinh viên nào có 2 môn học phải thi cùng một ca thi**. Chắc chắn là không xếp theo kiểu mỗi ca một môn rồi :> nếu vậy thì kì thi sẽ kéo dài rất lâu. Trong bài toán này thì mỗi đỉnh là một môn, **2 đỉnh kề nhau nếu như có một sinh viên nào đó đăng kí cả 2 môn này**. **Mỗi ca thi sẽ là một màu**.

=> Ta cần tô màu đồ thị sao cho 2 đỉnh kề nhau thì được tô 2 màu khác nhau. Và số màu tô phải là ít nhất.

> [!INFO]
> The minimum value of $k$ for which a graph, G, has a valid coloring is called its chromatic number, $\chi(G)$

Việc xác định $\chi(G)$ là một bài toán kinh điển thuộc nhóm NP-complete. Đặc trưng của bài toán này nằm ở sự bất đối xứng về chi phí tính toán: trong khi việc kiểm tra tính hợp lệ của một phương án tô màu cho trước có thể thực hiện rất nhanh chóng (thời gian đa thức), thì việc tìm ra cách tô màu tối ưu lại cực kỳ khó khăn và hiện chưa có thuật toán giải nhanh nào được biết đến. Do đó, việc tìm ra một thuật toán hiệu quả để giải quyết bài toán này không chỉ mang lại giá trị thực tiễn to lớn trong tối ưu hóa nguồn lực mà còn giúp giải quyết giả thuyết $P$ vs $NP$.

### 11.7.2 Some Coloring Bounds

Một cách tự nhiên, ta có:

- Đồ thị vòng chẵn ($C_{even}$): Luôn có $\chi = 2$. Bạn chỉ cần tô xen kẽ màu 1 và màu 2.
- Đồ thị vòng lẻ ($C_{odd}$): Luôn có $\chi = 3$. Do đỉnh cuối cùng sẽ kề với cả đỉnh đầu tiên và đỉnh áp chót, nên 2 màu là không đủ.
- Đồ thị đầy đủ ($K_n$): Trong $K_n$, mọi đỉnh đều nối với nhau. Vì thế, không có hai đỉnh nào được phép trùng màu. $\chi(K_n) = n$.
- Đồ thị lưỡng phân: $\chi(G)$ = 2, tập $L$ một màu, tập $R$ một màu.

> [!INFO]
> A graph, G, with at least one edge is bipartite iff $\chi(G)$ = 2

Việc tô được 2 màu với việc phân ra được 2 tập đỉnh trong đồ thị lưỡng phân nó là tương đương nhau, nên ta có bổ đề trên đây.

> [!INFO]
> Nếu bậc cao nhất của một đỉnh trong đồ thị là $k$, thì đồ thị đó có thể tô được bằng $k+1$ màu.

Kết quả này có thể chứng minh dựa trên quy nạp. Tác giả có một lời khuyên rất hay là đừng dùng quy nạp trên $k$ (vì sẽ rất rắc rối), mà hãy dùng quy nạp trên số đỉnh $n$ hoặc số cạnh $e$. Nhớ là có thể thôi, chứ $k + 1$ chưa chắc là số màu ít nhất.

### 11.7.3 Why coloring?

Một số ứng dụng của tô màu đồ thị, chủ yếu là **tối ưu hóa tài nguyên bị giới hạn**:

- **Triển khai phần mềm quy mô lớn:** Có một số máy chủ phụ thuộc vào nhau. Thay vì cập nhật từng cái một, họ chỉ cần chia thành vài đợt (số màu cần tô). Mỗi đợt cập nhật hàng nghìn máy chủ cùng lúc.
- **Cấp phát tần số vô tuyến:** Hai đài phát thanh có vùng phủ sóng chồng lấn không được phép dùng chung tần số (vì sẽ gây nhiễu). Tìm sắc số $\chi(G)$ để sử dụng ít tần số nhất mà vẫn đảm bảo tín hiệu rõ nét.
- **Cấp phát thanh ghi:** Hai biến số không thể dùng chung một thanh ghi nếu chúng đang được sử dụng cùng lúc trong chương trình. Sử dụng tối thiểu số thanh ghi (màu) để chạy chương trình hiệu quả nhất.
- **Tô màu bản đồ và Đồ thị phẳng**: Đây là bài toán khởi nguồn của lý thuyết tô màu đồ thị. **Định lý Bốn màu:** Mọi bản đồ trên mặt phẳng đều có thể được tô bằng tối đa 4 màu sao cho các quốc gia giáp ranh không trùng màu.

## 11.8 Simple Walks

Phần này nhắc lại khái niệm về đường đi trên đồ thị, nhưng lần này là cho simple graphs. Chắc các bạn đều biết hết rồi nên mình sẽ không ghi ở đây.

### 11.8.2 Cycles as Subgraphs

Nếu ta gọi một chu trình là một "đường đi khép kín" (closed walk), ta vô tình tạo ra một điểm bắt đầu (ví dụ: $A \to B \to C \to A$). Nhưng thực tế, cái vòng đó vẫn là một dù bạn bắt đầu từ $A, B$ hay $C$. Để giải quyết việc này, tác giả đã chuyển sang dùng khái niệm Đồ thị con (Subgraph).

> [!INFO]
> Đồ thị $G$ là con của $H$ nếu toàn bộ đỉnh và cạnh của $G$ đều nằm trong $H$.
>
> Chu trình là một tập hợp các đỉnh và cạnh tạo thành một đồ thị con đẳng cấu (isomorphic) với $C_n$

$C_n$ là gì? Đây là một "khuôn mẫu" chuẩn về một cái vòng có $n$ cạnh (ví dụ $C_3$ là tam giác, $C_4$ là hình vuông). Ta sẽ kêu chu trình là một đồ thị mà nó đẳng cấu với đồ thị vòng ;v. Chỉ là vấn đề về định nghĩa thôi.

## 11.9 Connectivity

Phần này bàn về khái niệm liên thông giữa 2 đỉnh, đồ thị liên thông, thành phần liên thông. Thành phần liên thông = đồ thị con mà nó liên thông.

### 11.9.2 Odd Cycles and 2-Colorability

> [!INFO]
> Các tính chất sau là tương đương:
>
> - Đồ thị chứa một chu trình độ dài lẻ
> - Đồ thị không thể tô bằng 2 màu (hay nói cách khác nó không phải lưỡng phân)
> - Đồ thị chứa một đường đi khép kín độ dài lẻ

Từ đây cũng suy ra một kết quả hay dùng: **đồ thị lưỡng phân khi và chỉ khi nó không chứa chu trình lẻ**.

### 11.9.3 K-connected Graphs

Trong thực tế (như đường ống dầu hay cáp điện), chúng ta cần sự dự phòng. Một mạng lưới tốt là mạng lưới vẫn hoạt động được ngay cả khi một vài thành phần bị hỏng.

> [!INFO]
> Hai đỉnh được gọi là $k$-connected nếu bạn xóa đi bất kỳ $k-1$ cạnh nào, thì đồ thị thu được sau đó vẫn liên thông.
>
> Cầu: Là cạnh mà nếu thiếu nó, đồ thị không còn liên thông nữa.
>
> Một cạnh là cầu khi nó không nằm trong chu trình nào (khá hiển nhiên)

Tổng quát hơn, nếu hai đỉnh được kết nối bởi một số $k$ đường đi rời rạc về cạnh (tức là không có cạnh nào xuất hiện đồng thời trong hai đường đi khác nhau), thì chúng chắc chắn là $k$-kết nối. Điều này là do ta phải xóa ít nhất một cạnh từ mỗi con đường đó thì mới có thể khiến chúng mất liên lạc.

Một sự thật cơ bản, mà chúng tôi xin phép bỏ qua phần chứng minh cực kỳ khéo léo của nó, chính là **định lý Menger**. Định lý này khẳng định rằng điều ngược lại cũng đúng: nếu hai đỉnh là $k$-kết nối, thì sẽ có đúng $k$ đường đi rời rạc về cạnh nối giữa chúng.

### 11.9.4 The Minimum Number of Edges in a Connected Graph

> [!INFO]
> Mọi đồ thị $G$ đều có ít nhất $|V(G)| - |E(G)|$ thành phần liên thông
>
> Dẫn đến hệ quả: Mọi đồ thị liên thông có $n$ đỉnh thì phải có ít nhất $n - 1$ cạnh

Khi bạn gặp một bài toán đồ thị, hai cách tiếp cận này nên là những lựa chọn đầu tiên bạn cân nhắc: **quy nạp trên số cạnh và quy nạp trên số đỉnh của đồ thị**.

Mặt khác, khi quy nạp trên số cạnh chẳng hạn, ta hay gặp buildup error. Cụ thể ta thường bắt đầu với một đồ thị $k$ cạnh rồi thêm một cạnh nữa để có đồ thị $(k+1)$ cạnh. Bạn sẽ sai khi giả định rằng mọi đồ thị $(k+1)$ cạnh đều có thể được tạo ra bằng cách thêm 1 cạnh vào một đồ thị $k$ cạnh "có tính chất X nào đó". Cách làm đúng là bắt đầu bằng một đồ thị $(k+1)$ cạnh bất kỳ (tổng quát hoàn toàn), bẻ đi 1 cạnh để nó rơi về trường hợp $k$ cạnh đã biết, sau đó gắn lại để xem tính chất có được bảo toàn không.

## 11.10 Forests & Trees

> [!INFO]
> Tree: đồ thị liên thông và không có chu trình
> Forest: đồ thị không có chu trình (gồm nhiều thành phần liên thông hợp thành, mỗi thành phần đó là một tree)

### 11.10.2 Properties

Sau đây là các tính chất của cây:

- Mọi đồ thị con liên thông cũng là một cây
- Có duy nhất một đường đi giữa mọi cặp đỉnh (Nếu không nó sẽ tạo chu trình)
- Thêm một cạnh giữa hai nút không kề nhau sẽ tạo ra chu trình. (Nếu thêm sẽ tạo chu trình)
- Xóa bất kỳ cạnh nào cũng làm đồ thị mất liên thông (Mọi cạnh đều là cạnh cắt)
- Nếu cây có ít nhất 2 đỉnh, nó phải có ít nhất 2 lá
- Số lượng đỉnh luôn lớn hơn số lượng cạnh đúng 1 đơn vị

### 11.10.3 Spanning Trees

> [!INFO]
> Every connected graph contains a spanning tree, a subgraph containing all the vertices of G.

### 11.10.4 Minimum Weight Spanning Trees

Cây khung (Spanning trees) rất thú vị bởi vì chúng kết nối tất cả các nút của một đồ thị bằng cách sử dụng số lượng cạnh ít nhất có thể. Trong nhiều ứng dụng, có các chi phí bằng số hoặc trọng số (weights) gắn liền với các cạnh của đồ thị. Trọng số của một đồ thị được định nghĩa đơn giản là tổng trọng số của tất cả các cạnh cấu thành nên nó.

=> **Bài toán tìm cây khung tối tiểu (tối thiểu hóa trọng số/chi phí)** hay còn gọi là **tìm MST**

Với **pre-MST là một đồ thị con bao trùm của $G$ và đồng thời là đồ thị con của ít nhất một MST nào đó của $G$.** Định nghĩa hơi khó hiểu ha ;>

> [!INFO] Chiến lược xây dựng MST
>
> - **Khởi tạo:** Bắt đầu với một rừng bao trùm rỗng (pre-MST). Thật ra là bắt đầu với đồ thị chỉ toàn đỉnh, không có cạnh.
> - **Lặp lại:** Liên tục tìm và thêm các cạnh mở rộng vào rừng hiện tại.
> - **Kết thúc:** Khi số cạnh đạt đúng $|V(G)| - 1$, rừng sẽ trở thành một cây. Vì nó là một pre-MST và đã là một cây, nó chắc chắn là một MST.

Làm sao để tìm và thêm các cạnh mở rộng? Có một phương pháp gọi là **Solid Coloring** như sau:

> [!INFO] Phương pháp Solid Coloring
>
> - Tô màu khối (Solid Coloring): Tô màu tất cả các đỉnh trong mỗi thành phần liên thông của pre-MST $F$ bằng màu Đen hoặc Trắng. Các đỉnh trong cùng một thành phần phải cùng màu. Phải tồn tại ít nhất một cụm màu Đen và một cụm màu Trắng.
> - Xác định cạnh xám (Gray Edges): Một cạnh xám là cạnh nối giữa một đỉnh màu trắng và một đỉnh màu đen trong đồ thị gốc $G$.
> - Áp dụng bổ đề: Một cạnh sẽ là cạnh mở rộng nếu nó có trọng số nhỏ nhất trong số tất cả các cạnh xám của một cách tô màu khối bất kỳ.

Ví dụ: Nếu bạn có 4 thành phần liên thông $A, B, C, D$. Bạn có thể tô $\{A, B\}$ màu Trắng và $\{C, D\}$ màu Đen. Hoặc chỉ tô $\{A\}$ màu Trắng và $\{B, C, D\}$ màu Đen. Mỗi cách chọn này là một "loại" solid coloring khác nhau.

Mỗi loại solid coloring dẫn đến các thuật toán khác nhau, tiêu biểu như:

- Thuật toán Prim: Thuật toán này duy trì một tập đỉnh đã liên thông $V_{tree}$ và mở rộng nó.
- Thuật toán Kruskal: Thuật toán này tập trung vào việc chọn các cạnh rẻ nhất trên toàn đồ thị mà không tạo thành chu trình.
- Thuật toán tổng quát hóa (dùng cùng coloring với Prim): Chính là dựa trên phương pháp solid coloring. Grow a forest one edge at a time by picking any component and adding a minimum weight edge among the edges leaving that component.

Khác với thuật toán Prim (bắt buộc phải mọc ra từ một gốc duy nhất), Thuật toán 3 cho phép bạn chọn bất kỳ thành phần liên thông (component) nào để mở rộng. Do đó có thể áp dụng **tính song song**, áp dụng nhiều bộ xử lí song song để hoàn thành công việc. Mặt khác, đối với bài toán MST, **sự tham lam** luôn mang lại kết quả đúng. Các nhà toán học đã chứng minh được rằng chỉ cần bạn cứ chọn cạnh rẻ nhất (thỏa mãn điều kiện), bạn chắc chắn sẽ có được cây khung rẻ nhất toàn cục.

Nếu đồ thị có các trọng số đôi một khác nhau (distinct weights), thì đồ thị đó chỉ có duy nhất một MST. Lúc này, cả Prim và Kruskal chắc chắn sẽ hội tụ về cùng một kết quả duy nhất. Vì cả hai đều tuân theo nguyên lý chọn cạnh xám rẻ nhất.

Về mặt kỹ thuật, các thuật toán như Prim hay Kruskal có độ phức tạp khoảng $O(E \log V)$ hoặc $O(E \log E)$. Rất lẹ ;v

# 12. Planar Graphs

## 12.1 Drawing Graphs in the Plane

Tính phẳng của đồ thị tức là bạn có thể vẽ chúng trên một mặt phẳng mà không có các cạnh cắt nhau. Đây là 2 ví dụ kinh điển mà đồ thị của chúng là không phẳng:

- Bài toán Ba ngôi nhà ($K_{3,3}$): Đây là đồ thị lưỡng phân đầy đủ, nơi mỗi nút trong nhóm 3 nút này phải kết nối với tất cả các nút trong nhóm 3 nút kia.
- Bài toán Quadrapus ($K_5$): Đây là đồ thị đầy đủ với 5 nút, nơi mọi nút đều được kết nối trực tiếp với nhau.

Tuy nhiên, chúng ở trạng thái "suýt soát": Chỉ cần loại bỏ đúng một cạnh duy nhất, phần còn lại của đồ thị sẽ trở thành đồ thị phẳng.

![[II.55.png]]

Việc nghiên cứu tính phẳng có ứng dụng thực tiễn quan trọng trong tối ưu hóa bố cục bảng mạch điện tử (các đường dẫn điện không được phép chạm nhau), thiết kế sơ đồ luồng (flowcharts) và lập lịch trình, giúp giảm thiểu sự chồng chéo và tăng tính minh bạch cho các hệ thống dữ liệu phức tạp.

## 12.2 Definitions of Planar Graphs

Ở mục này có đưa ra định nghĩa: Một đồ thị được gọi là "phẳng" nếu bạn có thể vẽ nó sao cho các cạnh (được coi là các đường cong trơn) không cắt nhau. Tuy nhiên, "đường cong trơn" là một khái niệm thuộc về toán học liên tục và hình học, vốn rất phức tạp để định nghĩa chính xác. Và việc tin vào hình vẽ có thể dẫn đến những "chứng minh rác" (bogus proofs).

Do đó chúng ta định nghĩa đồ thị phẳng bằng toán học rời rạc thông qua cấu trúc dữ liệu đệ quy.

### 12.2.1 Faces

Khi bạn vẽ một đồ thị phẳng, các cạnh của nó chia mặt phẳng thành các vùng riêng biệt. Có những vùng nằm bên trong (hữu hạn) và luôn có một vùng bao quanh bên ngoài (vô hạn - gọi là outside face). Ta gọi nó là **continuous faces**.

Trong toán học rời rạc và lập trình, chúng ta không thể "vẽ" vùng vô hạn. Thay vào đó, chúng ta xác định mỗi mặt bằng chu trình các đỉnh (cycle) bao quanh mặt đó. Vì "chu trình" là một kiểu dữ liệu (list/array) mà máy tính có thể xử lý, tính toán và chứng minh. Đây gọi là **discrete faces**.

![[II.56.png]]

Trong các đồ thị phẳng phức tạp, ranh giới của một mặt không phải lúc nào cũng là một chu trình đơn giản (cycle). Sự xuất hiện của các cấu trúc như cạnh cầu (bridges) hoặc phần treo (dongles) buộc chúng ta phải mở rộng định nghĩa về mặt rời rạc. Thay vì chỉ sử dụng các chu trình đỉnh, **ranh giới của một mặt được xác định chính xác hơn dưới dạng các đường đi đóng (closed walks)**.

![[II.57.png]]

Như ở ví dụ trên thì ta định nghĩa theo đường sau: abcefgecda, đây không phải là chu trình, mà là một đường đi đóng.

![[II.58.png]]

Như hình này thì không định nghĩa dựa trên chu trình được ha ;v nên họ mới dùng closed walks.

### 12.2.2 A Recursive Definition for Planar Embeddings

Ý tưởng chính ở đây là sử dụng logic của các mặt (faces):

- Planar Embedding: Một tập hợp các đường đi đóng đại diện cho ranh giới của các mặt.
- Quy tắc xây dựng không giao cắt: Một cạnh mới có thể được vẽ mà không cắt các cạnh cũ nếu và chỉ nếu hai đầu mút của nó cùng nằm trên ranh giới của cùng một mặt.
- Cập nhật cạnh: Mỗi khi một cạnh mới được thêm vào, cấu trúc của các mặt sẽ thay đổi (một mặt cũ bị chia đôi thành hai mặt mới), và tập hợp các đường đi đóng này cần được cập nhật lại.

Mặc dù khái niệm tính phẳng áp dụng cho mọi đồ thị, nhưng định nghĩa đệ quy về Planar Embedding thường ưu tiên xét trên đồ thị liên thông để đảm bảo tính nhất quán trong việc xác định ranh giới các mặt. Việc giới hạn này cho phép mô tả quá trình xây dựng đồ thị thông qua các thao tác logic như 'chia mặt' (split a face) hoặc 'thêm cầu' (add a bridge). Đối với các đồ thị không liên thông, Planar Embedding có thể được hiểu là sự kết hợp của các thành phần liên thông riêng lẻ cùng chia sẻ một mặt ngoài vô hạn, đảm bảo rằng cấu trúc tổng thể vẫn tuân thủ các quy tắc.

Đây là định nghĩa chính thức. Một Planar Embedding của đồ thị liên thông là một tập hợp không rỗng các đường đi đóng (closed walks) được gọi là các mặt rời rạc (discrete faces). Cấu trúc này được xây dựng đệ quy thông qua các trường hợp sau:

- Base case: Nếu đồ thị $G$ chỉ gồm một đỉnh duy nhất $v$, Planar Embedding của $G$ có đúng một mặt rời rạc là đường đi đóng có độ dài bằng 0 tại chính đỉnh $v$.
- Trường hợp chia mặt (Split a face): Áp dụng khi thêm một cạnh mới nối hai đỉnh $a$ và $b$ đã tồn tại nhưng chưa kề nhau, với điều kiện cả hai cùng nằm trên một mặt rời rạc $\gamma$. Giả sử mặt $\gamma$ có dạng $\gamma = \alpha \widehat{} \beta$ (trong đó $\alpha$ là đường đi từ $a$ đến $b$, và $\beta$ là đường đi từ $b$ về $a$). hi thêm cạnh $\langle a—b \rangle$, mặt $\gamma$ sẽ bị thay thế bởi hai mặt rời rạc mới là: $$\alpha \widehat{} \langle b—a \rangle \quad \text{và} \quad \langle a—b \rangle \widehat{} \beta$$
- Trường hợp thêm cầu (Add a bridge): Áp dụng khi kết nối hai đồ thị liên thông rời rạc $G$ và $H$ bằng một cạnh mới $\langle a—b \rangle$. Giả sử $\gamma$ là một mặt của $G$ chứa đỉnh $a$, và $\delta$ là một mặt của $H$ chứa đỉnh $b$. Khi kết nối $G$ và $H$ bằng cạnh $\langle a—b \rangle$, hai mặt $\gamma$ và $\delta$ sẽ bị thay thế bởi một mặt mới duy nhất được gộp lại theo công thức: $$\gamma \widehat{} \langle a—b \rangle \widehat{} \delta \widehat{} \langle b—a \rangle$$

![[II.59.png]]

![[II.60.png]]

A bridge is simply a cut edge, but in the context of planar embeddings, the bridges are precisely the edges that occur twice on the same discrete face —as opposed to once on each of two faces. Dongles are trees made of bridges; we only use dongles in illustrations, so there’s no need to define them more precisely.

### 12.2.3 Does It Work?

Mối liên hệ giữa hình vẽ và lý thuyết Planar Embedding là một ví dụ điển hình của việc mô hình hóa các khái niệm hình học liên tục thành cấu trúc dữ liệu rời rạc. Mặc dù việc tư duy dựa trên hình vẽ mang tính trực quan cao, nhưng phương pháp Planar Embedding lại cung cấp một nền tảng toán học an toàn và chính xác hơn. Về cơ bản, một đồ thị được coi là phẳng khi mọi thành phần liên thông của nó đều có thể biểu diễn dưới dạng các tập hợp 'mặt' rời rạc.

### 12.2.4 Where Did the Outer Face Go?

Trong một bản vẽ trên giấy, chúng ta luôn thấy một vùng trống trải dài vô tận bao quanh đồ thị, gọi là mặt ngoài. Tuy nhiên, trong toán học nhúng phẳng (embedding), khái niệm "ngoài" hay "trong" chỉ là tương đối:

- Hai hình vẽ trông có vẻ khác nhau (vì có mặt ngoài khác nhau) thực chất có thể là cùng một Planar Embedding nếu chúng có chung các tập hợp chu trình ranh giới.
- Nếu bạn chọn một mặt bất kỳ, "chọc thủng" nó và kéo dãn lỗ thủng đó ra, mặt đó sẽ biến thành ranh giới bao quanh toàn bộ phần còn lại của đồ thị khi trải phẳng lên giấy, tức là nó có thể thành mặt ngoài.

=> Điều này giải thích tại sao thao tác "thêm cầu" (add bridge) luôn thực hiện được. Ta có thể chọn bất kỳ mặt nào từ hai đồ thị rời rạc để nối chúng lại, vì ta luôn có thể "biến" các mặt đó thành mặt ngoài để kết nối mà không sợ cắt qua các cạnh khác.

## 12.3 Euler’s Formula

Giá trị cốt lõi của việc định nghĩa đồ thị phẳng dưới dạng đệ quy nằm ở khả năng **áp dụng phương pháp quy nạp cấu trúc** để chứng minh các tính chất toán học. Phần này chứng minh định lí Euler cho đồ thị phẳng.

> [!INFO]
> If a connected graph has a planar embedding, then $v - e + f = 2$ where v is the number of vertices, e is the number of edges and f is the number of faces.

## 12.4 Bounding the Number of Edges in a Planar Graph

Sau đây là một số bổ đề:

- Trong một Planar Embedding, mỗi cạnh chỉ có hai khả năng: hoặc nó là "biên giới" chung của hai mặt khác nhau, hoặc nó là một "cạnh cầu" nằm trọn trong một mặt duy nhất (xuất hiện 2 lần trên ranh giới mặt đó).
- Nếu đồ thị có ít nhất 3 đỉnh, mỗi mặt phải được bao quanh bởi ít nhất 3 cạnh (tương đương với việc một đa giác tối thiểu phải là hình tam giác).

Dựa trên 2 bổ đề vừa rồi và định lí Euler, ta chứng minh được kết quả sau:

> [!INFO]
> Đối với bất kỳ đồ thị phẳng liên thông nào có $v \ge 3$, số cạnh $e$ không bao giờ vượt quá $3v - 6$.

## 12.5 Returning to K5 and K(3;3)

Đối với đồ thị đầy đủ $K_5$, số lượng cạnh vượt quá giới hạn $3v - 6$ cho phép đối với một đồ thị phẳng. Trong trường hợp đồ thị lưỡng phân $K_{3,3}$, do đặc tính không chứa chu trình tam giác, ranh giới các mặt phải có độ dài tối thiểu là 4, dẫn đến một định mức cạnh khắt khe hơn là $e \le 2v - 4$. Từ đó chứng minh được cả hai đồ thị này đều không phẳng.

## 12.6 Coloring Planar Graphs

Để đi tới định lý **Mọi đồ thị phẳng đều có thể tô bằng 5 màu**, tác giả đưa ra ba bổ đề:

- Any subgraph of a planar graph is planar.
- Khi bạn "nén" hai đỉnh đang nối với nhau thành một đỉnh duy nhất, đồ thị mới tạo ra vẫn giữ được tính phẳng.
- Trong bất kỳ đồ thị phẳng nào, luôn tồn tại ít nhất một đỉnh có bậc (số cạnh nối vào nó) nhỏ hơn hoặc bằng 5. Đây là hệ quả trực tiếp từ việc đồ thị phẳng không thể có quá nhiều cạnh ($e \le 3v - 6$).

![[II.61.png]]

## 12.7 Classifying Polyhedra

> [!INFO] Khối đa diện đều (Regular Polyhedron)
> Là các vật thể 3D có tất cả các mặt là các đa giác đều giống hệt nhau và tại mỗi đỉnh, số lượng các mặt gặp nhau là như nhau. Ví dụ: tứ diện (tetrahedron), lập phương (cube), và bát diện (octahedron).

> [!INFO] Phép chiếu lên mặt cầu (Spherical Projection)
> Đặt một mặt cầu bên trong khối đa diện và "chiếu" ranh giới các mặt của nó lên mặt cầu đó. Hành động này biến các cạnh của vật thể 3D thành các cung tròn trên mặt cầu, tạo thành một đồ thị phẳng.

![[II.62.png]]

![[II.63.png]]

Vì việc nhúng đồ thị trên mặt cầu tương đương với việc nhúng trên mặt phẳng, chúng ta có thể áp dụng công thức $V - E + F = 2$ cho các khối 3D này. Điều này cho phép chúng ta dùng toán học để giới hạn và tìm ra chính xác có bao nhiêu khối đa diện đều tồn tại.

Gọi $m$ là số mặt gặp nhau tại mỗi đỉnh (tương ứng với số cạnh đi ra từ mỗi nút trong đồ thị phẳng). $n$ là số cạnh của mỗi mặt.

- Mối quan hệ Đỉnh - Cạnh: Theo bổ đề bắt tay, ta có $mv = 2e$.
- Mối quan hệ Mặt - Cạnh: Vì mỗi cạnh là biên giới của 2 mặt, ta có $nf = 2e$.
- Thay vào công thức Euler: Khi đưa các giá trị $v$ và $f$ từ hai phương trình trên vào công thức $v - e + f = 2$, ta rút ra được phương trình giới hạn: $$\frac{1}{m} + \frac{1}{n} = \frac{1}{2} + \frac{1}{e}$$

Vì mỗi đa giác phải có ít nhất 3 cạnh ($n \ge 3$) và mỗi đỉnh phải là nơi gặp nhau của ít nhất 3 mặt ($m \ge 3$). Nếu cả $m$ và $n$ đều lớn (ví dụ cùng bằng 6), vế trái sẽ bằng $1/2$, khiến $1/e = 0$ (vô lý vì số cạnh $e$ phải là số hữu hạn). Việc thử các giá trị nguyên nhỏ cho $m$ và $n$ chỉ cho ra **đúng 5 bộ nghiệm thỏa mãn**, tương ứng với 5 khối Platonic.

## 12.8 Another Characterization for Planar Graphs

> [!INFO]
> (Kuratowski). A graph is not planar if and only if it contains K5 or K(3;3) as a minor
> A minor of a graph G is a graph that can be obtained by repeatedly deleting vertices, deleting edges, and merging adjacent vertices of G.
