# Tuần 03: GIẢI THUẬT TÌM KIẾM ĐỐI KHÁNG

## 1. Tóm tắt Các Thành phần Đã Triển khai

| STT | Yêu cầu (Theo đề bài) | Thuật toán | Cấu trúc Liên Quan | Ghi chú |
| :--- | :--- | :--- | :--- | :--- |
| **Bài 3 & 4** | Tic-Tac-Toe với ma trận N x N | Minimax & Alpha-Beta | Class `GomokuAI_AlphaBeta` | Triển khai cốt lõi là Alpha-Beta và Heuristic cho N x N. |
| **Bài 5** | Ứng dụng kỹ thuật cắt tỉa Alpha-beta vào game cờ tướng, cờ vua và cờ vây. | Cấu trúc Alpha-Beta | Class `ChessAI` (Cấu trúc) | Phân tích tập trung vào Heuristic và Move Generator. |
| **Bài 6** | Xây dựng giao diện đồ họa cho trò chơi tictactoe. | Tkinter GUI | Class `TicTacToeGUI` | Giải pháp sử dụng Tkinter để tương thích với môi trường Colab. |

---

## 2. Phân tích Kỹ thuật và Triển khai Cốt lõi

### 2.1. Alpha-Beta Pruning cho Cờ Caro (Gomoku N x N)

Đây là giải pháp hợp lý nhất cho các bàn cờ lớn (N >= 5) khi Minimax thuần túy không khả thi. 

* **Alpha-Beta Pruning:** Sử dụng kỹ thuật cắt tỉa để giảm số lượng nút cần duyệt trong cây tìm kiếm.
* **Hàm Đánh giá Heuristic:** Gán giá trị số cho trạng thái bàn cờ trung gian. Điểm số được tính dựa trên:
    * Đếm số quân liên tiếp gần thắng (K-1, K-2).
    * Phân biệt giữa chuỗi bị chặn (đóng) và chuỗi mở (có thể mở rộng).
* **Giới hạn Độ sâu:** Bắt buộc phải giới hạn độ sâu tìm kiếm (MAX_DEPTH) để đảm bảo thời gian phản hồi hợp lý.

### 2.2. Cấu Trúc AI cho Game Phức tạp (Cờ Vua/Cờ Tướng)

Cấu trúc AI cho các trò chơi này dựa trên Alpha-Beta, nhưng hiệu suất phụ thuộc vào hai yếu tố chính:

* **Bộ tạo Nước đi Hợp lệ (Move Generator):** Phải mã hóa chính xác tất cả các quy tắc luật chơi và điều kiện kiểm tra chiếu tướng/chiếu hết.
* **Hàm Đánh giá (Evaluation Function):** Hàm này phải cân bằng giữa:
    * **Giá trị Vật chất:** Tổng điểm số cố định của các quân cờ.
    * **Giá trị Vị trí:** Thưởng hoặc phạt điểm dựa trên vị trí của quân cờ trên bàn. 

---

## 3. Hướng dẫn Vận hành và Giải quyết sự cố GUI

### 3.1. Môi trường Thực thi

* **Ngôn ngữ:** Python 3.x
* **Thư viện:** Tkinter (hoặc Pygame), Xvfb (để chạy GUI trên Colab).

### 3.2. Vấn đề Hiển thị GUI trên Colab

Do môi trường Colab là môi trường máy chủ, việc chạy các thư viện GUI (Pygame, Tkinter) đòi hỏi một máy chủ hiển thị ảo.

* **Giải pháp:** Sử dụng **Xvfb (X Virtual Framebuffer)** để mô phỏng một môi trường hiển thị.
* **Thứ tự Chạy (Quan trọng):**
    1.  Chạy các Cell định nghĩa hàm logic Minimax.
    2.  Chạy Cell cài đặt và khởi tạo Xvfb (`!apt-get install...`, `!Xvfb :99...`).
    3.  Chạy Cell chứa Class `TicTacToeGUI` và `root.mainloop()`.

