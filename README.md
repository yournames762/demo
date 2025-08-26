# Báo cáo đánh giá mô hình Few-Shot Object Detection

## 1. Giới thiệu  

Bài toán phát hiện đối tượng với dữ liệu viễn thám có nhiều thách thức do số lượng lớp lớn, dữ liệu huấn luyện ít, đối tượng nhỏ và xuất hiện trong nhiều bối cảnh khác nhau. Trong thí nghiệm này, mô hình Faster R-CNN được lựa chọn để thử nghiệm theo hướng few-shot, với số lượng ảnh huấn luyện rất hạn chế.  

## 2. Mô hình và dữ liệu  

- Mô hình: Faster R-CNN với backbone ResNet-50 FPN.  
- Tập dữ liệu: NWPU VHR-10.  
- Cấu hình huấn luyện:  
  - Số ảnh base classes: 50 ảnh mỗi lớp.  
  - Số ảnh novel classes: 5 ảnh mỗi lớp.  
  - Epoch huấn luyện base: 5.  
  - Epoch fine-tune novel: 5.  

## 3. Pipeline huấn luyện  

1. Tiền xử lý dữ liệu: Chia dữ liệu thành base và novel classes.  
2. Huấn luyện ban đầu trên base classes với 50 ảnh mỗi lớp.  
3. Fine-tune mô hình trên novel classes với 5 ảnh mỗi lớp.  
4. Đánh giá mô hình trên tập test.  

## 4. Khó khăn gặp phải  

- Dữ liệu huấn luyện ít dẫn đến khó tổng quát hóa.  
- Một số lớp có sự tương đồng hình dạng và bối cảnh, dễ gây nhầm lẫn.  
- Số epoch huấn luyện quá ít, mô hình chưa kịp hội tụ.  
- Chưa áp dụng augmentation nâng cao.  
- Chưa có đánh giá định lượng bằng mAP, chỉ dựa trên quan sát trực quan.  

## 5. Kết quả thực nghiệm  

- Mô hình chạy được pipeline đầy đủ từ train đến inference.  
- Tuy nhiên, kết quả dự đoán chưa tốt, nhiều trường hợp bounding box lệch, phát hiện sai hoặc bỏ sót đối tượng.  
- Một số lớp mới gần như không được phát hiện chính xác.  

## 6. Đánh giá chất lượng mô hình và hạn chế

- Mô hình dự đoán thiếu chính xác, xuất hiện nhiều false positive và false negative, đặc biệt là ở các lớp mới.  
- Các bounding box có độ chính xác thấp, IoU nhỏ, do dữ liệu hạn chế và số epoch quá ít khiến mô hình chưa hội tụ.  
- Mô hình có thể bị overfit trên một vài ảnh huấn luyện, dẫn đến kết quả tốt trên tập train nhưng kém trên tập validation, hoặc ngược lại là underfit do thời gian huấn luyện quá ngắn.  

Nhìn chung, đây mới chỉ là một bản demo thử nghiệm, nên kết quả thấp là dễ hiểu. Để cải thiện cần nhiều dữ liệu hơn, thời gian huấn luyện dài hơn, cũng như áp dụng các kỹ thuật augmentation và điều chỉnh siêu tham số.  

## 7. Kết luận  

Mặc dù kết quả hiện tại chưa tốt, nhưng pipeline đã được xây dựng hoàn chỉnh và chứng minh tính khả thi của few-shot object detection trên dữ liệu viễn thám. Các hạn chế chủ yếu đến từ việc thiếu dữ liệu và thời gian huấn luyện ngắn. Trong tương lai, nếu có thêm dữ liệu và tinh chỉnh hợp lý, mô hình hứa hẹn sẽ đạt được kết quả khả quan hơn.  
