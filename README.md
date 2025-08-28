TỔNG QUAN: Hệ thống nhận diện hành động và đếm số lượng hành động thực hiện (push-up, squat). Bao gồm các hàm: truyền và nhận thông tin, xử lý các thông tin vừa truyền hoặc nhận được (preprocess, process, postprocesing): những hàm xử lý này sẽ được dev trên Javascript hoặc Python. Tôi ưu tiên xử lý các hàm này bằng python (cho mọi người dễ đọc và chỉnh sửa code)

Front-end: 
    -Javascript: thực hiện truyền và nhận thông tin từ Back-end. 
        . Chức năng: 
            . Mở camera và truyền thông tin: hiện tại là những frames từ camera về cho Back-end.
            . Nhận thông tin đã xử lý và hiển thị trực quan cho người dùng 
            
        ## Hiện tại những thông tin nhận vào đều là giả (sẽ merge code vào sau khi các nhanh khác đã ổn định) 

Back-end:
    - Server: Connect với Front-end để nhận và truyền thông tin.
    - Chức năng: 
        . Nếu nhận được frames từ Front-end. Trích xuất thông tin (hàm trích xuất thông tin từ mediapipe)
        . Sau khi nhận được các landmarks đi qua nhận diện hành động (hàm action classification***)
        . Khi sau nhận diện được hành động, đưa dữ liệu   landmarks đến các hàm đếm tương ứng với hành động đó (Những hàm đếm số lượng).
        . Sau khi đếm, lưu về file json hoặc định dạng phù hợp và gửi dữ liệu đến Front-end (hàm gửi thông tin)
        
AI: action classification ***
    - Chuẩn bị dữ liệu (22 landmarks và 12 góc được tạo từ 22 landmarks đó). Trích xuất các điểm x,y,z và lưu vào file windows.h5 (shape là (30,78))
    - Đưa qua những hàm Features Engineering để chuẩn hóa (đang trong quá trình kiểm thử).
    - Huấn luyện với 2 model được tôi định nghĩa trong model.py (LSTM, BiLSTM).
        -> Kỳ vọng: 
            .f1_score > 0.95 ở tập test được chia từ file windows.h5
            .f1_score > 0.90 ở tập real_easy(video tự quay)
            .f1_score > 0.85 ở tập real_hard(video tự quay nhưng với góc độ khó hơn)
    - Inference: nhận landmarks và trả về kết quả nhận diện. Yêu cầu: > 25fps
    
Vai trò:
    - Dương: Leader, AI, IT Helpdesk
    - Vinh: Tổng hợp dữ liệu cho AI, Logic đếm, Based_code Javascript
    - Tuấn Anh: Tổ chức file code một cách khoa hợc, build base code cho dự án. Tiến hành merge thì cập nhật những hàm mới.

Sau khi test hệ thống chạy mượt: Tiến hành tạo GUI: GUI training tích hợp đóng mở hệ thống

Những điều cần bổ sung: ......
        
