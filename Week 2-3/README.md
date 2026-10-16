# Week 2-3 — README

Tệp: Week 2-3/KLTN_W2.ipynb

Mô tả
-----
Notebook này chứa các bước tiền xử lý và trực quan hóa dữ liệu tỉ giá USD/VND. Mục tiêu chính:
- Đọc dữ liệu lịch sử (CSV) của tỉ giá USD/VND.
- Tính các chỉ số đơn giản (Mid, Range).
- Chia dữ liệu thành 3 tập: Train (70%), Validation (15%), Test (15%).
- Vẽ biểu đồ để kiểm tra phân phối thời gian và vùng chia tập dữ liệu.

Nội dung chính của notebook
---------------------------
1. Import các thư viện: pandas, matplotlib, numpy.
2. Đọc file CSV (hiện tại đường dẫn trong notebook là tuyệt đối: `D:/KLTN/Week 1/VND=X.csv`).
3. Hiển thị một phần DataFrame (các cột: Close, High, Low, Open, Volume, Mid, Range).
4. Tính chỉ số độ dài dữ liệu và xác định chỉ số chia cho train/val/test (70%/15%/15%).
5. Vẽ các biểu đồ:
   - Biểu đồ High và Low theo thời gian với các đường vertical hiển thị ranh giới train/val/test.
   - Hai đồ thị xếp dọc: Mid (trên) và Range (dưới) cùng các đường chia tập dữ liệu.

Yêu cầu hệ thống & phụ thuộc
---------------------------
- Python 3.8+ (notebook ghi `3.13.9`, nhưng Python 3.8+ là đủ tốt).
- Thư viện Python:
  - pandas
  - matplotlib
  - numpy

Bạn có thể cài bằng pip:

pip install pandas matplotlib numpy

Dữ liệu (CSV)
------------
Notebook hiện đang đọc file từ đường dẫn tuyệt đối:

    D:/KLTN/Week 1/VND=X.csv

Để dễ chia sẻ và chạy lại, khuyến nghị:
- Tạo thư mục `data/` trong repo và đặt `VND=X.csv` vào `data/VND=X.csv`.
- Sửa lại dòng đọc file trong notebook thành:

    df = pd.read_csv("data/VND=X.csv", index_col="Date", parse_dates=True)

Hướng dẫn chạy
--------------
1. Mở repository trong Jupyter Notebook hoặc JupyterLab.
2. Mở `Week 2-3/KLTN_W2.ipynb`.
3. Nếu cần, chỉnh lại đường dẫn tới file CSV như mục Dữ liệu ở trên.
4. Chạy lần lượt các ô (Run all) để xem kết quả và biểu đồ.

Ghi chú
------
- Notebook tập trung vào trực quan hóa và kiểm tra chia tập dữ liệu; không bao gồm phần huấn luyện mô hình GRU hay Monte Carlo Dropout (những phần này có thể xuất hiện ở các notebook khác trong repo).
- Nếu bạn muốn tái tạo quy trình (training và đánh giá), cần thêm các cell/khối mã cho việc chuẩn hóa, tạo window dữ liệu, định nghĩa mô hình, huấn luyện và chạy MC Dropout.

Liên hệ
-------
Nếu cần bổ sung nội dung hoặc sửa đường dẫn dữ liệu, mở issue hoặc gửi pull request.
