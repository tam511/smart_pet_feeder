# MÁY CHO THÚ CƯNG ĂN TỰ ĐỘNG
## Đặt bài toán
Nhiều người nuôi chó, mèo phải đi làm, đi học hoặc đi công tác xa nhà cả ngày. Việc cho thú cưng ăn thường gặp các vấn đề sau:

- Ăn không đúng giờ, không đúng lượng. Cho ăn quá nhiều dễ gây béo phì, quá ít thì thú cưng bị đói.
- Không biết thú cưng đã ăn hay chưa. Chủ nhà đi vắng không có cách nào kiểm tra.
- Không biết khi nào hết thức ăn. Hộp thức ăn cạn mà không ai hay.
- Máy cho ăn tự động trên thị trường thường có giá cao, hoặc chỉ hẹn giờ cơ bản và không có giám sát từ xa.
- Cảm hứng cá nhân: bản thân em có nuôi mèo và em cảm thấy cần có thiết bị cho ăn tự động để cho meo ăn đúng giờ, có thể để mèo ở nhà cả ngày mà không lo lắng về việc cho mèo ăn.
- Từ nhu cầu thực tế đó, đề tài xây dựng một máy cho ăn thông minh giá rẻ. Máy tự cấp thức ăn theo yêu cầu, đo được lượng thức ăn trong bát và trong hộp, phát hiện thú cưng đến gần, đồng thời cho phép chủ nhà theo dõi và điều khiển từ xa qua MQTT và dashboard Node-RED trên máy tính hoặc điện thoại.
## Mục tiêu và nội dung chính
- Cấp thức ăn bằng servo SG90 theo lệnh từ dashboard hoặc từ nút nhấn tại chỗ.
- Đo khối lượng thức ăn trong bát bằng loadcell + HX711 để biết thú cưng đã ăn bao nhiêu và tránh đổ thêm khi bát còn đầy.
- Đo mức thức ăn còn trong hộp bằng cảm biến siêu âm HC-SR04 để cảnh báo khi sắp hết.
- Phát hiện thú cưng đến gần bằng cảm biến PIR HC-SR501.
- Hiển thị trạng thái tại chỗ bằng LCD I2C, cảnh báo bằng buzzer và LED.
- Có thể cho ăn từ xa, có nút nhấn vật lý để đổ hạt tuỳ nhu cầu.
- Giao tiếp MQTT qua broker online. Dashboard Node-RED hiển thị số liệu và gửi lệnh điều khiển.
- Mã nguồn viết trên nền tảng PlatformIO / Arduino.
## Sơ đồ khối dự kiến

<img width="1547" height="1033" alt="image" src="https://github.com/user-attachments/assets/c0804631-5fb4-40fd-81fc-3f8d45fbe97b" />


## Sơ đồ mạch dự kiến

<img width="543" height="253" alt="image" src="https://github.com/user-attachments/assets/b8189d93-af02-4533-944e-e4a021b0a5f0" />
<img width="752" height="453" alt="image" src="https://github.com/user-attachments/assets/8fe742b4-90b9-4e50-9ec2-9365ddb28d62" />
<img width="670" height="335" alt="image" src="https://github.com/user-attachments/assets/2622a6fa-9d42-44e2-a040-cda18b0eeeae" />
<img width="601" height="460" alt="image" src="https://github.com/user-attachments/assets/6bb1ad49-9464-478e-97be-e9e74181f43b" />
<img width="624" height="639" alt="image" src="https://github.com/user-attachments/assets/87f5fb4c-97f8-4933-9f3e-3d3d326a66b4" />

## Linh kiện dự kiến
- Esp32: vi điều khiển trung tâm
 - <img width="2468" height="1484" alt="image" src="https://github.com/user-attachments/assets/3d41a465-229d-4b1f-a2c9-38631093aaf4" />
- Loadcell: Cảm biến lực, đặt dưới bát để đo trọng lượng thức ăn
 - <img width="550" height="308" alt="image" src="https://github.com/user-attachments/assets/222f216c-66ad-4121-8cd9-d558fd38a474" />
- HX711: Mạch khuếch đại và chuyển đổi ADC 24-bit cho loadcell, gửi dữ liệu về ESP32
  - <img width="340" height="333" alt="image" src="https://github.com/user-attachments/assets/988a3cfc-00e5-42b3-a52e-524f653974b8" />
- HC-SR04: Cảm biến siêu âm, đo khoảng cách từ nắp đến mặt thức ăn để biết hộp còn nhiều hay ít
 - <img width="573" height="542" alt="image" src="https://github.com/user-attachments/assets/6d18c600-7f42-4e59-bc5b-86571dca4631" />
- PIR HC-SR501: Cảm biến chuyển động hồng ngoại, phát hiện thú cưng đến gần
 - <img width="511" height="538" alt="image" src="https://github.com/user-attachments/assets/e2591822-4f1f-412b-88da-024c2f311620" />
- Servo SG90: Xoay cơ cấu mở cửa để cấp thức ăn xuống bát
  - <img width="524" height="481" alt="image" src="https://github.com/user-attachments/assets/6586d334-b5c8-4d44-88bf-217b7b600114" />
- LCD I2C: Hiển thị trạng thái và thông số tại chỗ (giao tiếp 2 dây SDA/SCL)
 - <img width="441" height="435" alt="image" src="https://github.com/user-attachments/assets/74a7357c-eced-4e86-b988-736844887be6" />
- Buzzer: cảnh báo khi cho ăn, khi hết thức ăn hoặc khi có vấn đề
  - <img width="233" height="232" alt="image" src="https://github.com/user-attachments/assets/3f54940f-8488-45d7-af0d-4d472233ed49" />
- LED: báo trạng thái hoạt động
  - <img width="132" height="236" alt="image" src="https://github.com/user-attachments/assets/6519795e-31e8-44f3-b68e-14f9674c8e08" />
- Module buck 5V/3A: Hạ điện áp nguồn vào xuống 5V ổn định để cấp cho cả mạch
  - <img width="486" height="406" alt="image" src="https://github.com/user-attachments/assets/47093302-760d-4f8f-bac1-15169fb40562" />
- Nút nhấn: cho ăn tuỳ nhu cầu
  - <img width="229" height="242" alt="image" src="https://github.com/user-attachments/assets/ce5f977e-5aac-4d4a-852a-8e6d98bb66f1" />
- Công tắc: bật tắt nguồn của toàn mạch
  - <img width="151" height="141" alt="image" src="https://github.com/user-attachments/assets/f8387398-9497-4b17-b5a3-6eb68669f360" />










