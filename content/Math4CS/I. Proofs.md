# 1. What is a Proof?

Nội dung chủ yếu là giới thiệu về mệnh đề, các tiên đề, các cách chứng minh mệnh đề từ tiên đề hoặc mệnh đề đã chứng minh trước đó (trực tiếp, gián tiếp, phản chứng, phản đề, chứng minh chia trường hợp và chứng minh tương đương) giống với phần đầu môn **Cấu trúc Rời rạc ở UIT**. Ngoài ra **mục 1.10** còn giới thiệu một số tips để viết chứng minh dễ hiểu, rõ ràng hơn.

# 2. The Well Ordering Principle

> [!INFO]
> Every nonempty set of nonnegative integers has a smallest element.

**WOP** thường được dùng để tạo ra một sự mâu thuẫn nhằm chứng minh một tính chất nào đó **đúng cho mọi số nguyên**.

**Quy trình chứng minh bằng Well Ordering Principle (WOP)**

Để chứng minh một tính chất $P(n)$ đúng với mọi số nguyên không âm $n \in \mathbb{N}$, bạn thực hiện theo các bước:

- **Bước 1 Định nghĩa tập các "phần tử lỗi" ($C$):** Bạn thiết lập một tập hợp $C$ chứa tất cả các số nguyên $n$ làm cho $P(n)$ bị sai (các trường hợp phản ví dụ).
- **Bước 2 Phản chứng:** Giả sử tập $C$ này không rỗng (tức là giả sử có tồn tại ít nhất một số $n$ làm cho tính chất $P$ bị sai).
- **Bước 3 Áp dụng WOP:** Vì $C$ là tập con khác rỗng của các số nguyên không âm, theo nguyên lý WOP, chắc chắn phải tồn tại một phần tử nhỏ nhất trong tập $C$. Ta gọi phần tử này là $n$.
- **Bước 4 Tìm mâu thuẫn:** Đây là bước đòi hỏi tư duy sáng tạo nhất. Bạn cần chỉ ra một điều vô lý, thường bằng 2 cách: **Chứng minh rằng thực chất $P(n)$ vẫn đúng (mâu thuẫn với việc $n$ thuộc tập "lỗi" $C$)** hoặc **Tìm ra một phần tử khác cũng thuộc $C$ nhưng lại nhỏ hơn cả $n$ (mâu thuẫn với việc $n$ là phần tử nhỏ nhất).**
- **Bước 5 Kết luận:** Vì việc giả sử $C$ khác rỗng dẫn tới mâu thuẫn, nên $C$ buộc phải là tập rỗng. Điều này đồng nghĩa với việc không có "phần tử lỗi" nào tồn tại, hay $P(n)$ đúng với mọi $n$.

# 3. Logical Formulas

Nội dung về các phép logic AND, OR, NOT...Tóm lại, là **đại số Boolean**.

## 3.5 The SAT Problem

**Bài toán SAT (viết tắt của Satisfiability)** là bài toán xác định xem một mệnh đề logic cho trước có thể True hay không. Tức là liệu có một cách gán các giá trị True hoặc False cho các biến trong công thức logic sao cho toàn bộ công thức đó đạt giá trị True. Cách tiếp cận truyền thống là làm việc với bảng chân trị. Đương nhiên đây không phải là một ý tưởng hay (nếu có quá nhiều biến)

Việc tìm ra một giải pháp hiệu quả cho bài toán SAT có tầm ảnh hưởng sâu rộng đến nhiều lĩnh vực khác nhau:

- **Tối ưu hóa và Công nghệ:** Một giải pháp hiệu quả cho SAT sẽ ngay lập tức mang lại lời giải cho hàng loạt bài toán thực tế về lập lịch (scheduling), định tuyến (routing), phân bổ nguồn lực và xác thực mạch điện.
- **Ứng dụng đa ngành:** Các lĩnh vực như lập trình, đại số, tài chính và lý thuyết chính trị đều sẽ được hưởng lợi từ việc giải quyết nhanh chóng các bài toán ràng buộc phức tạp.
- **Xác thực hệ thống:** Các chương trình giải SAT (SAT-solvers) hiện đại đã được ứng dụng thành công trong việc xác thực các mạch kỹ thuật số có hàng triệu biến.

Mặc dù có vai trò quan trọng, việc giải quyết triệt để bài toán SAT vẫn đang gặp phải những rào cản lớn về mặt lý thuyết:

**A. Vấn đề "P vs. NP"**

Đây là câu hỏi quan trọng nhất trong lý thuyết khoa học máy tính: Liệu có tồn tại một quy trình giải SAT trong thời gian đa thức ($n^2, n^{14},...$) thay vì thời gian hàm mũ ($2^n$) hay không? Hiện nay, chưa ai có thể đưa ra câu trả lời hoặc chứng minh rằng điều đó là không thể.

**B. Nguy cơ đối với an ninh toàn cầu**

Nếu bài toán SAT được giải quyết hiệu quả (nghĩa là P = NP), thế giới có thể rơi vào tình trạng hỗn loạn:

- **Sụp đổ hệ thống bảo mật:** Việc giải mã các thông điệp mật sẽ trở nên dễ dàng.
- **Mất an toàn tài chính:** Các giao dịch trực tuyến sẽ không còn được bảo mật và các thông tin liên lạc bí mật có thể bị bất kỳ ai đọc được.

**C. Hạn chế của các công cụ hiện tại**

Các chương trình SAT-solvers hiện nay tuy rất mạnh mẽ nhưng vẫn tồn tại những nhược điểm:

- **Khó dự đoán:** Không thể dự đoán được loại công thức nào sẽ phù hợp với các phương pháp của SAT-solver.
- **Bế tắc với các bài toán không thỏa mãn:** Đối với những công thức không thể đạt giá trị Đúng (unsatisfiable), các chương trình này thường không mang lại kết quả khả quan.

# 4. Mathematical Data Type

