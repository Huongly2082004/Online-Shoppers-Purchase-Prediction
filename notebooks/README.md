# Online Shoppers Purchase Prediction

## 1. Giới thiệu

Đề tài xây dựng mô hình dự đoán khả năng mua hàng của khách hàng dựa trên dữ liệu hành vi truy cập website thương mại điện tử.

Mục tiêu của hệ thống là dự đoán một phiên truy cập có khả năng dẫn đến mua hàng hay không, đồng thời giải thích các đặc trưng có ảnh hưởng đến kết quả dự đoán.

## 2. Dataset

Dataset sử dụng là Online Shoppers Purchasing Intention Dataset.

Các đặc trưng đầu vào bao gồm:

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

Biến mục tiêu:

- Revenue: xác định khách hàng có thực hiện mua hàng hay không.

## 3. Tiền xử lý dữ liệu

Quy trình tiền xử lý gồm:

- Kiểm tra và xử lý dữ liệu trùng lặp.
- Kiểm tra kiểu dữ liệu.
- Phân tách biến đầu vào và biến mục tiêu.
- Mã hóa các biến phân loại.
- Chia dữ liệu thành tập Train, Validation và Test.
- Sử dụng seed cố định để đảm bảo khả năng tái lập kết quả.

Sau khi mã hóa, dữ liệu có 28 đặc trưng.

Kích thước dữ liệu:

- Train: 7323 mẫu
- Validation: 2441 mẫu
- Test: 2441 mẫu

## 4. Mô hình

Ba mô hình được sử dụng:

1. Logistic Regression
2. Decision Tree
3. Random Forest

Các mô hình được đánh giá bằng:

- ROC-AUC
- F1-score
- Precision
- Recall
- Confusion Matrix

Do dữ liệu có sự mất cân bằng giữa hai lớp, F1-score và chiến lược lựa chọn ngưỡng quyết định được sử dụng để đánh giá và cải thiện khả năng nhận diện khách hàng có khả năng mua hàng.

## 5. Kết quả

Kết quả đánh giá trên tập Test:

| Model | Threshold | ROC-AUC | F1 | Precision | Recall |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.5608 | 0.9171 | 0.6619 | 0.6034 | 0.7330 |
| Decision Tree | 1.0000 | 0.7400 | 0.5624 | 0.5646 | 0.5602 |
| Random Forest | 0.4100 | 0.9259 | 0.6640 | 0.6739 | 0.6545 |

Random Forest cho kết quả tốt nhất trong ba mô hình với ROC-AUC = 0.9259 và F1-score = 0.6640.

## 6. Giải thích mô hình

SHAP được sử dụng để giải thích mức độ đóng góp của các đặc trưng đến kết quả dự đoán.

Ba đặc trưng quan trọng nổi bật gồm:

- PageValues
- ExitRates
- BounceRates

Trong đó PageValues có mức độ ảnh hưởng lớn nhất đến dự đoán.

## 7. Demo dự đoán

Hệ thống có khả năng nhận thông tin của một phiên truy cập và đưa ra:

- Xác suất khách hàng mua hàng.
- Kết quả dự đoán.
- Ngưỡng quyết định được sử dụng.
- Các đặc trưng đóng góp chính vào kết quả dự đoán.

Ví dụ:

- Xác suất mua hàng: 41.00%
- Ngưỡng quyết định: 0.41
- Kết quả: Có khả năng mua hàng.

## 8. Cấu trúc dự án

```text
Online-Shoppers-Purchase-Prediction/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│
├── src/
│
├── results/
│
├── requirements.txt
└── README.md
