# Reflection — Day 18 Lakehouse Lab

**Câu hỏi:** Anti-pattern nào trong slide §5 mà team bạn dễ vướng nhất? Vì sao?

**Trả lời:**

Với tư cách là người mới học về Data Lakehouse, mình nhận thấy team mình dễ vướng phải nhất là **Small-File Problem** (vấn đề quá nhiều file nhỏ). 

**Lý do:** Khi mới bắt đầu xây dựng các đường ống dẫn dữ liệu (data pipeline), chúng mình thường tập trung vào việc đẩy dữ liệu vào Bronze layer càng nhanh càng tốt, đặc biệt là với các luồng dữ liệu nhỏ liên tục (streaming-like ingestion). Nếu không nắm vững kiến thức về lưu trữ, chúng mình sẽ vô tình tạo ra hàng nghìn file Parquet tí hon. 

Qua bài Lab 18, mình hiểu rằng điều này sẽ làm "tổn thọ" hiệu suất truy vấn do máy tính phải tốn quá nhiều thời gian để mở và đọc từng file nhỏ. Việc áp dụng Delta Lake với các lệnh như `OPTIMIZE` để gộp file và `Z-ORDER` để sắp xếp dữ liệu theo các cột thường dùng (như `user_id`) là một "cứu cánh" thực sự, giúp tăng tốc truy vấn lên nhiều lần (như con số 7.0x thực tế trong NB2) và giữ cho Lakehouse luôn gọn gàng, khỏe mạnh.