Trình bày rõ hơn về tập hợp, dãy số, tích Cartesian và hàm số. Đều là kiến thức cũ ở THPT.
**Phân biệt khái niệm Domain, Codomain, Range**. Domain là tập xác định của hàm số, Codomain là tập đích (ví dụ khi f: A -> B thì B chính là tập đích), Range là tập giá trị và là tập con của tập đích.

## 4.4 Binary Relations (Quan hệ hai ngôi)

> [!INFO]
> Binary relations define relations between two objects.

Quan hệ hai ngôi thực chất giống hệt định nghĩa về Hàm số, ngoại trừ một điều kiện quan trọng.

- Hàm số ($f: A \to B$): Một phần tử $a \in A$ chỉ có thể liên kết với tối đa một phần tử $b \in B$. Trong đồ thị của hàm số, không bao giờ có hai cặp $(a, b_1)$ và $(a, b_2)$ với $b_1 \neq b_2$.
- Quan hệ ($R$): Không có giới hạn này. Một phần tử $a$ có thể liên kết với bao nhiêu phần tử ở tập đích tùy ý, hoặc không liên kết với phần tử nào cả.

Ví dụ 1 Quan hệ "Nhỏ hơn" ($<$): Trên tập số thực, số $a$ có quan hệ với $b$ khi $a < b$.

Ví dụ 2 Quan hệ "Tập con" ($\subseteq$): Tập hợp $A$ có quan hệ với $B$ khi $A \subseteq B$.

Ví dụ 3 Hàm số là trường hợp đặc biệt của quan hệ.

# 5. Induction (Quy nạp)

**Weak vs Strong Induction:** Trong một lập luận quy nạp thông thường, bạn giả sử rằng $P(n)$ đúng và cố gắng chứng minh rằng $P(n+1)$ cũng đúng. Còn trong một lập luận quy nạp mạnh, bạn có quyền giả sử rằng tất cả các mệnh đề $P(0), P(1), \dots,$ và $P(n)$ đều đã đúng khi bạn tiến hành chứng minh $P(n+1)$. Vì vậy, bạn có thể dựa trên một tập hợp các giả thiết mạnh hơn, điều này giúp công việc chứng minh của bạn trở nên dễ dàng hơn.

## 5.3 Strong Induction vs Induction vs Well Ordering

Về mặt lý thuyết, **nguyên lý Thứ tự tốt (Well Ordering Principle), Quy nạp thông thường (Ordinary Induction) và Quy nạp mạnh (Strong Induction)** thực chất là ba cách trình bày khác nhau cho cùng một kiểu lập luận toán học. Mọi bài chứng minh sử dụng phương pháp này đều có thể được định dạng lại một cách hệ thống để chuyển sang phương pháp kia mà không làm thay đổi bản chất logic.

Điểm khác biệt nằm ở "tín hiệu" mà chúng gửi tới người đọc: Quy nạp thông thường phù hợp khi bước $n+1$ chỉ phụ thuộc vào bước $n$, trong khi Quy nạp mạnh báo hiệu nhu cầu sử dụng dữ liệu từ nhiều bước nhỏ hơn trước đó. Mặt khác, nguyên lý Thứ tự tốt thường mang lại cách tiếp cận ngắn gọn, tự nhiên hơn bằng cách tập trung vào việc tìm kiếm phản ví dụ nhỏ nhất để dẫn đến mâu thuẫn.

Việc lựa chọn phương pháp nào tùy thuộc vào sự rõ ràng của từng bài toán cụ thể, nhưng điều quan trọng nhất là người viết cần công bố rõ phương pháp đã chọn ngay từ đầu để người đọc dễ dàng theo dõi lộ trình chứng minh.

## 5.4 State Machines

Hãy tưởng tượng một hệ thống (như đèn giao thông, thang máy hoặc một đoạn code). Tại bất kỳ thời điểm nào, hệ thống đó cũng đang ở một trạng thái nhất định (ví dụ: Đèn Xanh). Khi có một sự kiện xảy ra (hết thời gian chờ), hệ thống thực hiện một bước nhảy (transition) sang trạng thái tiếp theo (Đèn Vàng). **Trong tin học, State Machine giúp ta mô hình hóa logic phức tạp thành các trạng thái và các quy tắc chuyển đổi rõ ràng.**

### 5.4.1 States and Transitions

> [!INFO] State machine
> State machine thực chất chỉ là một Quan hệ hai ngôi (Binary Relation) trên một tập hợp, nhưng được gọi bằng những cái tên chuyên biệt trong ngữ cảnh hệ thống:
> - **Tập hợp (Set)**: Được gọi là tập hợp các Trạng thái (States). Mỗi phần tử trong tập này đại diện cho một "tình huống" mà hệ thống có thể ở đó.
> - **Quan hệ (Relation)**: Được gọi là Quan hệ chuyển trạng thái (Transition Relation).
> - **Cặp $(q, r)$**: Được gọi là một Bước chuyển (Transition), ký hiệu là $q \to r$.

![[I.01.png]]

Tác giả phân chia máy trạng thái thành hai loại chính

- Máy trạng thái hữu hạn (Finite State Machines - FSM)
- Máy trạng thái vô hạn (Infinite State Machines)

Trong các giáo trình khác hoặc trong các ứng dụng chuyên sâu hơn, máy trạng thái thường đi kèm với các nhãn (labels):

- Input/Output: Giá trị đưa vào để chuyển trạng thái và kết quả trả về.
- Costs/Capacities: Chi phí để thực hiện một bước chuyển hoặc dung lượng tối đa của một trạng thái.
- Probabilities: Xác suất để một bước chuyển xảy ra (như trong Chuỗi Markov).

**Phần này khá giống với khái niệm state và transition trong Reinforcement Learning.**

### 5.4.3 The Invariant Principle

