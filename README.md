# MÁY CHO ĂN THÔNG MINH CHO THÚ CƯNG

> Đề tài cuối kỳ môn học: Phát triển ứng dụng IoT  
> Giảng viên hướng dẫn: TS. Nguyễn Anh Tuấn  
> Sinh viên thực hiện: Vũ Thanh Tâm - 23001626
## Đặt vấn đề

Trong xã hội hiện đại, nhịp sống bận rộn với công việc, học tập và những chuyến công tác hay lịch trình dài ngày khiến cho nhiều người nuôi thú cưng (chó, mèo) gặp phải nhiều khó khăn trong việc duy trì một chế độ chăm sóc ổn định và khoa học. 

* **Thực trạng và khó khăn của người nuôi thú cưng:**
  * Việc cho ăn thủ công thường xuyên bị sai lệch về thời gian và định lượng. Ăn quá nhiều dẫn đến nguy cơ béo phì, tiểu đường; ăn quá ít khiến thú cưng còi cọc, suy dinh dưỡng.
  * Khi vắng nhà cả ngày, chủ nhân hoàn toàn không có phương thức để kiểm tra xem vật nuôi đã thực sự ăn hay chưa.
  * Hộp chứa thức ăn có thể cạn kiệt bất ngờ mà không có cảnh báo, khiến thú cưng phải chịu đói suốt nhiều giờ liền.

* **Hạn chế của các giải pháp trên thị trường:**
  * Các dòng máy tự động giá rẻ thường chỉ dùng cơ chế hẹn giờ cơ học đơn giản, dễ bị kẹt hạt và hoàn toàn thiếu các tính năng giám sát từ xa.
  * Các dòng máy thông minh cao cấp tích hợp camera có giá thành quá đắt đỏ và phụ thuộc hoàn toàn vào hệ thống đám mây của nhà sản xuất.

* **Cảm hứng và động lực thực tế:**
  * Bắt nguồn từ chính trải nghiệm cá nhân — việc nuôi mèo và thấu hiểu sự lo lắng mỗi khi phải để thú cưng ở nhà một mình cả ngày.
  * Định hướng thiết kế và chế tạo một hệ thống máy cho ăn thông minh phân khúc giá rẻ nhưng mang lại hiệu quả cao.

* **Mục tiêu và giải pháp tổng thể của đề tài:**
  * Tự động phân phát thức ăn chính xác theo thời gian và yêu cầu lập trình.
  * Tích hợp cảm biến đo lường khối lượng để theo dõi lượng thức ăn trong bát và hộp chứa, kết hợp cảm biến phát hiện sự hiện diện của thú cưng.
  * Kết hợp giao thức MQTT và giao diện Dashboard trực quan trên Node-RED, cho phép người dùng giám sát toàn diện và điều khiển từ xa một cách thuận tiện từ bất cứ đâu.
## Mục tiêu và nội dung chính

### Mục tiêu
Mục tiêu của đề tài là xây dựng một hệ thống IoT hoàn chỉnh trên phần cứng thực tế, trong đó ESP32 vừa đóng vai trò là bộ điều khiển trung tâm tại chỗ, vừa là một thiết bị kết nối mạng linh hoạt. Hệ thống đáp ứng ba mục tiêu cốt lõi:
1. **Cấp thức ăn tự động và chính xác:** Đảm bảo đúng định lượng và đúng thời điểm.
2. **Giám sát đa thông số:** Theo dõi lượng thức ăn còn lại trong bát, mức dự trữ trong hộp chứa và sự hiện diện của thú cưng.
3. **Giám sát & Điều khiển từ xa:** Cho phép chủ nhà tương tác toàn diện thông qua giao thức MQTT và giao diện trực quan Node-RED Dashboard.

---

### Nội dung thực hiện

* **Cấp thức ăn tự động và thủ công:**
  * Thức ăn được dự trữ trong hộp chứa đặt phía trên. Khi có lệnh cho ăn, ESP32 điều khiển động cơ Servo SG90 xoay cơ cấu mở cửa trong khoảng thời gian xác định để thức ăn rơi xuống bát, sau đó đóng lại.
  * Hỗ trợ hai phương thức kích hoạt: nhấn nút "Cho ăn ngay" trên Dashboard từ xa hoặc bấm nút nhấn vật lý trực tiếp trên máy.
  * Cho phép tùy chỉnh khẩu phần mỗi lần cho ăn linh hoạt ngay trên giao diện Dashboard.

