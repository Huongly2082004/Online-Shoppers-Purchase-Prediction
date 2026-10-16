# Online Shoppers Purchase Prediction

## 1. Giới thiệu đề tài

Đề tài xây dựng hệ thống dự đoán khả năng mua hàng của một phiên truy cập trong môi trường thương mại điện tử dựa trên dữ liệu hành vi của các phiên truy cập website.

Mỗi bản ghi trong bộ dữ liệu tương ứng với một phiên truy cập website. Mục tiêu là sử dụng các đặc trưng hành vi và thông tin của phiên truy cập để dự đoán phiên đó có phát sinh mua hàng hay không.

## 2. Dataset

### 2.1. Thông tin bộ dữ liệu

Tên bộ dữ liệu: Online Shoppers Purchasing Intention Dataset

Nguồn dữ liệu: UCI Machine Learning Repository

DOI: 10.24432/C5F88Q

Đơn vị quan sát: Một phiên truy cập website

Biến mục tiêu: Revenue

Dữ liệu ban đầu gồm:

- 12.330 phiên truy cập
- 18 cột
- 17 đặc trưng đầu vào
- 1 biến mục tiêu là Revenue

### 2.2. Biến mục tiêu

Biến Revenue cho biết phiên truy cập có phát sinh mua hàng hay không.

- False: Không phát sinh mua hàng
- True: Có phát sinh mua hàng

Phân bố biến mục tiêu:

| Revenue | Số lượng phiên | Tỷ lệ (%) |
|---|---:|---:|
| False | 10.297 | 84,37 |
| True | 1.908 | 15,63 |

Dữ liệu có sự mất cân bằng giữa hai lớp. Vì vậy, khi xây dựng và đánh giá mô hình, không chỉ sử dụng Accuracy mà cần xem xét thêm các chỉ số phù hợp với dữ liệu mất cân bằng.

## 3. Các đặc trưng của dữ liệu

Các đặc trưng trong bộ dữ liệu gồm:

- Administrative
- Administrative_Duration
- Informational
- Informational_Duration
- ProductRelated
- ProductRelated_Duration
- BounceRates
- ExitRates
- PageValues
- SpecialDay
- Month
- OperatingSystems
- Browser
- Region
- TrafficType
- VisitorType
- Weekend

Trong đó:

- Các đặc trưng Administrative, Informational, ProductRelated thể hiện số lượng trang thuộc các nhóm nội dung mà phiên truy cập truy cập.
- Các đặc trưng có hậu tố `_Duration` thể hiện thời gian truy cập tương ứng.
- BounceRates và ExitRates thể hiện các chỉ số liên quan đến hành vi rời khỏi website.
- PageValues thể hiện giá trị trang trong phiên truy cập.
- Month, OperatingSystems, Browser, Region, TrafficType và VisitorType cung cấp thông tin về thời điểm và đặc điểm của phiên truy cập.
- Weekend cho biết phiên truy cập có diễn ra vào cuối tuần hay không.

## 4. Kiểm tra và loại bỏ bản ghi trùng

Dữ liệu ban đầu được kiểm tra các bản ghi trùng lặp trước khi thực hiện các bước xử lý tiếp theo.

Kết quả kiểm tra:

- Số dòng ban đầu: 12.330
- Số bản ghi trùng: 125
- Số dòng sau khi loại bỏ bản ghi trùng: 12.205

Các bản ghi trùng được loại bỏ bằng phương thức `drop_duplicates()` của Pandas.

Dữ liệu sau khi loại bỏ bản ghi trùng được lưu tại:

`data/processed/online_shoppers_deduplicated.csv`

## 5. Kiểm tra giá trị thiếu

Sau khi loại bỏ bản ghi trùng, dữ liệu được kiểm tra giá trị thiếu.

Kết quả:

- Tổng số giá trị thiếu: 0
- Không có đặc trưng nào chứa giá trị thiếu.

## 6. Thống kê mô tả

Dữ liệu được thực hiện thống kê mô tả nhằm kiểm tra đặc điểm phân bố của các đặc trưng số.

Các thống kê được xem xét gồm:

- Số lượng quan sát
- Giá trị trung bình
- Độ lệch chuẩn
- Giá trị nhỏ nhất
- Phân vị 25%
- Trung vị (50%)
- Phân vị 75%
- Giá trị lớn nhất

Kết quả thống kê mô tả được lưu tại:

`results/descriptive_statistics.csv`

## 7. Phân bố các biến phân loại

### 7.1. Biến Month

Phân bố số lượng phiên truy cập theo tháng:

| Month | Số lượng phiên |
|---|---:|
| May | 3.329 |
| Nov | 2.982 |
| Mar | 1.860 |
| Dec | 1.706 |
| Oct | 549 |
| Sep | 448 |
| Aug | 433 |
| Jul | 432 |
| June | 285 |
| Feb | 181 |

### 7.2. Biến VisitorType

Phân bố loại phiên truy cập:

| VisitorType | Số lượng phiên |
|---|---:|
| Returning_Visitor | 10.431 |
| New_Visitor | 1.693 |
| Other | 81 |

## 8. Mã hóa dữ liệu

Các biến phân loại được mã hóa để chuyển đổi dữ liệu về dạng có thể sử dụng làm đầu vào cho các mô hình dự đoán.

Sau khi mã hóa:

- Kích thước dữ liệu: 12.205 × 29
- Số đặc trưng đầu vào: 28
- Biến mục tiêu: Revenue

Các đặc trưng đầu vào sau khi mã hóa gồm:

- Administrative
- Administrative_Duration
- Informational
- Informational_Duration
- ProductRelated
- ProductRelated_Duration
- BounceRates
- ExitRates
- PageValues
- SpecialDay
- OperatingSystems
- Browser
- Region
- TrafficType
- Weekend
- Month_Aug
- Month_Dec
- Month_Feb
- Month_Jul
- Month_June
- Month_Mar
- Month_May
- Month_Nov
- Month_Oct
- Month_Sep
- VisitorType_New_Visitor
- VisitorType_Other
- VisitorType_Returning_Visitor

Dữ liệu sau xử lý được lưu tại:

`data/processed/online_shoppers_processed.csv`

## 9. Chia dữ liệu

Dữ liệu được chia thành ba tập Train, Validation và Test.

| Tập dữ liệu | Số dòng | Số đặc trưng |
|---|---:|---:|
| Train | 7.323 | 28 |
| Validation | 2.441 | 28 |
| Test | 2.441 | 28 |

Tỷ lệ phân bố biến mục tiêu được duy trì gần tương đương giữa ba tập.

### Train

- False: 84,36%
- True: 15,64%

### Validation

- False: 84,39%
- True: 15,61%

### Test

- False: 84,35%
- True: 15,65%

## 10. Chuẩn hóa dữ liệu

Các đặc trưng đầu vào được chuẩn hóa trước khi sử dụng cho các bước xây dựng mô hình.

Kích thước dữ liệu sau chuẩn hóa:

- Train: 7.323 × 28
- Validation: 2.441 × 28
- Test: 2.441 × 28

## 11. Cấu trúc thư mục

Online-Shoppers-Purchase-Prediction/
│
├── data/
│   ├── raw/
│   │   └── online_shoppers_intention.csv
│   │
│   └── processed/
│       ├── online_shoppers_deduplicated.csv
│       └── online_shoppers_processed.csv
│
├── notebooks/
│   └── 01_data_preparation.ipynb
│
├── src/
│
├── results/
│   └── descriptive_statistics.csv
│
├── requirements.txt
└── README.md

## 12. Sản phẩm bàn giao

Các sản phẩm của đề tài bao gồm:

- Dữ liệu gốc của bộ dữ liệu Online Shoppers Purchasing Intention Dataset.
- Dữ liệu sau khi loại bỏ các bản ghi trùng lặp.
- Số liệu thống kê mô tả của dữ liệu.
- Notebook thực hiện quá trình tiền xử lý và phân tích dữ liệu.
- Mã nguồn và cấu trúc thư mục của dự án được lưu trữ trên GitHub.

Các tệp dữ liệu chính:

- `data/raw/online_shoppers_intention.csv`: Dữ liệu gốc.
- `data/processed/online_shoppers_deduplicated.csv`: Dữ liệu sau khi loại bỏ bản ghi trùng lặp.
- `results/descriptive_statistics.csv`: Số liệu thống kê mô tả.
- `notebooks/01_data_preparation.ipynb`: Notebook thực hiện quá trình chuẩn bị và phân tích dữ liệu.

## 13. Hướng phát triển

Trong các giai đoạn tiếp theo, đề tài có thể được phát triển theo các hướng:

- Tiếp tục tối ưu hóa các mô hình dự đoán khả năng mua hàng của phiên truy cập.
- Thử nghiệm thêm các thuật toán phân loại khác để so sánh hiệu quả.
- Cải thiện phương pháp lựa chọn ngưỡng quyết định phù hợp với mục tiêu dự đoán.
- Phát triển phần giải thích kết quả dự đoán bằng SHAP trực quan hơn.
- Xây dựng giao diện demo cho phép nhập thông tin của một phiên truy cập và nhận kết quả dự đoán.
- Bổ sung các biểu đồ trực quan để hỗ trợ phân tích hành vi của các phiên truy cập.