> [!INFO] Execution & Reachability
> An **execution** of the state machine is a (possibly infinite) sequence of states with the property that it begins with the start state, and if $q$ and $r$ are consecutive states in the sequence, then $q \to r$.
> A state is called **reachable** if it appears in some execution.

> [!INFO] The Invariant Principle
> If a preserved invariant of a state machine is true for the start state, then it is true for all reachable states.

### 5.4.5 Fast Exponentiation

Để khẳng định một chương trình "chạy đúng", chúng ta cần chứng minh được hai thành phần độc lập nhưng bổ sung cho nhau: Partial Correctness (Tính đúng đắn từng phần) và Termination (Tính dừng).

**Partial Correctness**

Cái tên "Partial" (từng phần) ở đây không có nghĩa là kết quả đúng một nửa, sai một nửa. Nghĩa là NẾU chương trình kết thúc và trả về kết quả, thì kết quả đó chắc chắn phải đúng với yêu cầu hệ thống. Nó không đảm bảo chương trình sẽ kết thúc. Chương trình có thể bị kẹt trong một vòng lặp vô hạn (infinite loop).

Thường sử dụng Nguyên lý Bất biến (Invariant Principle). Chúng ta chứng minh rằng tại mọi bước chạy, một tính chất logic nào đó (Invariant) luôn được giữ vững, cho đến khi máy dừng lại ở kết quả cuối cùng.

**Termination**

Đảm bảo rằng quy trình tính toán chắc chắn sẽ dừng lại và đưa ra một giá trị cuối cùng, chứ không chạy mãi mãi.

Chúng ta gán cho mỗi bước của chương trình một giá trị (thường là một số nguyên không âm). Nếu ta chứng minh được giá trị này giảm dần sau mỗi bước, thì theo Well Ordering Principle, nó không thể giảm vô hạn. Nó bắt buộc phải chạm đến phần tử nhỏ nhất và dừng lại.

### 5.4.6 Derived Variables

Dưới đây là một phương pháp tổng quát hơn để phân tích và chứng minh các thuật toán sẽ dừng lại, bằng cách mượn ý tưởng từ vật lý.

**Phép đo trạng thái (State Measure)**

Để chứng minh một thuật toán không chạy mãi mãi, chúng ta cần một công cụ để đo lường "tiến độ" của nó.

Gán cho mỗi trạng thái của máy một con số (thường là số nguyên không âm), gọi là "kích thước" (size) của trạng thái đó.Nếu mỗi bước chuyển trạng thái đều làm giảm con số này, thì theo Nguyên lý Thứ tự tốt (WOP), nó không thể giảm mãi được. Khi đạt tới giá trị nhỏ nhất, máy sẽ không thể thực hiện thêm bước chuyển nào nữa—tức là thuật toán đã dừng.

**Biến dẫn xuất (Derived Variables) và Hàm tiềm năng (Potential Functions)**

Tác giả mở rộng khái niệm này ra ngoài phạm vi các số nguyên giảm dần

**Derived Variables:** Trong tin học, bất kỳ giá trị nào được tính toán dựa trên trạng thái của máy (như tổng các phần tử trong mảng, số lượng nút còn lại trong cây...) đều được gọi là biến dẫn xuất.

**Hàm tiềm năng (Potential Functions):** Đây là một thuật ngữ mượn từ vật lý (như thế năng). Trong phân tích thuật toán (Amortized Analysis), chúng ta dùng hàm này để theo dõi năng lượng hoặc tài nguyên mà thuật toán đang tiêu thụ.

> [!TIP] Hàm tiềm năng (Potential Function)
> Phương pháp này cực kỳ hữu ích vì đôi khi chúng ta không thấy thuật toán "giảm" một cách trực tiếp (ví dụ: một biến chạy có thể tăng), nhưng một tổ hợp các biến (hàm tiềm năng) lại luôn giảm.

> [!INFO] Mối liên hệ với Phương pháp đơn biến
> Phần này nói về việc sử dụng WOP và hàm tiềm năng để chứng minh một chương trình sẽ đạt trạng thái dừng. Trong toán học tổ hợp cũng có một dạng bài toán yêu cầu chứng minh tồn tại trạng thái dừng, gọi là **phương pháp đơn biến**.
>
> - **Ý tưởng chính**: Tìm một hàm số sao cho giá trị của nó luôn giảm sau mỗi bước, cho đến khi đạt đến một giá trị giới hạn (ví dụ bằng 0).

> [!IMPORTANT] Ứng dụng Invariant Principle (Nguyên lý bất biến)
> Việc ứng dụng Invariant Principle dùng để tìm ra quy luật không đổi trong mọi trạng thái.
>
> - **Mục tiêu**: Chứng minh không tồn tại một trạng thái $T$ nào đó.
> - **Cách làm**: Chỉ cần chứng minh trạng thái $T$ không thỏa mãn một tính chất bất biến vốn luôn được duy trì trong suốt quá trình thực thi (execution) hoặc giữa các bước chuyển trạng thái (state transitions).

# 6. Recursive Data Types (Kiểu dữ liệu đệ quy)

> [!INFO] Định nghĩa Đệ quy (Recursive Data Types)
> Một kiểu dữ liệu được gọi là đệ quy khi nó được xác định dựa trên chính nó. Phần tử ở sau được định nghĩa dựa trên phần tử ở trước.
>
> **Lưu ý:** Khái niệm này thực chất chúng ta đã làm quen rất kỹ ở phần dãy số rồi.

Một số ví dụ về kiểu dữ liệu này:

- Strings (Chuỗi ký tự): Một chuỗi là một ký tự đứng trước một chuỗi khác (ví dụ: "abc" là 'a' + "bc").
- Balanced strings of brackets (Chuỗi ngoặc cân bằng): Các quy tắc để đảm bảo ngoặc mở luôn có ngoặc đóng tương ứng (như (())).
- Nonnegative integers (Số nguyên không âm): Số $n+1$ được tạo ra từ số $n$.
- Arithmetic expressions (Biểu thức số học): Một biểu thức có thể gồm các biểu thức con kết hợp với nhau bằng các toán tử $+$, $-$, $\times$, $\dots$