* **Đo lường lượng thức ăn trong bát:**
  * Bát ăn đặt trên cảm biến trọng lượng Loadcell 1kg, tín hiệu vi sai truyền qua module giải mã HX711 về ESP32 để tính toán khối lượng thực tế (đơn vị: gram).
  * Ứng dụng số liệu: Ngăn chặn việc tiếp tục đổ thêm thức ăn khi bát vẫn còn đầy, đồng thời theo dõi lượng thức ăn giảm dần theo thời gian để nhận biết thú cưng đã ăn bao nhiêu.
  * Cần tiến hành hiệu chuẩn (calibration) cảm biến trước khi đưa vào vận hành.

* **Đo mức dự trữ thức ăn trong hộp:**
  * Cảm biến siêu âm HC-SR04 lắp tại nắp hộp chứa, đo khoảng cách từ nắp xuống bề mặt thức ăn.
  * Khoảng cách đo được tỉ lệ nghịch với lượng thức ăn còn lại. Khi mức thức ăn giảm xuống dưới ngưỡng cài đặt, hệ thống tự động phát cảnh báo lên Dashboard và kích hoạt còi Buzzer/LED tại chỗ để nhắc nhở châm thêm.

* **Phát hiện sự hiện diện của thú cưng:**
  * Sử dụng cảm biến chuyển động PIR HC-SR501 để phát hiện khi thú cưng tiến lại gần khu vực máy cho ăn.
  * Dữ liệu hỗ trợ nhận biết thú cưng có đến ăn hay không và cập nhật trạng thái "thú cưng đang ở gần" lên giao diện quản lý.

* **Hiển thị và cảnh báo tại chỗ:**
  * **Màn hình LCD I2C:** Hiển thị thời gian thực các thông số như khối lượng thức ăn trong bát, dung lượng còn lại trong hộp và trạng thái hoạt động (Sẵn sàng, Đang cho ăn, Cảnh báo cạn thức ăn).
  * **Buzzer & LED:** Phát âm thanh tín hiệu khi bắt đầu chu trình cho ăn hoặc báo động khi có sự cố/cạn thức ăn.

* **Giao tiếp dữ liệu qua MQTT:**
  * ESP32 kết nối Wi-Fi và giao tiếp với MQTT Broker online theo mô hình Publish/Subscribe.
  * **Publish:** ESP32 gửi định kỳ các thông số (khối lượng bát, mức thức ăn hộp, trạng thái PIR, trạng thái máy) lên các topic tương ứng.
  * **Subscribe:** ESP32 đăng ký các topic nhận lệnh từ Dashboard (cho ăn tức thời, thay đổi khẩu phần, bật/tắt còi báo).
  * Giúp phân tách độc lập giữa thiết bị và giao diện điều khiển, cho phép truy cập từ bất kỳ đâu có kết nối Internet.

* **Xây dựng Dashboard trên Node-RED:**
  * Giao diện thiết kế bằng Node-RED Dashboard, tương thích hoàn toàn trên cả máy tính và trình duyệt điện thoại.
  * Tích hợp đầy đủ các thành phần: Đồng hồ đo khối lượng/mức thức ăn, chỉ chỉ báo trạng thái, nút nhấn cho ăn tức thời, ô nhập khẩu phần, biểu đồ lịch sử khối lượng theo thời gian và hộp thoại thông báo cảnh báo.

* **Môi trường phát triển và phần mềm:**
  * Mã nguồn vi điều khiển ESP32 được lập trình và quản lý trên môi trường **PlatformIO / Arduino IDE**.
  * Quy trình phát triển: Sử dụng nền tảng mô phỏng **Wokwi** để kiểm tra và tối ưu hóa logic thuật toán trước khi lắp ráp phần cứng, sau đó nạp code thực tế để thử nghiệm mạch vật lý.

---

### Luồng vận hành hệ thống

