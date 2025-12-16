# Tuần 03: GIẢI THUẬT TÌM KIẾM ĐỐI KHÁNG

## 1. Tóm tắt các yêu cầu đã triển khai

| STT | Bài tập | Thuật toán | Ma trận Ứng dụng | Ghi chú |
| :--- | :--- | :--- | :--- | :--- |
| **BTTL 1** | Cài đặt Minimax | Minimax | 3x3 | Thuật toán cốt lõi. |
| **BTTL 2** | Cài đặt Cắt tỉa Alpha-beta | Alpha-Beta Pruning | 3x3 | Tối ưu hóa tốc độ tìm kiếm. |
| **BTVN 3 & 4** | Mở rộng Minimax & Alpha-beta | Minimax & Alpha-Beta Pruning | NxN (5x5, 10x10) | Yêu cầu phải sử dụng Hàm Lượng Giá Heuristic. |
| **BTVN 5** | Ứng dụng Alpha-beta | Alpha-Beta Pruning | Cờ Tướng, Cờ Vua, Cờ Vây | Phân tích lý thuyết về hàm Heuristic và Move Generator. |
| **BTVN 6** | Xây dựng Giao diện Đồ họa | Tkinter/OpenCV | 3x3 | Tích hợp AI vào giao diện người dùng. |

---

## 2. Phân tích thuật toán cốt lõi

### 2.1. Cấu trúc trò chơi 

Thuật toán được xây dựng dựa trên các thành phần cơ bản của lý thuyết trò chơi:

* **Trạng thái ban đầu (Initial State):** Ma trận trò chơi rỗng + Xác định người chơi bắt đầu (X hoặc O).
* **Hàm chuyển trạng thái (Successor):** Trả về trạng thái mới sau khi thực hiện một nước đi hợp lệ.
* **Hàm lợi ích (Utility Function):** Đánh giá kết quả cuối cùng: +1 (X thắng), -1 (O thắng), 0 (Hòa).
* **Hàm Lượng giá Heuristic E(n):** Được sử dụng cho các ma trận lớn (NxN) khi tìm kiếm tuyệt đối không khả thi: $E(n) = X(n) - O(n)$ (Số khả năng thắng của X trừ đi số khả năng thắng của O).

### 2.2. Thuật toán Minimax

* **Nguyên tắc:** MAX (người chơi hiện tại) luôn cố gắng tối đa hóa Hàm Lợi ích, trong khi MIN (đối thủ) luôn cố gắng tối thiểu hóa Hàm Lợi ích.
* **Triển khai:**
    * Hàm `maxValue(state)`: Tìm nước đi tốt nhất cho MAX (tìm giá trị lớn nhất).
    * Hàm `minValue(state)`: Tìm nước đi tốt nhất cho MIN (tìm giá trị nhỏ nhất).
    * Thuật toán duyệt toàn bộ cây trò chơi cho đến trạng thái kết thúc (`terminal(state)`).

### 2.3. Thuật toán cắt tỉa Alpha-beta (Alpha-Beta Pruning)

Alpha-beta là một tối ưu hóa của Minimax, cho phép loại bỏ các nhánh cây tìm kiếm không cần thiết mà không ảnh hưởng đến kết quả cuối cùng.

* **Nguyên tắc cắt tỉa:** Việc cắt tỉa xảy ra khi $\alpha \ge \beta$. 
    * $\alpha$ (alpha): Giá trị tốt nhất mà MAX có thể đảm bảo được tính đến thời điểm hiện tại. (Luôn tăng)
    * $\beta$ (beta): Giá trị tốt nhất mà MIN có thể đảm bảo được tính đến thời điểm hiện tại. (Luôn giảm)
* **Giải thích:** Nếu tại một nút MIN, giá trị $\beta$ hiện tại (ví dụ: $\beta \le 3$) nhỏ hơn hoặc bằng giá trị $\alpha$ đã được đảm bảo ở nút MAX cha (ví dụ: $\alpha \ge 10$), thì nhánh đó sẽ không bao giờ được chọn, và việc tìm kiếm ở các nút con còn lại sẽ bị dừng (cắt tỉa).