## 6.1 Recursive Definitions and Structural Induction

Ta bắt đầu với kiểu dữ liệu **String**.

Thay vì coi chuỗi là một mảng (array) nằm ngang như cách ta thường viết ($1011$), toán học định nghĩa nó theo cấu trúc "vỏ bọc" (nested):

- **Base case (Trường hợp cơ sở):** Chuỗi rỗng (ký hiệu là $\lambda$) là một chuỗi.
- **Constructor (Bộ tạo):** Một chuỗi mới được tạo ra bằng cách lấy một ký tự $a$ gắn vào đầu một chuỗi $s$ đã có sẵn: $\langle a, s \rangle$.

**Tại sao lại dùng cặp $\langle a, s \rangle$?**

Cách này phản ánh đúng cấu trúc Linked List (Danh sách liên kết). Trong Python, nó tương đương với việc phần tử đầu tiên trỏ tới phần còn lại của danh sách. Chuỗi $1011$ thực chất là: 1 kết nối với (0 kết nối với (1 kết nối với (1 kết nối với Rỗng))).

Cấu trúc dữ liệu được định nghĩa thế nào thì các hàm xử lý nó cũng được định nghĩa như thế. Đều có base case và constructor.

- **Độ dài của chuỗi rỗng:** $|\lambda| = 0$.
- **Độ dài của một chuỗi có ký tự đầu $a$:** $|\langle a, s \rangle| = 1 + |s|$.

### 6.1.1 Structural Induction

Như đã giới thiệu ở trên, đây là định nghĩa của Quy nạp cấu trúc:

> [!INFO] Structural Induction Proof
> A **structural induction** proof has two parts corresponding to the recursive definition:
>
> - **Base case**: Prove that each base case element has the property.
> - **Constructor case**: Prove that each constructor case element has the property, khi constructor được áp dụng cho các phần tử đã có tính chất đó.

Nguyên lý Quy nạp cấu trúc (Structural Induction) là một phiên bản **mở rộng và tổng quát hóa của quy nạp toán học thông thường**, được thiết kế riêng để làm việc với các kiểu dữ liệu đệ quy.

Thay vì chạy dọc theo các số nguyên $0, 1, 2, \dots, n$, quy nạp cấu trúc chạy dọc theo quy trình xây dựng dữ liệu. Nếu bạn chứng minh được một tính chất $P$ được bảo toàn qua mọi "bộ lắp ghép" (constructors) của dữ liệu, thì tính chất đó phải đúng cho toàn bộ tập dữ liệu đó.

![[I.02.png]]

### 6.1.2 One More Thing

Tương tự như cách định nghĩa độ dài, việc đếm một ký tự $c$ trong chuỗi $s$ cũng tuân theo cấu trúc của dữ liệu:

![[I.03.png]]

![[I.04.png]]

![[I.05.png]]

## 6.2 Strings of Matched Brackets

Sách ghi khá đẹp nên mình chụp vào luôn, khỏi ghi lại

![[I.06.png]]

![[I.07.png]]

> [!WARNING] Tính nhập nhằng trong kiểu dữ liệu đệ quy
> Một kiểu dữ liệu đệ quy bị coi là nhập nhằng khi cùng một phần tử dữ liệu có thể được tạo ra bằng nhiều cách khác nhau (nhiều lộ trình đệ quy khác nhau) dựa trên các quy tắc đã cho.
>
> **Hệ quả:** Nếu một phần tử có thể được tạo ra theo hai cách, và bạn định nghĩa một hàm $f$ dựa trên cấu trúc đó, thì hàm $f$ có thể trả về hai giá trị khác nhau cho cùng một đầu vào. Khi đó, $f$ vi phạm định nghĩa của một hàm số.

Dưới đây là một ví dụ minh họa.

![[I.08.png]]

![[I.09.png]]

Tập hợp **AmbRecMatch** trong ảnh là một định nghĩa bị nhập nhằng (ambiguous), còn tập hợp **RecMatch** ban đầu thì không. Việc một tập hợp có thể được định nghĩa bằng hai bộ quy tắc khác nhau không làm cho nó bị nhập nhằng, mà sự nhập nhằng nằm ở cấu trúc bên trong của chính bộ quy tắc đó.

## 6.3 Recursive Functions on Nonnegative Integers

Thay vì coi số nguyên là những ký hiệu có sẵn, chúng ta xây dựng chúng từ con số không:

- **Base case (Trường hợp cơ sở):** $0 \in \mathbb{N}$.
- **Constructor (Bộ tạo):** Nếu $n$ đã tồn tại, thì "số liền sau" của nó ($n+1$) cũng tồn tại.

Với cách định nghĩa này, số $3$ thực chất là: $(((0+1)+1)+1)$. Nó hoàn toàn giống với cấu trúc của một chuỗi (String) hay một danh sách (List) mà bạn đã học ở phần trước.

Tác giả muốn nhấn mạnh một tư duy hệ thống:

- **Quy nạp thường**: Bạn chứng minh cho $n=0$, sau đó chứng minh từ $n \to n+1$
- **Quy nạp cấu trúc**: Bạn chứng minh cho Base case ($0$), sau đó chứng minh tính chất được bảo toàn qua Constructor ($n \to n+1$).

Hai phương pháp này là một. Quy nạp cấu trúc là phiên bản tổng quát hơn vì nó có thể áp dụng cho cả những cấu trúc "phân nhánh" như Cây (Trees), trong khi quy nạp thường chỉ áp dụng cho cấu trúc "đường thẳng" như số nguyên.

### 6.3.2 Ill-formed Function Definitions

