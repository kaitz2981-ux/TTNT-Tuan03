# Bài 1: GIẢI THUẬT TÌM KIẾM ĐỐI KHÁNG

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

------------------------------------------------------------------------------------------------------
# Bài 2: CÁC PHƯƠNG PHÁP GIẢI BÀI TOÁN THỎA MÃN RÀNG BUỘC

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

## 4. Kết luận

Dự án đã hoàn thành việc triển khai các thuật toán tìm kiếm nền tảng, minh họa sự chuyển đổi từ giải thuật tìm kiếm toàn bộ (Minimax 3x3) sang tìm kiếm dựa trên Heuristic và cắt tỉa (Alpha-Beta N x N) để giải quyết các trò chơi có độ phức tạp cao hơn.