---

## 3. BTVN

### 3.1. Ứng dụng cho ma trận $N \times N$ (Bài 3 & 4)

* **Vấn đề:** Khi kích thước $N$ tăng ($N=5, 10$), không gian trạng thái bùng nổ, Minimax vét cạn không khả thi.
* **Giải pháp:** Phải sử dụng **Cắt tỉa Alpha-beta** và giới hạn độ sâu (Depth-Limited Search), kết hợp với **Hàm Lượng giá Heuristic $E(n)$** để ước lượng giá trị của các trạng thái không kết thúc.

### 3.2. Ứng dụng vào game Cờ phức tạp (Bài 5)

Việc ứng dụng Alpha-beta cho Cờ Tướng/Vua/Vây đòi hỏi các thành phần phức tạp hơn:

* **Tạo nước đi hợp lệ:** Phải mã hóa toàn bộ luật chơi phức tạp (như luật chiếu, bắt quân).
* **Hàm đánh giá:** Hàm Heuristic phức tạp, tính toán không chỉ lợi thế vật chất mà còn lợi thế vị trí, khả năng tấn công/phòng thủ, và các yếu tố chiến thuật khác.

---

## 4. Giao diện đồ họa (Bài 6)

* **Công cụ:** Sử dụng thư viện `Tkinter` (hoặc `OpenCV` như trong ví dụ `Thuật giải Minimax 2`) để xây dựng GUI.
* **Tích hợp AI:** Lớp `GUI` hoặc hàm `mainLoop` gọi hàm `minimax` hoặc `FindBestMove` (sử dụng Alpha-beta) để xác định nước đi của máy tính và cập nhật trạng thái bảng.
------------------------------------------------------------------------------------------------------
# Tuần 04: CÁC PHƯƠNG PHÁP GIẢI BÀI TOÁN THỎA MÃN RÀNG BUỘC

## 1. Tóm tắt Các Yêu cầu Đã Triển khai

| STT | Bài tập | Lĩnh vực | Thuật toán Chính | Ghi chú |
| :--- | :--- | :--- | :--- | :--- |
| **1 & 2** | Đọc file ma trận `.txt` và tổ chức code. | Xử lý Dữ liệu/I/O | N/A | Tập trung vào tổ chức code module và hiển thị màu. |
| **3** | Bài toán Người bán hàng (TSP). | Tối ưu hóa Tuyến đường | Thuật toán Tham lam  / Quy hoạch động  | Tìm chu trình chi phí tối thiểu qua N thành phố. |
| **BTVN** | Sắp xếp lịch học (Scheduling). | Thuật toán Mềm | **Giải thuật Di truyền ** | Tối ưu hóa lịch học PTTH dựa trên các ràng buộc. |

---

## 2. Chi tiết triển khai kỹ thuật

### 2.1. Bài toán người bán hàng

TSP là một bài toán NP-Hard yêu cầu tìm chu trình ngắn nhất đi qua mọi đỉnh (thành phố) chỉ một lần.

* **Mô hình Dữ liệu:** Sử dụng ma trận kề để biểu diễn chi phí (quãng đường) giữa các thành phố.
* **Chiến lược Giải quyết (Ví dụ triển khai):**
    * **Tham lam:** Bắt đầu từ một thành phố và luôn chọn thành phố gần nhất chưa đi qua. Giải pháp nhanh, nhưng chỉ cho kết quả gần tối ưu.
    * **Quy hoạch Động:** Cung cấp giải pháp tối ưu cho N nhỏ ($N \le 20$), nhưng có độ phức tạp cao $O(N^2 2^N)$.

### 2.2. Giải thuật di truyền cho sắp xếp lịch

GA là một thuật toán tối ưu hóa dựa trên cơ chế tiến hóa tự nhiên, rất hiệu quả cho các bài toán Quy hoạch phức tạp với nhiều ràng buộc (như sắp xếp lịch học). 