> [!WARNING] Tính xác định tốt (Well-definedness)
> Không phải mọi định nghĩa trông có vẻ "đệ quy" đều là một hàm số hợp lệ. Để một hàm đệ quy được coi là **xác định tốt** (well-defined), nó phải tuân thủ nghiêm ngặt cấu trúc của kiểu dữ liệu nền tảng.

**Tính đến đây ta thấy có 2 lỗi:** định nghĩa cấu trúc dữ liệu bị nhập nhằng, và định nghĩa hàm xử lí không khớp với cấu trúc của kiểu dữ liệu.

**Các sai lầm phổ biến**

- **Thiếu trường hợp cơ sở (Missing Base Case):** Bạn định nghĩa $f(n) = f(n-1) + 1$ nhưng không nói $f(0)$ bằng bao nhiêu. Lúc này, máy tính sẽ rơi vào vòng lặp vô hạn vì không biết điểm dừng.
- **Định nghĩa "nhìn về phía trước" (Circular or Forward Reference):** Ví dụ định nghĩa $f(n)$ dựa trên $f(n+1)$. Điều này vi phạm tính đệ quy vì bạn đang cố gắng giải thích cái đơn giản bằng cái phức tạp hơn chưa được tạo ra.
- **Nhập nhằng (Ambiguity):** Đối với các kiểu dữ liệu phức tạp hơn số nguyên (như chuỗi ngoặc AmbRecMatch bạn vừa xem), nếu có hai cách để tạo ra $n+1$, nhưng hai cách đó lại dẫn đến hai giá trị $f(n+1)$ khác nhau, thì hàm đó không còn là hàm số duy nhất nữa.

**Giả thuyết Collatz**

Giả thuyết Collatz (hay hàm $f_4$) là một ví dụ điển hình trong toán học về một định nghĩa hàm trông có vẻ đệ quy nhưng lại cực kỳ khó để xác định là "xác định tốt" (well-defined).

![[I.10.png]]

Mặc dù thực nghiệm đã chứng minh mọi số nguyên lên đến hơn $10^{18}$ đều cuối cùng hội tụ về giá trị 1, nhưng về mặt lý thuyết, chúng ta vẫn chưa thể chứng minh điều này đúng cho mọi số tự nhiên $\mathbb{N}$.

Thách thức chính nằm ở chỗ quy tắc $3n+1$ xác định giá trị của $f_4(n)$ dựa trên một đối số lớn hơn chính nó, điều này vi phạm nguyên tắc cốt lõi của quy nạp cấu trúc trên tập số nguyên: luôn phải xây dựng dựa trên các giá trị nhỏ hơn. Do không thể thiết lập một lộ trình "đi xuống" chắc chắn về trường hợp cơ sở (base case), Giả thuyết Collatz trở thành một minh chứng cho thấy: một quy trình bước-nối-bước đơn giản vẫn có thể chứa đựng những sự phức tạp không thể giải quyết bằng các công cụ logic thông thường. Trong khoa học máy tính, đây là lời nhắc nhở quan trọng về việc kiểm chứng tính hội tụ và tính dừng (termination) của các thuật toán tối ưu hóa.

**Hàm Ackermann**

![[I.11.png]]

Nó nổi tiếng vì tốc độ tăng trưởng nhanh khủng khiếp, nhanh hơn bất kỳ hàm đa thức hay hàm mũ thông thường nào.

Để tính $A(m, n)$, bạn phải tính $A$ của một giá trị bên trong là $A(m, n-1)$. Giá trị bên trong này có thể trở nên cực kỳ lớn, lớn hơn nhiều so với $m$ và $n$ ban đầu.

**Thuật toán Union-Find**

Hàm Ackermann không chỉ là một bài toán lý thuyết suông. Nó xuất hiện khi phân tích thuật toán Union-Find (dùng để quản lý các tập hợp không giao nhau).

Số bước chạy của Union-Find tỉ lệ với Hàm ngược Ackermann ($\alpha(n)$). Vì hàm Ackermann tăng cực nhanh, nên hàm ngược của nó tăng cực kỳ chậm. Thậm chí với đầu vào là số lượng nguyên tử trong vũ trụ, giá trị của $\alpha(n)$ vẫn nhỏ hơn 5. Điều này có nghĩa là trên thực tế, thuật toán Union-Find chạy nhanh gần như một hàm tuyến tính (linear).

## 6.4 Arithmetic Expressions

Phần này giới thiệu về **Biểu thức số học (Aexp)** như một kiểu dữ liệu đệ quy. Đây là nền tảng để máy tính có thể "hiểu" và xử lý các công thức toán học mà chúng ta nhập vào.

![[I.12.png]]

![[I.13.png]]

### 6.4.1 Evaluation and Substitution with Aexp’s

Tức là tính toán và thay thế (thay giá trị) vào biểu thức. Có 2 cách.

**Mô hình Thay thế (Substitution Model)**

Trong mô hình này, chúng ta thực hiện việc thay thế các ký hiệu trước, sau đó mới tính toán giá trị số.

Ví dụ: Để tính giá trị của $x(x-1)$ khi thay $x = 3x$ tại $x=2$

- **Bước 1 (Subst):** Thay $3x$ vào $x(x-1)$ để được biểu thức mới là $3x(3x - 1)$.
- **Bước 2 (Eval):** Thay $x=2$ vào biểu thức mới: $3(2) \cdot (3(2) - 1) = 6 \cdot 5 = 30$.

**Nhược điểm:** Phép tính $3 \times 2$ bị lặp lại hai lần vì cụm $3x$ xuất hiện hai lần sau khi thay thế. Điều này gây lãng phí tài nguyên tính toán.

**Mô hình Môi trường (Environment Model)**

Mô hình này tối ưu hơn bằng cách tính toán giá trị của biểu thức thay thế ngay lập tức.

Ví dụ: Tính giá trị của biểu thức thay thế ($3x$) trước, sau đó dùng kết quả đó làm "môi trường" (giá trị mới của $x$) để tính biểu thức chính.

