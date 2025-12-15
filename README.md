# Bài 1: GIẢI THUẬT TÌM KIẾM ĐỐI KHÁNG
# DỰ ÁN: TRIỂN KHAI THUẬT TOÁN TÌM KIẾM TRÍ TUỆ NHÂN TẠO (AI Search Algorithms)

Dự án này tập trung vào việc triển khai và ứng dụng các thuật toán tìm kiếm tối ưu (Minimax và Cắt tỉa Alpha-beta) vào các trò chơi chiến thuật, dựa trên yêu cầu của Bài tập tuần 3.

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