**Ghi chú:** Nếu gặp lỗi môi trường (ví dụ: TclError), người dùng cần kiểm tra lại việc khởi động Xvfb và đảm bảo rằng biến môi trường DISPLAY đã được đặt đúng.

---

## 4. Kết luận

Dự án đã hoàn thành việc triển khai các thuật toán tìm kiếm nền tảng, minh họa sự chuyển đổi từ giải thuật tìm kiếm toàn bộ (Minimax 3x3) sang tìm kiếm dựa trên Heuristic và cắt tỉa (Alpha-Beta N x N) để giải quyết các trò chơi có độ phức tạp cao hơn.

------------------------------------------------------------------------------------------------------
# Tuần 04: CÁC PHƯƠNG PHÁP GIẢI BÀI TOÁN THỎA MÃN RÀNG BUỘC

## 1. Tóm tắt Các Yêu cầu Đã Triển khai

| STT | Bài tập | Lĩnh vực | Thuật toán Chính | Ghi chú |
| :--- | :--- | :--- | :--- | :--- |
| **1 & 2** | Đọc file ma trận `.txt` và tổ chức code. | Xử lý Dữ liệu/I/O | N/A | Tập trung vào tổ chức code module và hiển thị màu. |
| **3** | Bài toán Người bán hàng (TSP). | Tối ưu hóa Tuyến đường | Thuật toán Tham lam (Greedy) / Quy hoạch Động (DP) | Tìm chu trình chi phí tối thiểu qua N thành phố. |
| **BTVN** | Sắp xếp lịch học (Scheduling). | Thuật toán Mềm | **Giải thuật Di truyền (Genetic Algorithm)** | Tối ưu hóa lịch học PTTH dựa trên các ràng buộc. |

---

## 2. Chi tiết Triển khai Kỹ thuật

### 2.1. Bài toán Người bán hàng (Traveling Salesperson Problem - TSP)

TSP là một bài toán NP-Hard yêu cầu tìm chu trình ngắn nhất đi qua mọi đỉnh (thành phố) chỉ một lần.

* **Mô hình Dữ liệu:** Sử dụng ma trận kề để biểu diễn chi phí (quãng đường) giữa các thành phố.
* **Chiến lược Giải quyết (Ví dụ triển khai):**
    * **Tham lam (Nearest Neighbor):** Bắt đầu từ một thành phố và luôn chọn thành phố gần nhất chưa đi qua. Giải pháp nhanh, nhưng chỉ cho kết quả gần tối ưu.
    * **Quy hoạch Động (Held-Karp):** Cung cấp giải pháp tối ưu cho N nhỏ ($N \le 20$), nhưng có độ phức tạp cao $O(N^2 2^N)$.

### 2.2. Giải thuật Di truyền (Genetic Algorithm - GA) cho Sắp xếp Lịch

GA là một thuật toán tối ưu hóa dựa trên cơ chế tiến hóa tự nhiên, rất hiệu quả cho các bài toán Quy hoạch phức tạp với nhiều ràng buộc (như sắp xếp lịch học). 

* **Mô hình Hóa (Representation):**
    * **Chromosome (Gen):** Một chuỗi số hoặc đối tượng đại diện cho một lịch học hoàn chỉnh. Ví dụ: một mảng chứa thông tin [Giáo viên, Môn học, Lớp, Thời gian].
* **Hàm Thích nghi (Fitness Function):** Đánh giá chất lượng của lịch, điểm số càng cao nếu lịch càng thỏa mãn các ràng buộc:
    * **Ràng buộc Cứng (Hard Constraints):** Không vi phạm luật (Ví dụ: 1 giáo viên không thể dạy 2 lớp cùng lúc, số tiết học phải đủ). Vi phạm dẫn đến điểm Fitness rất thấp (gần 0).
    * **Ràng buộc Mềm (Soft Constraints):** Tính tối ưu (Ví dụ: Phân bố tiết học đều, không dạy quá nhiều tiết liên tiếp). Thỏa mãn giúp tăng điểm Fitness.