**Ưu điểm:** Chỉ cần thực hiện phép nhân $3 \times 2$ đúng một lần. Đây là cách các ngôn ngữ lập trình hiện đại thường hoạt động để tăng hiệu năng.

## 6.5 Induction in Computer Science

Tổng kết lại chương 6.

**Quy nạp thông thường & Quy nạp mạnh:** Áp dụng cho bất kỳ thứ gì có thể gán cho một "kích thước" là số nguyên không âm (như số bước chạy của một thuật toán).

**Quy nạp cấu trúc:** Đi xa hơn việc chỉ "đếm số", nó cung cấp một cách tiếp cận tự nhiên và trực tiếp để chứng minh các tính chất của dữ liệu đệ quy (như chuỗi, cây, biểu thức) mà không cần phải quy đổi chúng về con số.

Mặc dù bạn có thể dùng Quy nạp thường trên "độ dài" của chuỗi hoặc "số phép toán" trong một biểu thức để chứng minh một tính chất, nhưng tác giả chỉ ra rằng: Quy nạp cấu trúc tạo ra các bài chứng minh ít cồng kềnh và mạch lạc hơn vì nó đi sát với cách dữ liệu được tạo ra. Quy nạp cấu trúc thực sự mạnh hơn quy nạp thường khi làm việc với các kiểu dữ liệu vô hạn (ví dụ: những cái cây vô tận). Tuy nhiên, trong thực tế lập trình, điểm quan trọng nhất vẫn là sự đơn giản và tự nhiên.

# 7. Infinite Sets

Tại sao dân tin học lại phải học về vô hạn, trong khi bộ nhớ máy tính và cả vũ trụ này đều hữu hạn?

- Nếu chúng ta chỉ chấp nhận những tập hợp hữu hạn, toán học và khoa học sẽ trở nên cực kỳ rắc rối. Sẽ rất vô lý nếu vật lý từ bỏ số thực chỉ vì chúng ta không thể đo đạc vô hạn trong một vũ trụ hữu hạn.
- Làm việc với các tập hợp vô hạn buộc chúng ta phải cực kỳ khắt khe trong lập luận
- Việc nghiên cứu các tập hợp vô hạn đã dẫn đến khám phá về giới hạn logic tuyệt đối của máy tính.

## 7.1 Infinite Cardinality

Tác giả nêu rõ họ sẽ không định nghĩa giá trị cụ thể cho kích thước của một tập vô hạn (vốn đòi hỏi các khái niệm phức tạp như số thứ tự - ordinals và tính thứ tự tốt). Thay vì cố gắng trả lời câu hỏi "Tập hợp này lớn bao nhiêu?", chúng ta chỉ tập trung vào việc so sánh: "Tập hợp này có cùng kích thước hoặc lớn bằng tập hợp kia không?".

Tức là sẽ vận dụng **Mapping Theorem**, 2 tập được gọi là lớn bằng nhau khi có song ánh giữa chúng.

### 7.1.1 Infinity is different

![[I.14.png]]

### 7.1.2 Countable Sets

Một tập hợp được gọi là đếm được nếu nó finite và nếu nó countably infinite. Countably infinite nghĩa là vô hạn đếm được.

> [!INFO] Tập hợp vô hạn đếm được (Countably Infinite)
> Giả sử có một tập $A$. $A$ được gọi là **countably infinite** khi có một song ánh từ $\mathbb{N}$ đến $A$.

> [!INFO] Tập hợp đếm được (Countable)
> Tổng quát, giả sử có tập $A$. $A$ được gọi là **countable** (kể cả khi $A$ hữu hạn hay vô hạn) khi có một toàn ánh từ $\mathbb{N}$ đến $A$.

Có người sẽ thắc mắc tại sao toàn ánh từ $N$ là đủ để kết luận tập đó đếm được. Đây là giải thích.

Một toàn ánh $g: \mathbb{N} \to A$ có nghĩa là mọi phần tử trong tập $A$ đều được "phủ kín" bởi ít nhất một số tự nhiên.

- Nếu bạn coi $\mathbb{N}$ là một danh sách các vị trí $0, 1, 2, \dots$, thì toàn ánh đảm bảo rằng bạn có thể viết ra một danh sách $g(0), g(1), g(2), \dots$ chứa mọi phần tử của $A$.
- Việc cho phép lặp lại (nhiều số tự nhiên cùng trỏ đến một phần tử trong $A$) không làm mất đi tính chất "liệt kê được" của tập hợp.

Về mặt toán học, nếu bạn có một toàn ánh từ $\mathbb{N}$ đến $A$, bạn luôn có thể tạo ra một danh sách mới không lặp lại bằng cách: Duyệt qua danh sách $g(0), g(1), g(2), \dots$. Nếu gặp một phần tử đã xuất hiện trước đó, hãy bỏ qua nó và đi tiếp.

**=> Toàn ánh cho phép chúng ta dùng một công thức duy nhất cho cả tập hữu hạn và vô hạn mà không cần tách riêng các trường hợp.**

Các tập hợp đếm được có tính đóng dưới phép hợp (union) và phép nhân (product). Nghĩa là **hợp của nhiều tập đếm được vẫn là đếm được.**

Tác giả khẳng định rằng các tập hợp vô hạn đếm được chính là những tập hợp "bé nhất" trong thế giới vô hạn. Vì Nếu $A$ là một tập hợp vô hạn bất kỳ và $B$ là một tập hợp đếm được, thì luôn tồn tại một toàn ánh từ $A$ đến $B$.

Việc thêm một số lượng hữu hạn phần tử vào một tập vô hạn không làm thay đổi kích thước của nó. Thậm chí, bạn có thể thêm một lượng vô hạn đếm được các phần tử mới vào một tập vô hạn, và kết quả vẫn là một tập hợp có cùng kích thước ban đầu. Nhưng không có nghĩa là bạn luôn có thể thêm một lượng vô hạn phần tử mà kích thước vẫn giữ nguyên (điều này chỉ đúng với một số trường hợp cụ thể).

