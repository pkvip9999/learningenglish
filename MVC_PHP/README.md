

[Source](https://medium.com/@noufel.gouirhate/create-your-own-mvc-framework-in-php-af7bd1f0ca19 "Permalink to Create your own MVC framework in PHP – Noufel Gouirhate – Medium")

# Tạo MVC framework PHP của riêng bạn  – Noufel Gouirhate – Medium

### Giải thích về MVC

Để tránh những loại tình huống, Các lập trình viên bắt đầu nghĩ cách tổ chức code mới cho website của họ. Một cách để làm điều đó là  _mẫu thiết kế MVC_. Mục tiêu là chia dự án thành 3 phần lớn:

* **Model**: Tương tác với cơ sở dữ liệu. Nó nhận, lưu trữ và truy suất dữ liệu cho người dùng
* **View**: Hiểu thị thông tin cho người dùng và tích hợp dữ liệu từ controller.
* **Controller**: Gửi và nhận dữ liệu từ model và chuyển qua view.

![][1]

### Cấu trúc

Để thiết lập mẫu thiết ké này, Chúng ta sẽ cấu trúc dự án của chúng ta. Chúng ta có thể tìm thấy rất nhiều cách thông qua internet. Nhưng đây là đề nghị của tôi:

![][2]

Như bạn nhận thấy, tôi đưa ra xương sống của MVC framework với ba thư mục (Models, Views, Controllers) và một só thứ khác :

* Thư mục Webroot là thư mục duy nhất người dùng có thể truy cập.
* Router.php, dispatcher.php, request.php, .htaccess là một phần của hệ thống routing.
* Config : tất cả các cài đặt cần thiết cho website của chúng tôi. Chúng tôi sẽ lấy tệp db.php làm điểm truy cập duy nhất tới cơ sở dữ liệu của chúng tôi (singleton class).

### Kiến trúc tổng thể

![][3]

Khi truy cập trang web của chúng tôi, người dùng sẽ tự động được chuyển hướng đến Webroot/index.php nhờ vào file two.htaccess.

Cái đầu tiên sẽ chuyển hướng người dùng đến thư mục Webroot.

![][4]

Cái thứ 2 sẽ chuyển hướng họ tới index.php. Lưu ý rằng chúng tôi lưu trữ tạm tham số (p=$1).

![][5]

index.php yêu cầu tất cả các file chúng tôi sẽ cần đề tạo bộ điều phối .Sau khi tạo một thể hiện của lớp Dispatch, chúng tôi đã sẵn sàng để thiết lập logic định tuyến của chúng tôi.

![][6]

### Hệ thống định tuyến

#### _request.php_

Mục tiêu của file này là lấy url theo yêu cầu của người dùng.

![][7]

#### router.php

Bộ định tuyến lấy được url dược băt bởi _request.php_ and tách url thành 3 phần khác nhau bằng kí tự "/".

![][8]

Những đầu vào này sẽ được sử lý thông qua dispatcher. dispatcher đang làm công việc giống như người điều phối không lưu. Khi có một yêu cầu mới được tải, nó chon controller và hành động với các tham số. Vì vậy chỉ với duy nhất một phương thức dispatch()), bạn có thể chạy tất cả các logic định tuyến này.

![][9]

### Cơ sỏ dữ liệu

model sẽ sử lý yêu cầu đến cơ sở dữ liệu. Vì vậy chúng tôi sẽ phải gọi cơ sở dữ liệu cảu chúng tôi rất nhiều lần. Một cách đơ giản, tại mỗi liên kết, chúng ta có thể tạo một thể hiện của cơ sở dữ liệu. Giải pháp này không thực sự hiệu quả . Tôi khuyên chúng ta nên tạo một singleton để xử lý liên kết đến cơ sở dữ liệu của chúng ta  :

![][10]

### MVC

Bây giờ chúng tôi đã thiết lập bộ điều phối, trang web của chúng tôi có thể tải một hành động từ controller

Ở dây chúng tôi tạo một todo app, vi vậy chúng tôi tạo _tasksController.php_. Controller sẽ yêu cầu dữ liệu từ model model Task.php và chuyển dữ liệu tới view. Để làm quá trình này dễ dàng hơn, chúng ta sẽ tạo một lớp cha Controller để sử lý chúng.

![][11]

Phương thức _set()_ method sẽ hợp nhất tất cả các dữ liệu chúng ta cần tới view.

Phương thức _render()_ sẽ import dữ liệu với phương thức extract và sau đó tải bố cục được yêu cầu trong thư mục View. Hơn thế nữa, điều này cho phép chúng tôi có một bố cục để tránh sự lặp lại ngu ngốc của HTML trong view của chúng tôi.

Chúng tôi đã sẵn sàng để làm việc trên tasksController.php. Hãy kiểm tra mã của chúng ta, tôi sẽ tạo một hành động chỉ mục:

![][12]

Và xem nhanh với thông báo "Xin chào". 

Và đây là kết quả :

![][13]

 MVC framework của chúng ta được thiết lập! Bây giờ chúng ta chỉ cần thực hiện các hành động CRUD về tài nguyên tác vụ. Nếu bạn muốn biết thêm chi tiết về điều này và nhận trang web với các nhiệm vụ CRUD, bạn có thể kiểm tra repo trên Github của tôi.

Vì vậy, bây giờ, bạn đã phát triển một cấu trúc MVC bền vững hơn nhiều so với trang web php truyền thống của chúng ta. Nhưng vẫn còn rất nhiều việc phải làm (bảo mật, sử lý lỗi…). Các chủ đề này đã được xử lý bởi các framework như Laravel hoặc Symfony .

[1]: https://cdn-images-1.medium.com/max/1600/1*xnuMvzXzmAxYXcRrd1Wj5Q.png
[2]: https://cdn-images-1.medium.com/max/1600/1*IA0nHOylfQYxjnGwi1XGaQ.png
[3]: https://cdn-images-1.medium.com/max/1600/1*gRErOZyn7ptn373U9fv0Yg.png
[4]: https://cdn-images-1.medium.com/max/1600/1*_agMehf9fNamnUtWqnv4kg.png
[5]: https://cdn-images-1.medium.com/max/1600/1*I67GugEBv0ONYruFet_wbA.png
[6]: https://cdn-images-1.medium.com/max/1600/1*tPlzi7umbyf6JJ9WSkfx8w.png
[7]: https://cdn-images-1.medium.com/max/1600/1*3m5NfXYUAoDAllbVdS8N1w.png
[8]: https://cdn-images-1.medium.com/max/1600/1*EVNESudstEyfXwvx6b5f1Q.png
[9]: https://cdn-images-1.medium.com/max/1600/1*I9mpgAX_OpaJa35jiQfUVg.png
[10]: https://cdn-images-1.medium.com/max/1600/1*EBlYRwirAwcywwTg0T1waw.png
[11]: https://cdn-images-1.medium.com/max/1600/1*Dmg_0gOYlq5ONFlKRkfbGw.png
[12]: https://cdn-images-1.medium.com/max/1600/1*n6l3kSUruZfOxpUNmKgTHA.png
[13]: https://cdn-images-1.medium.com/max/1600/1*MSUdTGHL_ozUGdBVeixirQ.png

  