1. **Khởi tạo:** Cấp nguồn cho thiết bị, ESP32 khởi động, tiến hành kết nối Wi-Fi và thiết lập liên lạc với MQTT Broker.
2. **Giám sát liên tục:** ESP32 đọc dữ liệu chu kỳ từ Loadcell (HX711), cảm biến siêu âm (HC-SR04), cảm biến chuyển động (PIR) và kiểm tra trạng thái nút nhấn.
3. **Cập nhật dữ liệu:** Dữ liệu được hiển thị trực tiếp lên màn hình LCD I2C tại chỗ, đồng thời Publish lên MQTT Broker để cập nhật theo thời gian thực (Real-time) trên Node-RED Dashboard.
4. **Xử lý lệnh cho ăn:** Khi nhận tín hiệu kích hoạt (từ nút bấm vật lý hoặc lệnh trên Dashboard), ESP32 kiểm tra điều kiện an toàn của bát (tránh tràn), điều khiển Servo SG90 quay mở cửa xả, phát tín hiệu còi Buzzer và nháy LED báo hiệu.
5. **Cập nhật & Cảnh báo:** Hoàn tất chu trình cho ăn, hệ thống tính toán lại khối lượng trong bát và kiểm tra lượng dự trữ trong hộp; nếu phát hiện cạn thức ăn dưới ngưỡng quy định, hệ thống lập tức gửi cảnh báo về điện thoại/máy tính và bật tín hiệu cảnh báo tại chỗ.
## Sơ đồ khối dự kiến

<img width="1547" height="1033" alt="image" src="https://github.com/user-attachments/assets/c0804631-5fb4-40fd-81fc-3f8d45fbe97b" />


## Sơ đồ mạch dự kiến

<p align="center">
  <img width="480" alt="image" src="https://github.com/user-attachments/assets/b8189d93-af02-4533-944e-e4a021b0a5f0" /><br>
  <img width="480" alt="image" src="https://github.com/user-attachments/assets/8fe742b4-90b9-4e50-9ec2-9365ddb28d62" /><br>
  <img width="480" alt="image" src="https://github.com/user-attachments/assets/2622a6fa-9d42-44e2-a040-cda18b0eeeae" /><br>
  <img width="480" alt="image" src="https://github.com/user-attachments/assets/6bb1ad49-9464-478e-97be-e9e74181f43b" /><br>
  <img width="480" alt="image" src="https://github.com/user-attachments/assets/87f5fb4c-97f8-4933-9f3e-3d3d326a66b4" />
</p>





## Danh mục linh kiện phần cứng

| STT | Tên linh kiện | Hình ảnh thực tế |
| :---: | :--- | :---: |
| **1** | **ESP32 DevKit** | <img width="120" alt="image" src="https://github.com/user-attachments/assets/3d41a465-229d-4b1f-a2c9-38631093aaf4" /> |
| **2** | **Mạch giảm áp Buck** | <img width="100" alt="image" src="https://github.com/user-attachments/assets/47093302-760d-4f8f-bac1-15169fb40562" /> |
| **3** | **Cảm biến siêu âm HC-SR04** | <img width="100" alt="image" src="https://github.com/user-attachments/assets/6d18c600-7f42-4e59-bc5b-86571dca4631" /> |
| **4** | **Module HX711** | <img width="100" alt="image" src="https://github.com/user-attachments/assets/988a3cfc-00e5-42b3-a52e-524f653974b8" /> |
| **5** | **Loadcell 1kg** | <img width="120" alt="image" src="https://github.com/user-attachments/assets/222f216c-66ad-4121-8cd9-d558fd38a474" /> |
| **6** | **Cảm biến chuyển động PIR HC-SR501** | <img width="100" alt="image" src="https://github.com/user-attachments/assets/e2591822-4f1f-412b-88da-024c2f311620" /> |
| **7** | **Động cơ Servo SG90** | <img width="100" alt="image" src="https://github.com/user-attachments/assets/6586d334-b5c8-4d44-88bf-217b7b600114" /> |
| **8** | **Màn hình LCD 1602 (I2C)** | <img width="100" alt="image" src="https://github.com/user-attachments/assets/74a7357c-eced-4e86-b988-736844887be6" /> |
| **9** | **Còi Buzzer 5V** | <img width="80" alt="image" src="https://github.com/user-attachments/assets/3f54940f-8488-45d7-af0d-4d472233ed49" /> |
| **10** | **Đèn LED báo hiệu** | <img width="60" alt="image" src="https://github.com/user-attachments/assets/6519795e-31e8-44f3-b68e-14f9674c8e08" /> |
| **11** | **Nút nhấn (Push Button)** | <img width="80" alt="image" src="https://github.com/user-attachments/assets/ce5f977e-5aac-4d4a-852a-8e6d98bb66f1" />|


## Chức năng chi tiết từng linh kiện phần cứng

Trong hệ thống máy cho ăn thông minh, mỗi linh kiện đảm nhận một nhiệm vụ chuyên biệt, phối hợp nhịp nhàng với nhau để tạo thành một chu trình khép kín từ đo lường, xử lý đến chấp hành và giám sát:

* **1. ESP32 DevKit (Vi điều khiển trung tâm)**
  * **Chức năng:** Là "bộ não" của toàn bộ hệ thống. ESP32 thực hiện thu thập dữ liệu từ các cảm biến (Loadcell, siêu âm, PIR), xử lý logic điều khiển các ngoại vi (Servo, LCD, Buzzer, LED) và duy trì kết nối Wi-Fi để truyền/nhận dữ liệu thời gian thực với MQTT Broker và Node-RED Dashboard.

* **2. Mạch giảm áp Buck (DC-DC)**
  * **Chức năng:** Chuyển đổi và ổn định điện áp từ nguồn pin sạc (18650) xuống mức điện áp chuẩn $+5\text{V}$, cung cấp nguồn điện an toàn, ổn định cho động cơ Servo, cảm biến siêu âm, màn hình LCD và các module phụ trợ hoạt động mà không bị sụt áp.

* **3. Cảm biến siêu âm HC-SR04**
  * **Chức năng:** Đo lường khoảng cách từ nắp hộp xuống bề mặt thức ăn bên trong thùng chứa. Dữ liệu này giúp hệ thống quy đổi ra lượng thức ăn còn lại và tự động phát cảnh báo khi dung tích hộp sắp cạn kiệt.

* **4. Module HX711 & Cảm biến Loadcell 1kg**
  * **Cảm biến Loadcell:** Đặt dưới khay bát ăn, chịu lực tác động và chuyển đổi trọng lượng thức ăn thành tín hiệu điện analog vi sai.
  * **Module HX711:** Khuếch đại và chuyển đổi tín hiệu tương tự sang số (ADC) 24-bit với độ chính xác cao, truyền dữ liệu khối lượng thức ăn (gram) về ESP32 để kiểm soát khẩu phần chính xác và theo dõi thói quen ăn của thú cưng.

* **5. Cảm biến chuyển động PIR HC-SR501**
  * **Chức năng:** Phát hiện sự hiện diện và chuyển động của thú cưng khi chúng tiến lại gần khu vực khay ăn, từ đó ghi nhận thời điểm vật nuôi đến ăn và cập nhật trạng thái lên hệ thống giám sát từ xa.

* **6. Động cơ Servo SG90**
  * **Chức năng:** Đóng vai trò là cơ cấu chấp hành chính. Nhận tín hiệu xung PWM từ ESP32 để xoay trục mở/đóng cửa xả thức ăn từ thùng chứa xuống bát với định lượng thời gian chính xác.

* **7. Màn hình LCD 1602 (giao tiếp I2C)**
  * **Chức năng:** Hiển thị trực quan các thông số vận hành tại chỗ (khối lượng thức ăn trong bát, lượng thức ăn trong hộp, trạng thái hoạt động của máy) giúp người dùng dễ dàng theo dõi trực tiếp khi đứng cạnh thiết bị.

* **8. Còi Buzzer 5V**
  * **Chức năng:** Phát ra tín hiệu âm thanh cảnh báo tại chỗ trong các trường hợp quan trọng: báo hiệu bắt đầu chu trình cho ăn hoặc phát tiếng kêu nhắc nhở khi hộp chứa thức ăn bị cạn.

* **9. Đèn LED báo hiệu**
  * **Chức năng:** Cung cấp tín hiệu trực quan bằng ánh sáng để thông báo trạng thái hoạt động của hệ thống (ví dụ: trạng thái kết nối Wi-Fi, trạng thái đang thực hiện cấp thức ăn hoặc báo lỗi).

* **10. Nút nhấn (Push Button)**
  * **Chức năng:** Cho phép người dùng chủ động thao tác thủ công ngay trên thiết bị (bấm để kích hoạt nhanh lệnh cho ăn ngay lập tức) mà không cần phụ thuộc vào điện thoại hay giao diện máy tính.
## Tài liệu tham khảo

### Datasheet linh kiện
1. Espressif Systems, *ESP32 Series Datasheet*. [https://www.espressif.com/documentation/esp32_datasheet_en.pdf](https://www.espressif.com/documentation/esp32_datasheet_en.pdf)
2. Avia Semiconductor, *HX711: 24-Bit Analog-to-Digital Converter (ADC) for Weigh Scales*. [https://datasheet.eeworld.com.cn/view/18792612.html](https://datasheet.eeworld.com.cn/view/18792612.html)
3. ElecFreaks, *Ultrasonic Ranging Module HC-SR04*. [https://cdn.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf](https://cdn.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf)