### 7.1.3 Power sets are strictly bigger

Mọi người thường nghĩ khi một tập hợp infinite thì xem như chúng tương tự nhau, bằng nhau (vì đều vô hạn mà). Nhưng có những tập vô hạn lớn hơn rất nhiều. Tập các tập con là một ví dụ.

![[I.15.png]]

**Từ đó dẫn tới hệ quả:** pow($\mathbb{N}$) là vô hạn không đếm được (vì $\mathbb{N}$ "nhỏ hơn", thì làm sao có toàn ánh từ $\mathbb{N}$ đến tập pow($\mathbb{N}$) được)

### 7.1.4 Diagonal Argument (Optional)

Trong toán học lý thuyết, việc chứng minh một tập hợp là "không đếm được" đòi hỏi những công cụ logic mạnh mẽ hơn việc liệt kê thông thường. **Phương pháp đường chéo của Georg Cantor** là một kỹ thuật phản chứng kinh điển, dùng để chỉ ra rằng có những tập hợp vô hạn "lớn hơn" so với tập số tự nhiên $\mathbb{N}$.

Phương pháp này thường được minh họa thông qua tập hợp các chuỗi bit vô hạn $\{0, 1\}^\omega$. Quy trình chứng minh gồm các bước sau:

- **Giả thiết phản chứng:** Giả sử tập hợp $\{0, 1\}^\omega$ là đếm được, nghĩa là ta có thể lập một danh sách đầy đủ tất cả các chuỗi bit theo một thứ tự $A_1, A_2, A_3, \dots$.
- **Xây dựng bảng vô tận:** Sắp xếp các chuỗi này thành một ma trận vuông vô hạn, trong đó hàng $n$ là chuỗi $A_n$ và cột $k$ là bit thứ $k$ của chuỗi đó.
- **Thiết lập đường chéo $D$:** Tập hợp các bit nằm trên đường chéo chính của bảng, ký hiệu là $D = d_1 d_2 d_3 \dots$ (trong đó $d_n$ là bit thứ $n$ của chuỗi $A_n$).
- **Tạo chuỗi nghịch đảo $C$:** Xây dựng chuỗi $C$ bằng cách đảo ngược mọi bit trên đường chéo $D$ (nếu $d_n = 0$ thì bit tương ứng của $C$ là $1$ và ngược lại).

![[I.16.png]]

**Kết luận logic:** Chuỗi $C$ không thể xuất hiện ở bất kỳ vị trí nào trong danh sách ban đầu. Nó khác với chuỗi $A_1$ ở bit thứ nhất, khác với $A_2$ ở bit thứ hai, và tổng quát là khác với $A_n$ ở bit thứ $n$. Điều này dẫn đến mâu thuẫn: danh sách không hề đầy đủ như ta đã giả định, do đó tập $\{0, 1\}^\omega$ là không đếm được.

## 7.2 The Halting Problem (Optional)

Chúng ta đã đi qua tính partial correctness, tính termination, giờ ta sẽ chứng minh **tính không thể tính toán (Uncomputability).**

Một thực tế cơ bản trong lập trình: **Các chương trình thường xuyên xử lý các chương trình khác.** Ví dụ, Trình biên dịch (Compilers): Lấy mã nguồn (Java, Python...) làm đầu vào và tạo ra mã máy. Trình thông dịch (Interpreters): Chạy trực tiếp mã nguồn trên một máy ảo. Trình kiểm tra kiểu (Type-checkers): Phân tích mã nguồn để tìm lỗi trước khi chạy.

> [!INFO] Giới hạn của tính toán (Limits of Computation)
> The fundamental thing that just can’t be done by computation is **a perfect job** of type-checking, optimizing, or any kind of analysis of the overall run-time behavior of programs.

Tức là, các task (type-checking, optimizing...) không thể được hoàn thành một cách perfect trên mọi chương trình. Ta minh họa việc này thông qua **The Halting Problem**.

- **Định nghĩa:** Cho một chương trình bất kỳ, hãy xác định xem nó sẽ chạy mãi mãi hay cuối cùng sẽ dừng lại (halt).
- **Vấn đề:** Việc nhận biết một chương trình sẽ dừng là rất dễ (chỉ cần chạy nó và đợi), nhưng việc biết chắc chắn một chương trình không bao giờ dừng là bất khả thi. Bạn có thể đợi 100 năm, nhưng không thể biết nó sẽ chạy mãi mãi hay sẽ dừng ở năm thứ 101.

Tác giả sẽ dùng lập luận đường chéo (tương tự cách Cantor chứng minh số thực nhiều hơn số tự nhiên) để chỉ ra mâu thuẫn logic: **Nếu bạn có một chương trình "siêu cấp" có thể nhận biết mọi chương trình không dừng, bạn có thể dùng chính nó để tạo ra một chương trình mà "siêu chương trình" đó không thể phân tích được.**

**Bước 1: Giả định điều "không tưởng"**

Giả sử tồn tại một chương trình phân tích (gọi là $H$) có khả năng giải quyết Bài toán dừng.

- **Input:** Một chương trình $P_s$ và một dữ liệu $t$.
- **Output:** $H$ sẽ dừng và trả về "Dừng" nếu $P_s$ chạy trên $t$ và cuối cùng sẽ dừng. $H$ sẽ dừng và trả về "Không dừng" nếu $P_s$ chạy trên $t$ và sẽ lặp vô tận.

**Bước 2: Thu hẹp vào "Trường hợp đặc biệt"**

Để tạo ra mâu thuẫn, chúng ta chỉ quan tâm đến việc chuyện gì xảy ra khi một chương trình tự phân tích chính mã nguồn của nó. Tức là chúng ta xét $H(s, s)$—liệu chương trình $P_s$ có dừng khi đầu vào là chuỗi $s$ không?