* **Các Toán tử Gen:**
    * **Selection (Chọn lọc):** Chọn ra các cá thể tốt nhất (lịch tốt nhất) để lai tạo (Ví dụ: Roulette Wheel, Tournament Selection).
    * **Crossover (Lai ghép):** Kết hợp gen của hai lịch tốt để tạo ra lịch mới (Ví dụ: Single-Point Crossover).
    * **Mutation (Đột biến):** Thay đổi ngẫu nhiên một phần nhỏ của lịch để khám phá các giải pháp mới và tránh bị mắc kẹt tại cực trị địa phương (Local Maxima).

---

## 3. Tổ chức Code và Xử lý Dữ liệu

### 3.1. Xử lý Ma trận và Tô màu

* **Đọc File:** Hàm `read_matrix_from_txt(file_path)` đọc dữ liệu từ file `.txt` và chuyển đổi thành cấu trúc ma trận (ví dụ: list of lists).
* **Tổ chức Code:** Mã nguồn được chia thành các chương trình con/Class (Ví dụ: Class `TSP_Solver`, Class `Scheduler_GA`) để đảm bảo tính module và dễ bảo trì.
* **Tô màu:** Sử dụng thư viện/kỹ thuật console color codes để tô màu các giá trị ma trận, giúp trực quan hóa dữ liệu (ví dụ: các giá trị cao/thấp).

---

## 4. Kết luận

Tuần 04 đã thành công trong việc chuyển đổi trọng tâm từ tìm kiếm logic sang **tìm kiếm tối ưu hóa**, với sự áp dụng của các thuật toán phức tạp và mạnh mẽ như TSP và Giải thuật Di truyền để giải quyết các bài toán về chi phí và quy hoạch trong thế giới thực.

---

------------------------------------------------------------------------------------------------------------------------------------

# Tuần 05: HỌC MÁY

## 1. Tóm tắt Các Yêu cầu Đã Triển khai

| STT | Bài tập | Kỹ thuật | Phân loại Học | Ghi chú |
| :--- | :--- | :--- | :--- | :--- |
| **I.1** | Cài đặt lại thuật toán K-Means | K-Means Clustering | Học không giám sát | Triển khai đầy đủ các hàm cốt lõi (khởi tạo, gán nhãn, cập nhật tâm). |
| **I.2** | Cài đặt lại thuật toán K-NN | K-Nearest Neighbors | Học có giám sát | Cài đặt thủ công và sử dụng `GridSearchCV` để tìm K tối ưu. |
| **I.3** | Cài đặt ứng dụng demo | K-Means & K-NN | Tổng hợp | Tích hợp hai thuật toán vào một ứng dụng trực quan. |
| **BTVN** | Mô tả và Demo Ứng dụng | K-Means, K-NN, Tổng hợp | Ứng dụng thực tế | Mô tả và cài đặt demo mở rộng các thuật toán đã học. |

---

## 2. Phân tích Kỹ thuật và Cài đặt

### 2.1. Kỹ thuật K-Means Clustering (Học không giám sát)

K-Means là một phương pháp đơn giản nhưng hiệu quả để chia dữ liệu thành K cụm dựa trên đặc trưng.

* **Mục tiêu:** Tìm giá trị cực tiểu của hàm mục tiêu J (tổng bình phương khoảng cách từ mỗi điểm dữ liệu đến tâm cụm gần nhất của nó).
* **Triển khai:**
    * **Khởi tạo:** Hàm `kmeans_init_centers` chọn K tâm cụm ngẫu nhiên từ tập dữ liệu.
    * **Gán nhãn:** Hàm `kmeans_predict_labels` gán nhãn cho mỗi điểm dữ liệu bằng cách tìm tâm cụm gần nhất.
    * **Cập nhật:** Hàm `kmeans_update_centers` tính lại tâm cụm là trung bình cộng của tất cả các điểm được gán vào cụm đó.
    * **Trực quan hóa:** Sử dụng thư viện `matplotlib` để vẽ các điểm dữ liệu và tâm cụm qua từng bước lặp, minh họa quá trình hội tụ.