* **Mô hình Hóa:**
    * **Chromosome (Gen):** Một chuỗi số hoặc đối tượng đại diện cho một lịch học hoàn chỉnh. Ví dụ: một mảng chứa thông tin [Giáo viên, Môn học, Lớp, Thời gian].
* **Hàm thích nghi :** Đánh giá chất lượng của lịch, điểm số càng cao nếu lịch càng thỏa mãn các ràng buộc:
    * **Ràng buộc cứng:** Không vi phạm luật (Ví dụ: 1 giáo viên không thể dạy 2 lớp cùng lúc, số tiết học phải đủ). Vi phạm dẫn đến điểm Fitness rất thấp (gần 0).
    * **Ràng buộc mềm :** Tính tối ưu (Ví dụ: Phân bố tiết học đều, không dạy quá nhiều tiết liên tiếp). Thỏa mãn giúp tăng điểm Fitness.
* **Các Toán tử Gen:**
    * **Selection (Chọn lọc):** Chọn ra các lịch tốt nhất để đề xuất (Ví dụ: Roulette Wheel, Tournament Selection).
    * **Kết hợp:** Kết hợp thời gian của hai lịch tốt để tạo ra lịch mới (Ví dụ: Single-Point Crossover).
    * **Ngẫu biến:** Thay đổi ngẫu nhiên một phần nhỏ của lịch để khám phá các giải pháp mới và tránh bị mắc kẹt tại cực trị địa phương (Local Maxima).

---

## 3. Tổ chức Code và Xử lý Dữ liệu

### 3.1. Xử lý Ma trận và Tô màu

* **Đọc File:** Hàm `read_matrix_from_txt(file_path)` đọc dữ liệu từ file `.txt` và chuyển đổi thành cấu trúc ma trận (ví dụ: list of lists).
* **Tổ chức Code:** Mã nguồn được chia thành các chương trình con/Class (Ví dụ: Class `TSP_Solver`, Class `Scheduler_GA`) để đảm bảo tính module và dễ bảo trì.
* **Tô màu:** Sử dụng thư viện/kỹ thuật console color codes để tô màu các giá trị ma trận, giúp trực quan hóa dữ liệu (ví dụ: các giá trị cao/thấp).

---

## 4. Kết luận

Tuần 04 đã thành công trong việc chuyển đổi trọng tâm từ tìm kiếm logic sang **tìm kiếm tối ưu hóa**, với sự áp dụng của các thuật toán phức tạp và mạnh mẽ như TSP và Giải thuật Di truyền để giải quyết các bài toán về chi phí và quy hoạch trong thế giới thực.

------------------------------------------------------------------------------------------------------------------------------------

# Tuần 05: HỌC MÁY

## 1. Tóm tắt Các yêu cầu đã triển khai

| STT | Bài tập | Kỹ thuật | Phân loại Học | Ghi chú |
| :--- | :--- | :--- | :--- | :--- |
| **I.1** | Cài đặt lại thuật toán K-Means | K-Means Clustering | Học không giám sát | Triển khai đầy đủ các hàm cốt lõi (khởi tạo, gán nhãn, cập nhật tâm). |
| **I.2** | Cài đặt lại thuật toán K-NN | K-Nearest Neighbors | Học có giám sát | Cài đặt thủ công và sử dụng `GridSearchCV` để tìm K tối ưu. |
| **I.3** | Cài đặt ứng dụng demo | K-Means & K-NN | Tổng hợp | Tích hợp hai thuật toán vào một ứng dụng trực quan. |
| **BTVN** | Mô tả và Demo Ứng dụng | K-Means, K-NN, Tổng hợp | Ứng dụng thực tế | Mô tả và cài đặt demo mở rộng các thuật toán đã học. |

---

## 2. Phân tích kỹ thuật và cài đặt

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

* **Nguyên lý phân loại:** Chọn $K$ điểm láng giềng gần nhất, sau đó gán nhãn cho điểm mới bằng nhãn có số lượng lớn nhất trong $K$ láng giềng đó (ví dụ: $K=5$, 3 tam giác, 2 chữ thập -> gán nhãn tam giác).
* **Cài đặt hàm `KNN` thủ công:**
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

