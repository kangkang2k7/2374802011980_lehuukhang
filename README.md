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


#LAB CNN

## Câu 1: Thay đổi số lượng epoch

- **Yêu cầu:** Tăng số epoch từ 5 lên 10.
- **Kết quả:** Độ chính xác tăng, loss giảm dần qua các epoch.
- **Giải thích:** Tăng epoch giúp mô hình học kỹ hơn, giảm underfitting, nhưng quá nhiều có thể gây overfitting.

```python
for epoch in range(10):  # tăng từ 5 lên 10
    # Huấn luyện và tính loss, accuracy
    ...
    print(f"Epoch {epoch+1}, Loss: {epoch_loss:.4f}, Accuracy: {epoch_accuracy:.2f}%")
Câu 2: Thêm tầng tích chập thứ ba
Yêu cầu: Thêm conv3 vào mô hình.
class MNIST_CNN(nn.Module):
    def __init__(self):
        super().__init__()
        self.conv1 = nn.Conv2d(1, 16, 3)
        self.conv2 = nn.Conv2d(16, 32, 3)
        self.conv3 = nn.Conv2d(32, 64, 3)  # thêm conv3
        self.pool = nn.MaxPool2d(2, 2)
        self.fc1 = nn.Linear(64 * 1 * 1, 10)

    def forward(self, x):
        x = self.pool(torch.relu(self.conv1(x)))
        x = self.pool(torch.relu(self.conv2(x)))
        x = self.pool(torch.relu(self.conv3(x)))  # thêm conv3
        x = x.view(-1, 64 * 1 * 1)
        x = self.fc1(x)
        return x
Hiệu quả: Tầng conv3 giúp học được đặc trưng phức tạp hơn, cải thiện độ chính xác.

Câu 3: Thay đổi learning rate
Yêu cầu: Thử learning rate 0.001 và 0.1.

Kết quả: LR thấp học ổn định nhưng chậm, LR cao học nhanh nhưng dễ dao động.
optimizer = optim.SGD(model.parameters(), lr=0.001, momentum=0.9)  # LR thấp
# hoặc
optimizer = optim.SGD(model.parameters(), lr=0.1, momentum=0.9)  # LR cao
Câu 4: Trực quan hóa feature map tầng conv2
Yêu cầu: Vẽ thêm feature map từ conv2.
def visualize_feature_map():
    model.eval()
    images, _ = next(iter(test_loader))
    img = images[0].unsqueeze(0).to(device)

    conv1_output = torch.relu(model.conv1(img))
    conv2_output = torch.relu(model.conv2(model.pool(conv1_output)))

    plt.figure(figsize=(20, 4))

    plt.subplot(1, 5, 1)
    plt.title("Ảnh gốc")
    plt.imshow(img.cpu().squeeze(), cmap='gray')
    plt.axis('off')

    plt.subplot(1, 5, 2)
    plt.title("Feature Map conv1 - 1")
    plt.imshow(conv1_output[0, 0].cpu().detach().numpy(), cmap='gray')
    plt.axis('off')

    plt.subplot(1, 5, 3)
    plt.title("Feature Map conv1 - 2")
    plt.imshow(conv1_output[0, 1].cpu().detach().numpy(), cmap='gray')
    plt.axis('off')

    plt.subplot(1, 5, 4)
    plt.title("Feature Map conv2 - 1")
    plt.imshow(conv2_output[0, 0].cpu().detach().numpy(), cmap='gray')
    plt.axis('off')

    plt.subplot(1, 5, 5)
    plt.title("Feature Map conv2 - 2")
    plt.imshow(conv2_output[0, 1].cpu().detach().numpy(), cmap='gray')
    plt.axis('off')

    plt.show()
Ý nghĩa: Feature map conv2 chi tiết hơn, trừu tượng hơn so với conv1.

Kết luận chung
Số lượng epoch, kiến trúc mạng, learning rate đều ảnh hưởng rõ rệt đến kết quả.

Tăng độ sâu mạng giúp học đặc trưng phức tạp hơn.

Learning rate cần điều chỉnh phù hợp để cân bằng tốc độ và độ ổn định.

Trực quan feature map giúp hiểu cách mạng học và trích xuất đặc trưng.
