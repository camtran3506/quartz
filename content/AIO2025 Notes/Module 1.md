# Week 1

## Day 1: Skills for AIO2025

Buổi này giới thiệu thoi. Nếu là dân IT thì đọc slide xong đi ra là được.

1. Tìm tài liệu/paper học: **Google Scholar**, IEEEXplore, PubMed, Springer, ScienceDirect, **arxiv**. Nếu tìm đọc paper thì hay dùng arxiv nhất, chủ yếu vì nó free. Cuối cùng là **paperswithcode**, mà hình như nó đóng mẹ rồi huhu.
2. Cách đọc paper được thầy rcm: Title -> Abstract -> Introduction -> Experimental -> Method -> Related Works. Có thể dùng AI để đọc và tóm tắt, like **NotebookLM**.
3. Chỗ để code: Jupyter Notebook, Google Colab, Kaggle...Nên dùng **Anaconda** để tải Jupyter Notebook và quản lí môi trường.
4. Viết paper/report: Latex, làm trên **Overleaf**.

## Day 2: Basic Python

Thật sự là basic. Đối với ai đã học nhập môn lập trình, đọc slide cho biết và đi ra. Đối với ai chưa học code, thì xem cả video. Đối với Vibe Coder, bỏ qua buổi này.

1. Overflow and Underflow: Khi ngôn ngữ lập trình ko mô tả đc con số quá nhỏ hoặc quá lớn (do đặc thù type dữ liệu chỉ có bao nhiêu byte đó...)
2. Vì hàm log scale số xuống nhỏ hơn và nó đơn điệu nên hay được ứng dụng trong ML. Chủ yếu là lí do...toán học?
3. Một ví dụ khác là dùng hàm e mũ x để tính phần trăm a, b, c với a, b, c có thể là số thực. Ứng dụng trong hàm Softmax.
4. Ôn tập lại về ý tưởng tích phân: khi tính thể tích một hình lớn thì chia thành nhiều hình nhỏ ra đến vô cùng rồi tổng lại.
5. Có thể dùng if-else cho rule based chatbot.
6. Hàm Softmax và Stable Softmax được dùng để chuyển một dãy số thành phân phối xác suất, làm đầu ra của neural network. Chi tiết có thể đọc bài đọc thêm được đính kèm vào buổi học.

## Day 3: Loop in Python

Still basic. Học For với While và hết .-.

## Day 4: TA-Exercise

Buổi này để ôn lại 3 buổi kia và làm bài tập thêm. Toi nghĩ một tuần chỉ học buổi này thoi là đủ, mấy TA bắn rap vừa tốc độ học của toi, mà còn có bài tập nữa.

## Self Study

1. Các lỗi thường gặp trong lập trình (basic thoi...)
2. Dùng assert để kiểm tra điều kiện, debug. Nó sẽ in thông tin ra màn hình (tùy theo mình thiết lập) và dừng chương trình lại tại đó nếu bị lỗi, raise assertion error. Chắc là dùng để debug những lỗi logic của chương trình.
3. Có cách dùng vòng lặp for trong comprehension để tạo ra List, Dict nhanh chóng hơn. Ờm, tôi biết có tồn tại enumerate để giúp duyệt qua các phần tử tiện hơn nhưng tôi khong nhớ cách dùng.
4. Streamlit là một **package sử dụng cho ngôn ngữ Python**, tạo ra các web đơn giản để demo mô hình AI. Package sử dụng cho Python có nghĩa là user khi dùng các hàm trong thư viện đó thì dùng Python để code, nhưng package có thể được viết bằng các ngôn ngữ cấp thấp hơn như C/C++.
5. File Self_Study_2 có hướng dẫn một số lệnh cơ bản khi dùng Streamlit để tạo web. Ngoài ra còn nói sơ qua về cấu trúc 1 dự án, chia các file thực thi thành nhiều module, và các file này liên kết, gọi hàm của nhau bằng lệnh from 'tên file' import 'tên hàm' chẳng hạn. Chia ra chương trình chạy chính và các chương trình phụ.
6. Khi dùng streamlit, hóa ra có thể mở streamlit cloud để lấy public URL, cho người khác vào xem.

# Week 2

## Day 1: List

All about list và các hàm built-in, slicing của nó. Thuần code.

1. Built-in function khác method chỗ nào? Method chỉ gọi được từ chính object đã có định nghĩa method đó, còn hàm có sẵn thì đã có trong ngôn ngữ python rồi. Function nhận object vào; method thuộc về object và được object gọi.
2. Có lệnh del, dùng để xóa ;v lệnh xóa tối thượng xóa tên biến, xóa object vv.

## Day 2: Data Structure (1D, 2D List)

Học List Comprehension, 2D List, Linear Search (lướt qua nửa video để học, còn lại nửa đầu thì Day 1 dạy all rồi).

## Day 3: Data Structure (Tuple, Set, Dictionary)

1. Nhớ khái niệm Mutable và Immutable, tức là loại data structure nào được phép thay đổi value các phần tử được chứa bên trong nó.
2. Có thể dùng hàm dir(tuple) chẳng hạn, để biết có những hàm built in nào có sẵn cho nó.
3. Dùng Immutable cần ít memory hơn vì nó không phải lưu thêm data cho các thao tác thêm sửa xóa.
4. Set: không có 2 phần tử nào có cùng giá trị, và unordered, unindexed. Do đó nó không được contain các cấu trúc mutable.
5. Shallow copy và deep copy: shallow copy chỉ là tạo ra một ctdl (hoặc tên biến) mới trỏ vào giá trị cũ, deep là tạo giá trị mới hoàn toàn luôn.
6. Một số ứng dụng vào Text Classification, Histogram. Chỉ là ứng dụng một bước nhỏ trong các task này thôi, nếu đã học qua các bài toán này thì sẽ thấy dễ hiểu hơn.
7. Có 2 ứng dụng không được nhắc đến trong vid là tính IOU và thuật toán Non Maximum Suppression trong Object Detection.

## Day 4: TA-Exercise (Word Suggestion)

## Self Study
