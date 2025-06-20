# 2374802011980_lehuukhang
#lab2
Bài toán N-Queens yêu cầu đặt N quân hậu trên bàn cờ kích thước N x N sao cho:
Không có hai quân hậu nào nằm trên cùng hàng.
Không có hai quân hậu nào nằm trên cùng cột.
Không có hai quân hậu nào nằm trên cùng đường chéo chính hoặc phụ.
🧰 Công cụ sử dụng
Python 3.x
Thư viện: numpy, random
Cài đặt thư viện (nếu chưa có)
pip install numpy
🧠 Giải thuật chính
1. is_valid_state(state, num_queens)
Kiểm tra xem một trạng thái đã hoàn chỉnh chưa (đã đặt đủ N quân hậu).

2. get_candidates(state, num_queens)
Trả về danh sách các cột hợp lệ mà quân hậu có thể đặt tiếp theo, dựa trên:
Cột đã bị chiếm.
Hai đường chéo đã bị chiếm.
3. search(state, solutions, num_queens)
Thuật toán đệ quy backtracking:
Gọi đệ quy với từng ứng viên hợp lệ.
Nếu đạt trạng thái đầy đủ → thêm vào danh sách lời giải.
Nếu không hợp lệ → quay lui.
4. solve(num_queens)
Gọi hàm search và trả về tất cả các lời giải tìm được.
▶️ Cách chạy chương trình
File n_queens.py:
python n_queens.py
Khi được hỏi:
Nhap vao so quan hau N = 
→ Bạn có thể nhập 4 hoặc 8, ví dụ:
Nhap vao so quan hau N = 8
🧪 Ví dụ đầu ra
Nhập: N = 4
 Tổng số lời giải tìm được: 2
Lời giải 1:
Quân hậu tại dòng 0, cột 1
Quân hậu tại dòng 1, cột 3
Quân hậu tại dòng 2, cột 0
Quân hậu tại dòng 3, cột 2

Lời giải 2:
Quân hậu tại dòng 0, cột 2
Quân hậu tại dòng 1, cột 0
Quân hậu tại dòng 2, cột 3
Quân hậu tại dòng 3, cột 1
