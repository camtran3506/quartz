# 8. Number Theory
## 8.2 The Greatest Common Divisor (GCD)
### 8.2.2 The Pulverizer

![image](https://hackmd.io/_uploads/B17X8GRIWl.png)

![image](https://hackmd.io/_uploads/HJu1TGCLWe.png)

Với iff viết tắt cho "tương đương"

Có một cách thường dùng để tính GCD là thuật toán Euclid. Cùng với nó là Pulverizer, ý tưởng giống Euclid nhưng ghi lại linear combination của a và b ở từng bước.

![image](https://hackmd.io/_uploads/Byc_hMR8-e.png)

## 8.3 Prime Mysteries

![image](https://hackmd.io/_uploads/S1247XA8-g.png)

![image](https://hackmd.io/_uploads/ryT5X7RL-g.png)

Từ công thức $\pi(x) \approx \frac{x}{\ln x}$, ta có thể suy ra: Nếu bạn chọn ngẫu nhiên một số nguyên trong khoảng từ $1$ đến $x$, xác suất để số đó là số nguyên tố là khoảng:$$\frac{1}{\ln x}$$

## 8.4 The Fundamental Theorem of Arithmetic

![image](https://hackmd.io/_uploads/HkFnd7C8bl.png)

## 8.5 Alan Turing
### 8.5.1 Turing’s Code (Version 1.0)

Trước khi mã hóa thì ta phải số hóa thông điệp trước. Tức là chuyển text thành number.

Ví dụ: Chữ "victory" được ghép lại thành một con số khổng lồ: 22090320151825.

Trong mã của Turing, thông điệp $m$ phải là một số nguyên tố. Nếu số $m$ sau khi đổi từ chữ sang số không phải là số nguyên tố, ta sẽ thêm vài chữ số vào đuôi (padding) cho đến khi tìm được một số nguyên tố.
=> **Prime Number Theorem nói rằng số nguyên tố không quá hiếm.** Vì vậy, ta không cần phải thử quá nhiều lần; chỉ cần thêm vài chữ số (như số 13 trong ví dụ) là xác suất tìm được số nguyên tố là rất cao.

![image](https://hackmd.io/_uploads/H1dI44AIbg.png)

**Kiểm tra tính nguyên tố (Primality Testing)**
Câu hỏi đặt ra là: "Làm sao để chắc chắn $m$ và $k$ là số nguyên tố?". Nếu bạn chọn đại một số cực lớn (ví dụ có 500 chữ số), làm sao bạn biết nó là số nguyên tố hay là hợp số?

Tác giả nhấn mạnh rằng việc kiểm tra một số có phải nguyên tố hay không thực ra "dễ" hơn nhiều so với việc phân tích nó. Hiện nay, chúng ta có các thuật toán như Miller-Rabin (thuật toán xác suất cực nhanh) hoặc AKS (thuật toán đa thức chắc chắn).

**Tại sao quân Phát xít lại "bó tay"? (Độ an toàn)**
Hệ thống này dựa trên một thứ gọi là Hàm một chiều (One-way function): Bạn có $m$ và $k$ (hai số nguyên tố cực lớn). Việc nhân chúng lại để tạo ra $m_b = m \times k$ là cực kỳ nhanh chóng, ngay cả với máy tính yếu.  Kẻ địch chỉ có $m_b$. Để tìm lại thông điệp $m$, chúng buộc phải phân tích thừa số nguyên tố (factorize) số $m_b$.

Như đã đề cập ở phần trước, chưa ai tìm ra một thuật toán chạy trong "thời gian đa thức" để phân tích một số là tích của hai số nguyên tố lớn.

### 8.5.2 Breaking Turing’s Code (Version 1.0)

Khi bạn gửi hai tin nhắn $m_1$ và $m_2$ với cùng một khóa $k$:
Tin nhắn 1: $m_{c1} = m_1 \times k$
Tin nhắn 2: $m_{c2} = m_2 \times k$

Quân Phát xít (kẻ tấn công) bây giờ có hai con số $m_{c1}$ và $m_{c2}$. Chúng không cần phải phân tích thừa số nguyên tố (bài toán khó) nữa. Thay vào đó, chúng chỉ cần tìm Ước chung lớn nhất (GCD). Theo tính chất của GCD:$$gcd(m_{c1}, m_{c2}) = gcd(m_1 \cdot k, m_2 \cdot k) = k \cdot gcd(m_1, m_2)$$Vì $m_1$ và $m_2$ là các số nguyên tố khác nhau (theo quy định của mã Turing), nên $gcd(m_1, m_2) = 1$. Kết quả là:$$gcd(m_{c1}, m_{c2}) = k$$

## 8.8 Turing’s Code (Version 2.0)

![image](https://hackmd.io/_uploads/S10D-eyDWe.png)

Vì m_hat lúc này là một số dư trong khoảng 0 đến n, nên ta không thể tính m bằng cách lấy m_hat chia cho k được.

## 8.9 Multiplicative Inverses and Cancelling

![image](https://hackmd.io/_uploads/HyihwxkvWe.png)

Ở đây đang nói đến nghịch đảo modulo. Vì 2.8 = 16 mà chia dư cho 15 được 1 nên gọi 8 là nghịch đảo của 2.

### 8.9.1 Relative Primality

![image](https://hackmd.io/_uploads/B114_e1wWe.png)

![image](https://hackmd.io/_uploads/HJsNOgJDbe.png)

Vành $\mathbb{Z}_n$ là một cấu trúc cơ bản trong toán học, chứa các số dư có thể có khi thực hiện phép chia một số nguyên bất kỳ cho $n$.

Trong vành $\mathbb{Z}_n$ thì dấu = đại diện cho dấu modulo (chia dư) nha. Phần chứng minh Lemma 8.9.1 thì ý tưởng dựa trên gcd(k, n) = linear combination của k và n.

Khi $p$ là số nguyên tố, vành $\mathbb{Z}_p$ trở thành một Trường (Field). Đặc điểm tuyệt vời nhất của nó là:
* Mọi số khác $0$ đều có nghịch đảo
* Nếu $a \cdot b = 0$, thì chắc chắn $a = 0$ hoặc $b = 0$.

Khi $n$ là hợp số (ví dụ $n = 6, 15, 20$), $\mathbb{Z}_n$ chỉ là một vành. 
* Chỉ những số nào "nguyên tố cùng nhau" với $n$ ($\gcd(a, n) = 1$) mới có nghịch đảo.
* Hai số khác $0$ nhân với nhau lại có thể bằng $0$!

### 8.9.2 Cancellation

Trong số thực hay số hữu tỉ, nếu bạn có $t \cdot r = t \cdot s$ và $t \neq 0$, bạn hiển nhiên suy ra $r = s$. Nhưng trong $\mathbb{Z}_n$, bạn không thể làm điều tương tự.

![image](https://hackmd.io/_uploads/H1WdJ-yw-l.png)

Bạn chỉ có thể triệt tiêu $t$ trong phương trình $t \cdot r = t \cdot s \pmod n$ nếu và chỉ nếu $t$ có nghịch đảo modulo $n$ (tức là $\gcd(t, n) = 1$).

![image](https://hackmd.io/_uploads/rkCcJ-ywWe.png)

### 8.9.3 Decrypting (Version 2.0)

![image](https://hackmd.io/_uploads/BJavZW1PZg.png)

### 8.9.4 Breaking Turing’s Code (Version 2.0)

Đối với mã Turing Version 2.0, giả sử quân Phát xít thu thập được:
* $m$: Bản rõ (nội dung tin nhắn gốc).
* $\hat{m}$ (trong sách viết là $mb$): Bản mã tương ứng.
* $n$: Số modulo công khai.

Để tìm $k$, quân Phát xít chỉ cần "loại bỏ" $m$ khỏi vế phải. Trong số học thông thường, ta sẽ chia cho $m$. Trong vành $\mathbb{Z}_n$, chúng sử dụng công cụ gọi là The Pulverizer (Thuật toán Euclid mở rộng) để tìm số nghịch đảo của $m$. Sau khi tìm xong thì decrypt một cách bình thường như trên.

**Tác giả nhận định Version 2.0 là "vô giá trị".** Một hệ thống mật mã thực tế phải đảm bảo rằng dù kẻ tấn công có biết hàng ngàn cặp $(m, \hat{m})$, chúng vẫn không thể tìm ra khóa $k$ trong thời gian cho phép. Một khi $k$ bị lộ, toàn bộ các tin nhắn trong quá khứ và tương lai (sử dụng cùng khóa $k$) đều bị giải mã hoàn toàn.

## 8.10 Euler’s Theorem

![image](https://hackmd.io/_uploads/SyEpc-kwWg.png)

![image](https://hackmd.io/_uploads/HkmbobywWl.png)

Trong vành $\mathbb{Z}_n$, nghịch đảo của $k$ chính là $k^{\phi(n)-1}$. Đây là một ứng dụng thực tế giúp tìm số nghịch đảo mà không cần The Pulverizer.

![image](https://hackmd.io/_uploads/ByaVrV1PWe.png)

### 8.10.1 Computing Euler's Phi Function

![image](https://hackmd.io/_uploads/ryvxdE1v-e.png)

![image](https://hackmd.io/_uploads/HJvjuV1v-e.png)

![image](https://hackmd.io/_uploads/HJveKEkPbe.png)

Các bạn để ý thấy các phần này toàn chụp định nghĩa và định lí các thứ, thì nó vậy đó :-1: Về chứng minh thì nếu ai đã từng học qua chương trình THPT cho chuyên toán thì chắc đều biết rồi nên tôi nhắc lại thôi.

## 8.11 RSA Public Key Encryption
Khác với mã Turing (nơi người gửi và nhận phải gặp nhau lén lút để trao đổi khóa $k$), RSA cho phép giao dịch an toàn mà không cần gặp mặt trước:
* **Public Key (Khóa công khai):** Được phân phối rộng rãi. Ai cũng có thể dùng nó để mã hóa tin nhắn gửi cho bạn.
* **Private Key (Khóa bí mật):** Bạn giữ riêng cho mình. Chỉ có khóa này mới giải mã được những gì đã mã hóa bằng khóa công khai tương ứng.

Như bạn đã nhận thấy ở mã Turing Ver 2.0, việc chỉ nhân $m \cdot k \pmod n$ rất dễ bị bẻ gãy. RSA đã nâng cấp phép toán này:
* **Mã hóa:** Thay vì nhân, RSA nâng tin nhắn lên một lũy thừa bí mật.
* **Modulo:** RSA không hoạt động trên số nguyên tố $p$, mà hoạt động trên số $n = p \cdot q$ (tích của hai số nguyên tố khổng lồ).

Đoạn văn khẳng định Định lý Euler là trung tâm để hiểu RSA. Lý do là:
* RSA cần một cách để "đảo ngược" phép lũy thừa mà không cần thực hiện phép chia (vì trong $\mathbb{Z}_n$ không có phép chia thông thường).
* Nếu tin nhắn $m$ nguyên tố cùng nhau với $n$ ($\gcd(m, n) = 1$), Định lý Euler $m^{\phi(n)} \equiv 1 \pmod n$ giúp chúng ta tìm ra một số mũ $d$ sao cho khi nâng bản mã lên lũy thừa $d$, ta quay lại được tin nhắn gốc $m$.

![image](https://hackmd.io/_uploads/r1AEgHJwWl.png)

Sự bảo mật của hệ thống RSA không dựa trên một chứng minh toán học tuyệt đối rằng nó "không thể bị phá vỡ", mà dựa trên một giả thuyết về độ khó của việc tính toán và sự bền bỉ của nó trước thời gian. Cốt lõi bảo mật của RSA nằm ở giả thuyết rằng việc phân tích một số nguyên thành tích của hai số nguyên tố lớn (mỗi số dài hàng trăm chữ số) là một việc "khó khăn đến tuyệt vọng".

## 8.12 What has SAT got to do with it?
Mối đe dọa lớn nhất đối với RSA không đến từ các phép thử trực tiếp mà đến từ khả năng chuyển đổi bài toán phân tích số thành bài toán logic (SAT) thông qua các mạch kỹ thuật số.
* **Mạch kiểm tra tích (Product Checker):** Chúng ta có thể xây dựng một mạch điện sử dụng các cổng logic (AND, OR, NOT) để kiểm tra xem liệu $i \cdot j = k$. Mạch này chỉ yêu cầu số lượng cổng logic tỉ lệ thuận với $n^2$.
* **Chuyển đổi sang Logic:** Mọi mạch điện kỹ thuật số đều có thể được mô tả bằng các công thức logic có kích thước tương đương. Do đó, việc tìm các giá trị đầu vào cho mạch chính là giải bài toán SAT.

Nếu tồn tại một bộ giải SAT (SAT Solver) hiệu quả, việc phân tích thừa số một số $m$ khổng lồ sẽ được thực hiện qua $n$ lần thử như sau:
1. **Cố định giá trị mục tiêu:** Thiết lập đầu vào $k$ của mạch bằng đúng giá trị $m$ cần phân tích.
2. **Dò tìm từng bit của thừa số:**
* Thử đặt bit đầu tiên của thừa số $i$ là $1$.
* Sử dụng máy giải SAT để kiểm tra xem có tồn tại các giá trị bit còn lại của $i$ và $j$ để thỏa mãn mạch điện không.
* Nếu máy giải SAT trả về "Có", ta giữ bit đó là $1$; nếu không, ta đặt nó là $0$.
3. **Lặp lại:** Tiếp tục thực hiện tương tự cho đến bit cuối cùng của $i$. Sau $n$ bước, chúng ta tìm ra thừa số $i$ hoàn chỉnh.

**Nếu bài toán SAT có thể được giải trong thời gian đa thức (Polynomial time), thì bài toán phân tích thừa số nguyên tố cũng có thể được giải trong thời gian đa thức.**

# 9. Directed graphs & Partial Orders
## 9.3 Adjacency Matrices

Đây là khái niệm ma trận kề mà các bạn đã gặp trong môn DSA, ở phần đồ thị á, để biểu diễn giữa 2 đỉnh có kề hay không. Nếu có kề thì c_ij = 1, không kề thì nó = 0. Ta mở rộng khái niệm này ra một chút.

![image](https://hackmd.io/_uploads/r1LttHgD-e.png)

Mỗi ô ở hàng $u$, cột $v$ (ký hiệu là $C_{uv}$) cho bạn biết có bao nhiêu cách để đi từ đỉnh $u$ đến đỉnh $v$ trong đúng $k$ bước.
* Độ dài $k=1$: Chính là Ma trận kề (Adjacency Matrix - $A_G$). Nếu có cạnh nối trực tiếp từ $u$ đến $v$, giá trị là 1 (có 1 bước đi), nếu không là 0.
* Độ dài $k=0$: Chính là Ma trận đơn vị ($I$). Bạn chỉ có thể ở yên tại chỗ (từ $u$ đến chính nó) trong 0 bước. Vì vậy, các ô trên đường chéo chính là 1, các ô khác là 0.

![image](https://hackmd.io/_uploads/SJBq5HxDbx.png)

Định lý này nói rằng: Nếu bạn nhân ma trận đếm bước đi độ dài $k$ ($C$) với ma trận đếm bước đi độ dài $m$ ($D$), kết quả sẽ là ma trận đếm bước đi độ dài $k + m$.

Từ định lý này, chúng ta có một quy tắc cực kỳ hữu ích: **Lũy thừa của ma trận kề cho biết số bước đi.**

![image](https://hackmd.io/_uploads/HksQsrlvbg.png)

### 9.3.1 Shortest Paths
Ý tưởng rất đơn giản: Để tìm khoảng cách giữa đỉnh $u$ và đỉnh $v$, bạn cứ lũy thừa ma trận kề $A_G$ lên dần dần ($A^1, A^2, A^3, \dots$) và "canh chừng" (watching). Đến khi nhận thấy ô $(u, v) > 0$ lần đầu tiên thì khoảng cách ngắn nhất đúng bằng số mũ của ma trận.

Trong một đồ thị có $n$ đỉnh, một đường đi ngắn nhất (không đi vòng lại) chỉ có thể có tối đa là $n-1$ cạnh. Nếu bạn đã tính đến $A^{n-1}$ mà ô $(u, v)$ vẫn bằng 0, thì kết luận luôn: **Không có đường đi nào nối giữa $u$ và $v$ cả**.

Ý tưởng này là nền tảng cho **Đồ thị có trọng số** (Weighted Graphs) và các thuật toán tối ưu khác **(BFS cho đồ thị không trọng số, hoặc Dijkstra/Floyd-Warshall cho đồ thị có trọng số.)**

## 9.4 Walk Relations
Phần này bàn về việc, xác định giữa 2 đỉnh xem liệu có một đường đi nào từ đỉnh u sang đỉnh v hay không.

![image](https://hackmd.io/_uploads/B1TP78lDWx.png)

### 9.4.1 Composition of Relations

Nhớ rằng, một đồ thị có hướng $G$ trên tập đỉnh $V$ thực chất chỉ là một tập hợp các cặp $(a, b)$ mà trong đó có một mũi tên đi từ $a$ đến $b$. Hay nói cách khác là quan hệ hai ngôi.

![image](https://hackmd.io/_uploads/S19EdLePbl.png)

Để đi từ $a$ đến $c$, bạn phải tìm được một "trạm trung chuyển" $b$ sao cho $a$ đến được $b$ và $b$ đến được $c$.

Bây giờ, thay vì $R$ và $S$, chúng ta lấy $G$ hợp thành với chính nó ($G \circ G$, ký hiệu là $G^2$):
* $a G^2 c$ có nghĩa là: Có một đỉnh $b$ sao cho $a \to b$ và $b \to c$.
* $a \to b \to c$ chính là một bước đi độ dài 2.

![image](https://hackmd.io/_uploads/H1cUi8xPZg.png)

![image](https://hackmd.io/_uploads/B1NHAIgw-e.png)

$G^0$ là Quan hệ đồng nhất (Identity relation): Nghĩa là mỗi đỉnh tự kết nối với chính nó.

Định nghĩa $G^*$ là quan hệ bước đi: "$u$ có thể đến được $v$". Để điều này đúng, thì: Bạn có thể đến trong 0 bước (đứng yên tại chỗ: $G^0$) HOẶC bạn đến trong đúng 1 bước ($G^1$) HOẶC bạn đến trong đúng 2 bước ($G^2$)...

**Kĩ thuật Repeated Squaring**

Hãy gọi $R = G \cup G^0$. Quan hệ $R$ có nghĩa là: "Đi được từ $u$ đến $v$ trong 0 HOẶC 1 bước".

khi chúng ta hợp thành $R$ với chính nó ($R^2$):
* $R^2 = (G \cup G^0) \circ (G \cup G^0)$
* Theo tính chất phân phối, nó bao gồm: $G^0 \circ G^0 = G^0$ (0 bước) ; $G^0 \circ G = G^1$ (1 bước) ; $G \circ G^0 = G^1$ (1 bước) ; $G \circ G = G^2$ (2 bước)
* Vậy $R^2 = G^0 \cup G^1 \cup G^2$ (Nghĩa là: đi được trong **tối đa** 2 bước).

Tương tự như vậy, $R^{n-1}$ sẽ là tất cả các đường đi có độ dài **tối đa** $n-1$ bước.

## 9.5 Directed Acyclic Graphs & Scheduling

> [!INFO]
> A directed acyclic graph (DAG) is a directed graph with no cycles.

DAG là "xương sống" của nhiều hệ thống:
* **Lập lịch công việc (Task Scheduling):** Nếu bạn có 10 việc cần làm trên một máy tính có nhiều chip xử lý, DAG sẽ cho bạn biết việc nào có thể làm song song, việc nào phải đợi việc kia xong (Concurrency control).
* **Quản lý mã nguồn:** Các công cụ như Make, Gradle hay Bazel dùng DAG để biết phần nào của code cần biên dịch trước.
* **Excel:** Khi bạn đặt công thức ô C1 = A1 + B1, Excel tạo ra một DAG để biết phải tính ô nào trước khi dữ liệu thay đổi.

### 9.5.1 Scheduling

> [!INFO]
> A **topological sort** of a finite DAG is a list of all the vertices such that each vertex v appears earlier in the list than every other vertex reachable from
v.

> [!INFO]
> An vertex v of a DAG, D, is minimum iff every other vertex is reachable from v.
> A vertex v is minimal iff v is not reachable from any other vertex.

**Cách tạo một sắp xếp Topo:**
* Tìm các phần tử Minimal
* Chọn một trong số đó, giả sử là $u$
* Loại bỏ $u$ và các cạnh nối nó ra khỏi đồ thị
* Trong những đỉnh $v$ mà $u \to v$, ta tìm các phần tử Minimal mới
* Tiếp tục cho đến khi chọn được hết các đỉnh

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

Đây là cách lập lịch nhanh nhất có thể (với giả định bạn có vô hạn máy tính/nhân lực): Việc gì có độ sâu bằng $k$ thì hãy làm nó ngay ở bước thứ $k$. Nó giống hệt cách tôi giải thích trước đó, chỉ khác góc nhìn thôi. Hiểu rằng độ sâu $k$ này có nghĩa là cần làm $k$ việc trước rồi mới tới $a$.

### 9.5.3 Dilworth’s Lemma (Optional)

> [!INFO]
> An antichain in a DAG is a set of vertices such that no two elements in the set are comparable—no walk exists between any two different vertices in the set.

> [!INFO]
> In a DAG, $D$, if the size of the largest chain is $t$, then $V(D)$ can be partitioned into t antichains.

![image](https://hackmd.io/_uploads/S1pjyYgwbl.png)

## 9.6 Partial Orders

Gọi là quan hệ thứ tự một phần, nhưng chắc bạn quên nên tôi nhắc lại.

### 9.6.1 The Properties of the Walk Relation in DAGs

![image](https://hackmd.io/_uploads/SJVqXYgPWg.png)

![image](https://hackmd.io/_uploads/ByDoQYewbl.png)

![image](https://hackmd.io/_uploads/HkDaXtxPZe.png)

### 9.6.2 Strict Partial Orders

![image](https://hackmd.io/_uploads/H1VrLYgPWl.png)

For example, the less-than order, <, on numbers is a strict partial order.

![image](https://hackmd.io/_uploads/H1dEKFewWl.png)

Quan hệ thứ tự một phần (Strict Partial Order) quan tâm đến việc: "A có đứng trước C hay không?". Nó không quan tâm bạn đi đến đó bằng 1 bước hay 10 bước. Do đó **nhiều DAG có thể tạo ra cùng một quan hệ thứ tự một phần.**
=> Tìm một DAG có ít cạnh nhất để biểu diễn một quan hệ thứ tự, bỏ hết các cạnh thừa. 

### 9.6.3 Weak Partial Orders

![image](https://hackmd.io/_uploads/HJ8R5YlDbl.png)

![image](https://hackmd.io/_uploads/BJEPjKlvbl.png)

Hoặc ta có thể định nghĩa thông qua Strict Partial Orders như sau:

![image](https://hackmd.io/_uploads/rJ2ojtgP-l.png)

For example, <=, on numbers is a strict partial order.

## 9.7 Representing Partial Orders by Set Containment

![image](https://hackmd.io/_uploads/Syfn6KxDWl.png)

Nếu $a$ có quan hệ với $a'$ trong thế giới này, thì bản sao của chúng là $f(a)$ và $f(a')$ cũng phải có quan hệ tương ứng trong thế giới kia.

**Làm sao để biến một thứ tự bất kỳ thành quan hệ tập con?** Hãy đại diện mỗi phần tử $a$ bằng tập hợp của tất cả những kẻ đứng trước nó (bao gồm cả chính nó).

$$a \to \{b \in A \mid b \preceq a\}$$

Ví dụ:
* Số 3 được đại diện bởi tập các số chia hết cho nó trong tập đã cho: $\{1, 3\}$.
* Số 12 được đại diện bởi tập: $\{1, 3, 4, 6, 12\}$.
* Vì $3$ chia hết cho $12$, nên chắc chắn mọi số chia hết cho $3$ cũng phải chia hết cho $12$. Do đó: 

$$\{1, 3\} \subseteq \{1, 3, 4, 6, 12\}$$

![image](https://hackmd.io/_uploads/r1CoRFgw-x.png)

## 9.8 Linear Orders
Thứ tự Tuyến tính (Linear Order), hay còn gọi là Thứ tự Toàn phần (Total Order). Một quan hệ thứ tự một phần được gọi là tuyến tính nếu: **Mọi cặp phần tử khác nhau đều có thể so sánh được.** Đối với Partial Order thì có tồn tại các phần tử mà không so sánh với nhau được.

Ví dụ: Quan hệ tập con ($\subseteq$) là một phần, quan hệ < là toàn phần

## 9.9 Product Orders
**Tích của các quan hệ (Product of Relations)**—một cách để kết hợp hai hệ thống thứ tự cũ thành một hệ thống mới phức tạp hơn.

Cặp $(a_1, a_2)$ có quan hệ với cặp $(b_1, b_2)$ khi và chỉ khi cả hai điều kiện sau đều đúng:
* $a_1$ có quan hệ với $b_1$ trong hệ thống thứ nhất ($R_1$).
* $a_2$ có quan hệ với $b_2$ trong hệ thống thứ hai ($R_2$).

Nếu $R_1$ và $R_2$ là các Thứ tự một phần (Partial Orders), thì tích của chúng cũng là một thứ tự một phần. Tích của hai thứ tự tuyến tính KHÔNG nhất thiết là thứ tự tuyến tính.

> [!INFO]
> Khá giống tích Descartes (hoặc Cartesian) giữa 2 tập hợp ha ;v
## 9.10 Equivalence Relations

![image](https://hackmd.io/_uploads/r1zm-5xPWe.png)

Ví dụ về quan hệ tương đương cũng nhiều, nhưng đây là một ví dụ khá tổng quát, tạo ra quan hệ dựa trên một hàm số.

![image](https://hackmd.io/_uploads/SkEef9lPZx.png)

Hai phần tử $a$ và $a'$ có quan hệ với nhau khi và chỉ khi kết quả của chúng qua hàm $f$ là như nhau.
=> **Một quan hệ là quan hệ tương đương khi và chỉ khi nó có thể được biểu diễn dưới dạng $\equiv_f$ của một hàm số nào đó.**

### 9.10.1 Equivalence Classes

Tôi sẽ không chụp định nghĩa vào đây mà so sánh nó với một khái niệm đã làm quen từ trước: **phân hoạch của tập hợp**. **Quan hệ tương đương và Phân hoạch thực chất là hai cách nhìn cho cùng một vấn đề.**

**Phân hoạch $\to$ Quan hệ tương đương:** Nếu bạn chủ động chia một tập hợp thành các khối (blocks) không chồng lấn, thì việc "ở chung một khối" nghiễm nhiên là một quan hệ tương đương.

**Quan hệ tương đương $\to$ Phân hoạch:** Nếu bạn có một quan hệ tương đương, các lớp tương đương của nó sẽ tự động "cắt" tập hợp của bạn thành các khối hoàn hảo.

Ví dụ: Bạn có một túi bi nhiều màu. Nếu quan hệ tương đương là "có cùng màu", thì lớp tương đương của một viên bi Xanh chính là tập hợp tất cả các viên bi Xanh trong túi đó.

# 10. Communication Networks (Optional)

Việc thiết kế mạng được chuyển đổi sang ngôn ngữ đồ thị có hướng (digraphs) để tính toán. Ta cần nắm các khái niệm sau:

* **Gói tin (Packet):** Đơn vị dữ liệu kích thước cố định (ví dụ 256 hoặc 4096 bytes).
* **Điểm đầu cuối (Terminal):** Nơi bắt đầu (Source) và kết thúc (Destination) của gói tin.
* **Bộ chuyển mạch (Switches):** Nút trung gian điều hướng gói tin từ cạnh vào đến cạnh ra.
* **Bài toán Định tuyến (Routing Problem):** Một hoán vị $\pi$ xác định gói tin từ đầu vào $i$ phải tới đầu ra $\pi(i)$.
* **Phương án Định tuyến ($P$):** Tập hợp các đường đi cụ thể giải quyết hoán vị $\pi$.
* **Độ trễ:** Số lượng dây dẫn (cạnh) mà gói tin phải đi qua.
* **Đường kính (Diameter):** Chiều dài của đường đi ngắn nhất giữa cặp đầu vào - đầu ra xa nhau nhất. Đại diện cho độ trễ trong trường hợp xấu nhất.
* **Độ trễ mạng (Latency):** Là chiều dài của đường đi dài nhất trong một phương án định tuyến tối ưu nhất. Trong cấu trúc cây, Latency thường bằng Diameter vì đường đi là duy nhất.
* **Sự tắc nghẽn (Congestion):** Số lượng đường đi tối đa cùng chạy qua một Switch đơn lẻ trong một phương án định tuyến. Congestion càng cao, gói tin càng dễ bị chậm trễ tại các switch bị quá tải.

## 10.3 Network Diameter

Một cách để giảm đường kính của một mạng lưới là sử dụng các bộ chuyển mạch (switches) lớn hơn. Tuy nhiên, điều này không mang lại nhiều hiệu quả. Việc sử dụng một bộ chuyển mạch $N \times N$ sẽ chỉ che giấu bài toán thiết kế mạng ban đầu bên trong bộ chuyển mạch trừu tượng này. Cuối cùng, chúng ta sẽ phải thiết kế cấu trúc bên trong của bộ chuyển mạch quái vật đó bằng các thành phần đơn giản hơn, và thế là chúng ta lại quay trở về vạch xuất phát. Vì vậy, thách thức trong việc thiết kế một mạng truyền thông là tìm ra cách để đạt được chức năng của một bộ chuyển mạch $N \times N$ bằng cách sử dụng các thiết bị cơ bản, kích thước cố định, chẳng hạn như bộ chuyển mạch $3 \times 3$. 

## 10.4 Switch Count

Một mục tiêu khác trong việc thiết kế mạng truyền thông là sử dụng càng ít bộ chuyển mạch (switches) càng tốt. Số lượng bộ chuyển mạch trong một cây nhị phân hoàn chỉnh là $2N - 1$, đây là mức gần như tốt nhất có thể đạt được đối với các bộ chuyển mạch $3 \times 3$.

## 10.6 Congestion

Cây nhị phân hoàn chỉnh có một nhược điểm chí tử: bộ chuyển mạch gốc (root switch) là một nút thắt cổ chai. Ở điều kiện tốt nhất, bộ chuyển mạch này phải xử lý tất cả các gói tin đi từ nửa trái sang nửa phải và ngược lại. Trong trường hợp xấu nhất, nếu bộ chuyển mạch này hỏng, mạng lưới sẽ bị chia cắt thành hai phần có kích thước bằng nhau.

Bằng cách mở rộng khái niệm tắc nghẽn cho mạng lưới, chúng ta cũng có thể phân biệt giữa mạng 'tốt' và 'xấu' liên quan đến các vấn đề thắt nút. Đối với mỗi bài toán định tuyến $\pi$, chúng ta giả định một phương án định tuyến được chọn để tối ưu hóa sự tắc nghẽn (tức là có sự tắc nghẽn tối thiểu). Khi đó, mức độ tắc nghẽn lớn nhất mà một bộ chuyển mạch phải chịu đựng sẽ là mức tắc nghẽn tối đa trong số các định tuyến tối ưu này. **Mức tắc nghẽn 'maximin' này được gọi là sự tắc nghẽn của mạng**.

## 10.7 2-D Array

![image](https://hackmd.io/_uploads/SysiI4Xwbe.png)

The diameter of an array with $N$ inputs and outputs is $2N$, which is much worse than the diameter of $2 \log N + 2$ in the complete binary tree. But we get something in exchange: **replacing a complete binary tree with an array almost eliminates congestion**.

## 10.8 Butterfly

**Butterfly Network** giữ được đường kính ngắn gần như cây nhị phân, nhưng lại phân tán luồng dữ liệu tốt hơn để tránh tắc nghẽn cực đoan. Tuy nhiên, nó không hội tụ được những đặc tính tốt nhất của mỗi loại mạng, mà đúng hơn, nó là một sự thỏa hiệp nằm đâu đó ở giữa hai loại mạng này.

Ta định nghĩa theo kiểu đệ quy:
* **Trường hợp cơ sở ($F_1$):** Là mạng nhỏ nhất với 2 đầu vào và 2 đầu ra. Các switch được nối chéo nhau tạo thành hình chữ X (giống cánh bướm).
* **Bước dựng ($F_{n+1}$):** Để tạo ra một mạng lớn hơn, người ta lấy hai mạng nhỏ ($F_n$) và đặt thêm một hàng switch mới ở phía trước. Mỗi switch mới sẽ nối với một switch tương ứng ở mạng $F_n$ phía trên và một ở mạng $F_n$ phía dưới. **Chính cách nối "chéo" này giúp dữ liệu từ bất kỳ đầu vào nào cũng có thể tìm đường sang bất kỳ đầu ra nào mà không nhất thiết phải đi qua một "nút gốc" duy nhất.**

![image](https://hackmd.io/_uploads/rkH9k87Pbx.png)

![image](https://hackmd.io/_uploads/BkFiyUQvZl.png)

Đây là thuật toán Routing, cũng được định nghĩa theo kiểu đệ quy
* **Trường hợp cơ sở ($F_1$):** Chỉ có 2 đầu vào và 2 đầu ra. Đường đi là hiển nhiên.
* **Bước đệ quy ($F_{n+1}$):** Khi gói tin đang ở một switch đầu vào của mạng lớn ($F_{n+1}$): Nếu đích đến (output) nằm ở nhóm phía trên (top copy), gói tin sẽ nhảy vào cổng kết nối với mạng $F_n$ phía trên. Nếu đích đến nằm ở nhóm phía dưới (bottom copy), gói tin sẽ nhảy vào mạng $F_n$ phía dưới. Sau khi đã vào được mạng $F_n$ tương ứng, quy trình này lặp lại cho đến khi gói tin chạm đích.

Một đặc điểm quan trọng là: **Giữa bất kỳ đầu vào $i$ và đầu ra $j$ nào, chỉ tồn tại duy nhất một con đường**.

## 10.9 Beneš Network

Ý tưởng của Beneš cực kỳ đơn giản: **Ghép hai mạng Butterfly lại với nhau theo kiểu đối lưng (back-to-back).** Nếu mạng Butterfly chỉ cho phép dữ liệu đi theo một hướng đệ quy duy nhất, thì mạng Benes tạo ra một cấu trúc đối xứng.

Đây là định nghĩa đệ quy:
* **Trường hợp cơ sở ($B_1$):** Giống hệt $F_1$ (Butterfly cấp 1)
* **Bước dựng ($B_{n+1}$):** Được tạo ra từ hai mạng $B_n$ nhỏ hơn. Thêm một cột switch mới ở phía trước (đầu vào). Thêm một cột switch mới ở phía sau (đầu ra). Mỗi switch mới ở đầu vào nối với hai mạng $B_n$ bên trong, và mỗi switch mới ở đầu ra cũng nhận tín hiệu từ hai mạng $B_n$ đó.

![image](https://hackmd.io/_uploads/rkJnF8QD-l.png)

Đến đây, chúng ta đã có một cái nhìn toàn cảnh về sự tiến hóa của các mô hình mạng:

![image](https://hackmd.io/_uploads/BJJDq8XPZg.png)

# 11. Simple Graphs
