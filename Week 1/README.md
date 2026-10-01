# Tiền xử lý dữ liệu Tỷ giá USD/VND (Data Preprocessing for USD/VND)

## 📌 Giới thiệu
Dự án này thực hiện quy trình thu thập, phân tích và tiền xử lý chuỗi thời gian cho tỷ giá hối đoái USD/VND[cite: 1]. Mục tiêu chính là phân rã dữ liệu thô thành các thành phần có ý nghĩa (Midpoint và Range), sau đó chia tập dữ liệu và chuẩn hóa (Interval Scaler) nhằm chuẩn bị đầu vào chất lượng cao cho các mô hình học sâu như mạng nơ-ron hồi quy (GRU).

## 🛠️ Thư viện sử dụng (Dependencies)
Để chạy được mã nguồn trong dự án này, bạn cần cài đặt các thư viện Python sau:
* `pandas`
* `numpy`
* `matplotlib`
* `yfinance`
* `scikit-learn`

## 🚀 Quy trình thực hiện (Workflow)

### 1. Thu thập dữ liệu (Data Pulling)
* Truy xuất dữ liệu tỷ giá USD/VND (mã ticker: `VND=X`) trực tiếp từ **Yahoo Finance** bằng thư viện `yfinance`.
* Giai đoạn thu thập: Từ ngày **01/01/2020** đến **31/08/2026**.

### 2. Phân rã chuỗi thời gian (Time-series Decomposition)
Từ tập dữ liệu gốc bao gồm giá Đóng cửa (Close), Mở cửa (Open), Cao nhất (High) và Thấp nhất (Low), chuỗi dữ liệu được phân rã thành 2 biến mục tiêu chính:
* **Midpoint (\(m_t\))**: Tính bằng trung bình cộng của giá cao nhất và thấp nhất `(High + Low) / 2`.
* **Range (\(\epsilon_t\))**: Khổ độ giao động giá trong ngày, tính bằng `High - Low`.

### 3. Chia tập dữ liệu (Data Splitting)
Dữ liệu chuỗi thời gian được chia thành 3 tập để huấn luyện và đánh giá theo tỷ lệ **70 / 15 / 15**:
* **Train**: 70% dữ liệu đầu (khoảng 1213 mẫu).
* **Validation**: 15% dữ liệu tiếp theo (khoảng 260 mẫu).
* **Test**: 15% dữ liệu cuối cùng (khoảng 260 mẫu).
> **Lưu ý quan trọng**: Khi sử dụng hàm `train_test_split`, tham số `shuffle=False` được thiết lập nhằm giữ nguyên tính tuần tự về mặt thời gian của chuỗi dữ liệu.

### 4. Chuẩn hóa dữ liệu (Scaling)
* Sử dụng phương pháp **Interval Scaling** (thông qua hàm `MinMaxScaler` của scikit-learn) để ánh xạ toàn bộ tập dữ liệu về khoảng giá trị `[0, 1]`.
* Nhằm tránh rò rỉ dữ liệu (Data Leakage), việc chuẩn hóa được thực hiện **sau khi chia tập dữ liệu**. Bộ Scaler chỉ học các tham số trên tập Train, sau đó áp dụng (transform) lên các tập Validation và Test.

### 5. Xuất dữ liệu (Export to CSV)
Các tập dữ liệu (Train, Val, Test) sau khi được phân rã và chuẩn hóa được xuất ra định dạng `.csv` để lưu trữ và nạp vào mô hình máy học ở bước tiếp theo.
* Ví dụ: `Midpoint_train.csv`, `Midpoint_test.csv`, v.v...

## 🧠 Định hướng tiếp theo (Next Steps)
Sau khi hoàn thành bước tiền xử lý, dữ liệu đã sẵn sàng để được huấn luyện với **Mô hình GRU (Gated Recurrent Unit)** để giải quyết bài toán dự báo tỷ giá chuỗi thời gian.