**Bước 3: Chế tạo "Chương trình quái dị" (The Monster)**

Đây là lúc chúng ta dùng lập luận đường chéo. Hãy tưởng tượng ta xây dựng một chương trình mới, gọi là $M$ (viết tắt của Mischievous - kẻ tinh quái), dựa trên chương trình $H$ ở trên:

- Nếu $H(s, s)$ bảo rằng $P_s$ sẽ DỪNG: Thì chương trình $M$ sẽ cố tình LẶP VÔ TẬN.
- Nếu $H(s, s)$ bảo rằng $P_s$ KHÔNG DỪNG: Thì chương trình $M$ sẽ DỪNG NGAY LẬP TỨC.

$M$ luôn làm ngược lại hoàn toàn so với kết quả mà chương trình phân tích $H$ dự đoán về việc một chương trình tự chạy trên chính nó.

**Bước 4: Đòn chí mạng - Nghịch lý tự thân**

Chuyện gì sẽ xảy ra nếu chúng ta đưa mã nguồn của chính chương trình $M$ vào cho chương trình $M$ xử lý? (Tức là xét $M(m)$ với $m$ là mã nguồn của $M$).

- Nếu $H$ dự đoán $M$ sẽ dừng: Theo định nghĩa của $M$ ở Bước 3, nó sẽ lặp vô tận. (Mâu thuẫn: Dự đoán dừng nhưng thực tế lặp).
- Nếu $H$ dự đoán $M$ sẽ lặp vô tận: Theo định nghĩa của $M$ ở Bước 3, nó sẽ dừng lại. (Mâu thuẫn: Dự đoán lặp nhưng thực tế dừng).

Tác giả khẳng định rằng việc giải quyết trường hợp đặc biệt (liệu $P_s$ có dừng khi chạy trên chính mã nguồn $s$ không) đã chứng minh một sự thật lớn hơn: **Mọi ngôn ngữ lập trình đều không thể giải quyết được Bài toán dừng tổng quát.**
=> Nếu bạn không thể biết một chương trình có dừng hay không, bạn cũng không thể xây dựng một quy trình hoàn hảo để nhận biết bất kỳ thuộc tính thực thi (run-time property) nào.

Tuy nhiên, đây là thực tế:

- **Chương trình tùy ý (Arbitrary programs):** Lý thuyết chứng minh ta không thể phân tích được mọi chương trình bất kỳ (bao gồm cả những chương trình rác hoặc được cố tình thiết kế để đánh lừa).
- **Chương trình "Thú vị" (Interesting programs):** Trong thực tế, các chương trình chúng ta viết ra thường có cấu trúc rõ ràng và mục đích cụ thể. Chúng thường được thiết kế để có thể phân tích được nhằm xác nhận tính đúng đắn.

Dù về mặt logic là không thể giải quyết bài toán cho mọi trường hợp, nhưng chúng ta vẫn có thể làm cực tốt trên những chương trình thực tế mà con người sử dụng.

## 7.3 The Logic of Sets

### 7.3.1 Russell's Paradox

Vào cuối thế kỷ 19, nhà logic học Gottlob Frege cho rằng bất kỳ tính chất nào được định nghĩa rõ ràng cũng đều tạo thành một tập hợp. Nhưng Bertrand Russell đã chứng minh điều này sai bằng một lập luận chỉ vỏn vẹn 3 dòng.

Hãy tưởng tượng một tập hợp $W$, bao gồm tất cả các tập hợp **không tự chứa chính nó** làm phần tử. Câu hỏi đặt ra là: **$W$ có chứa chính nó không? ($W \in W$? )**

![[I.17.png]]

Cách duy nhất để cứu toán học là thừa nhận rằng: **$W$ thực chất không phải là một tập hợp**. Để phủ nhận $W$ là một tập hợp, các nhà toán học buộc phải từ bỏ một định lý cực kỳ tự nhiên: **"Mọi bộ sưu tập các đối tượng được định nghĩa rõ ràng đều là một tập hợp"**. Nếu không phải mọi bộ sưu tập đều là tập hợp, thì cái gì mới thực sự là tập hợp?

Cuối cùng, một hệ tiên đề đơn giản hơn và chặt chẽ hơn đã ra đời, gọi là **hệ tiên đề Zermelo-Fraenkel (ZF)**. Đây là hệ thống mà hầu hết các nhà toán học ngày nay đang sử dụng để định nghĩa tập hợp một cách an toàn, tránh được những vòng lặp chết người như nghịch lý Russell.

### 7.3.3 Avoiding Russell’s Paradox

**Tiên đề cơ sở (Foundation Axiom)**

Đây là một bổ sung kỹ thuật quan trọng trong hệ tiên đề ZFC. Ý tưởng của nó rất trực quan: các tập hợp không tự nhiên xuất hiện mà phải được xây dựng từ dưới lên.

- **Nguyên tắc xây dựng:** Một tập hợp phải được tạo thành từ những tập hợp "đơn giản hơn" nó.
- **Hệ quả trực tiếp:** Điều này dẫn đến quy tắc rằng không một tập hợp nào được phép là phần tử của chính nó ($S \notin S$). Nếu $S \in S$, nghĩa là $S$ không được xây dựng từ thứ gì đơn giản hơn, điều này vi phạm tính thứ tự của Tiên đề Cơ sở.

Do đó giải quyết được nghịch lý Russell.

## 7.4 Does All This Really Work?

Toán học hiện đại đang đứng trên một nền tảng cực kỳ mạnh mẽ nhưng không phải là tuyệt đối. ZFC giúp chúng ta tiến xa trong việc giải quyết các bài toán, nhưng ở mức độ bản chất, nó vẫn là một hệ thống mở với những câu hỏi chưa có lời đáp và những giới hạn logic không thể vượt qua **(Định lý Bất toàn của Gödel, Giả thuyết Continuum, Những nghịch lý từ Tiên đề Chọn (Axiom of Choice)...)**