### 2.2. Kỹ thuật K-Nearest Neighbors (K-NN) (Học có giám sát)

K-NN dùng để phân loại quan sát mới bằng cách so sánh điểm tương đồng với dữ liệu đã có nhãn.

* **Nguyên lý Phân loại:** Chọn $K$ điểm láng giềng gần nhất, sau đó gán nhãn cho điểm mới bằng nhãn có số lượng lớn nhất trong $K$ láng giềng đó (ví dụ: $K=5$, 3 tam giác, 2 chữ thập -> gán nhãn tam giác).
* **Cài đặt Hàm `KNN` thủ công:**
    * Tính khoảng cách Euclidean từ mỗi điểm kiểm tra đến tất cả điểm huấn luyện.
    * Sắp xếp khoảng cách theo chiều tăng dần.
    * Đếm số lượng của mỗi lớp trong top K láng giềng để đưa ra quyết định phân loại.
* **Tìm K Tối ưu (Bài 2):**
    * **Phương pháp 1 (Nhìn hình):** Huấn luyện và đánh giá trực quan với $K=1$ và $K=5$ để so sánh kết quả.
    * **Phương pháp 2 (Tự động):** Sử dụng `GridSearchCV` của thư viện `scikit-learn` kết hợp với Cross-Validation (cv=5) để tự động kiểm tra nhiều giá trị $K$ (từ 1 đến 10) và tìm ra giá trị $K$ mang lại độ chính xác cao nhất.

---

## 3. Bài tập Ứng dụng Demo (Bài 4 & 5)

Các bài tập này yêu cầu mô tả và cài đặt demo ứng dụng thực tế cho các thuật toán đã học:

### 3.1. Ứng dụng Demo K-Means và K-NN (Bài 4)

* **K-Means:** * **Mô tả:** Phân khúc khách hàng (Customer Segmentation) dựa trên các đặc trưng như tuổi, thu nhập và tần suất mua hàng.
    * **Demo:** Cài đặt demo K-Means để phân chia dữ liệu khách hàng thành các nhóm mục tiêu khác nhau.
* **K-NN:** * **Mô tả:** Phân loại bệnh tật (Disease Classification) hoặc Phân loại ảnh (Image Classification) dựa trên các điểm đặc trưng.
    * **Demo:** Cài đặt demo K-NN để phân loại một điểm dữ liệu mới vào một trong các lớp đã huấn luyện.

### 3.2. Ứng dụng Tổng hợp (Bài 5)

Bài 5 yêu cầu tổng hợp và mô tả ứng dụng của tất cả các thuật toán đã học (Minimax, Alpha-Beta, TSP, Genetic Algorithm, K-Means, K-NN). Ví dụ:

* **Genetic Algorithm (GA):** Ứng dụng vào Tối ưu hóa thiết kế (ví dụ: tìm hình dạng cánh máy bay tối ưu) hoặc Sắp xếp lịch học phức tạp.
* **TSP:** Ứng dụng vào Tối ưu hóa chuỗi cung ứng và định tuyến xe giao hàng.
* **Minimax/Alpha-Beta:** Ứng dụng vào các game chiến thuật hoặc mô hình hóa các quyết định trong giao dịch tài chính.

---

## 4. Kết luận

Tuần 05 đã hoàn thành việc nắm vững các kỹ thuật học máy cơ bản, cung cấp nền tảng vững chắc để phân loại dữ liệu (K-NN) và phân tích cấu trúc dữ liệu không giám sát (K-Means), đồng thời mở rộng khả năng ứng dụng tổng hợp các thuật toán AI đã học.

