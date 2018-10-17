

[Source](https://medium.com/exploring-code/why-should-you-learn-go-f607681fad65 )



[Homepage][1]

[Exploring Code][2]

[Sign in][3][Get started][4]

Member preview

![Go to the profile of Keval Patel][5]

[Keval Patel][6]BlockedUnblockFollowFollowing

www.kevalpatel2106.com | Android Developer | Machine learner | Gopher | Open Source Contributor

Jan 8, 2017

* * *

# Tại sao bạn nên học GoLang

![][7]

Image from: 

> "[Go sẽ là ngôn ngữ của máy chủ trong tương lai][8]" — Tobias Lütke, Shopify

Trong vài năm qua, có sự phát triển của ngôn ngữ lập trình mới: [**Go or GoLang**][9]. Không điều gì làm cho một lập trình viên phấn khích hơn là một ngôn ngữ lập trình mới, đúng không? Vì thế, tôi đã bắt đầu học Go 4 5 tháng trước và ở đây tôi sẽ nói cho bạn biết về tại sao bạn nên học ngôn ngữ lập trình mới đó.

Tôi sẽ không dạy bạn, làm sao bạn có thể viết "Hello World" trong bài viết này. Có nhiều bài viết trực tuyến khác về điều đó. **Tôi sẽ giải thích giai đoạn hiện tại của phần cứng và phần mền của mấy tính và tại sao chúng ta nên học một ngôn ngữ nới như Go?** Bởi vì nếu không có vấn đề gì thì chúng ta đã không cần giải pháp, đúng không?

* * *

### Giới hạn phần cứng:

[**Định luật *Moore*][10]** đang sai.**

Đầu tiên bộ vi sử lý Pentium 4 với với tốc độ 3.0GHz đã được [giới thiệu bởi Intel năm 2004][11] by Intel. Ngày nay, [Mackbook Pro 2016][12] của tôi có tốc độ  2.9GHz. Bởi vì, gần một thập kỷ không có quá nhiều thu hoạch đột phá trong sức mạnh xử lý. Chúng ta có thể nhìn thấy so sánh sự tăng sức mạnh xử lý theo từng năm trong biểu đồ dưới đây.

![][13]

Từ biểu đồ bạn có thể thấy rằng hiệu suất đơn luồng và tần số của bộ vi xử lý vẫn không thay đổi trong gần một thập kỷ qua. Nếu bạn nghĩ việc thêm transistor là giải pháp thế thì bạn sai rồi.Đó là bở vì trong phạm vi nhỏ hơn  thì một số vấn đề lượng tử bắt đầu xuất hiện (như tunneling) và bởi vì việc đưa thêm transistor vào sẽ tốn nhiều chi phí hơn([tại sao?][14]) và  số transistors bạn có thể thêm vào mỗi dollar băt đầu giảm.

vì vậy để giải quyết vấn đề trên

* Các nhà sản xuất bắt đầu bổ xung thêm nhiều nhân hơn cho bộ vi xừ lý. Ngày nay chúng ta có CPU 4 nhân và 8  nhân.
* Chúng ta cũng giới thiệu hyper-threading.
* Thêm bộ nhớ cache vào bộ xứ lý để tăng hiệu suất

Nhưng các giải pháp trên cũng có giới hạn của nó. Chúng ta không thể thêm nhiều hơn bộ nhớ cache vào bộ vi xử lý để tăng hiệu suất vì bộ nhớ cache cũng có giới hạn vật lý, bộ nhớ lớn hơn thì chậm hơn. Thêm nhiều nhân hơn vào bộ vi xử lý thì nó cũng đắt hơn. Ngoài ra điều đó không thể là vô tận. Các bộ xử lý đa nhân này có thể  chạy đa luồng và điều đó mang lại sư đồng bộ cho bức tranh. Chúng ta sẽ thảo luận sau.

Vì vậy nếu ta không thể dựa vào những cải tiến phần , chỉ còn một con đường duy nhất là phần mền hiệu quả hơn để tăng hiệu suất. Nhưng thật đáng buồn, ngôn ngữ lập trình hiện đại không hiệu quả 

> "Bộ vi xử lý hiện đại giống như những chiếc xe vui nhộn nito, chúng nổi trội ở phần tư dặm đầu. Không may may nhưng ngôn ngữ lập trình hiện đại giống như Monte Carlo, chúng đủ khúc khuỷu." — [David Ungar][15]

* * *

### **Go có goroutines !!**

Như chúng ta đã thảo luận ở trên, các nhà sản xuất đang thêm nhiều nhân hơn vào bộ vi sử lý để tăng hiệu suất. Tất cả các trung tâm dữ liệu  đều đang chạy trên những bô vi xử lý đó  và chúng ta sẽ mong đợi sự gia tăng về nhân trong những năm sắp tới. Thêm vào đó, những ứng dụng ngày nay sử dụng nhiều  micro-services để duy trì kết nối cở sử dữ liệu, message queues và duy trì bộ nhớ cache. vì thế, phần mền chúng ta phát triển và những ngôn ngư lập trình nên hỗ trợ đồng thời và chúng co khả năng mở rộng với số lượng core tăng lên.

Nhưng, hầu hết các ngôn ngữ lập trình hiện đại(như Java, Python etc.) đến từ môi trường đơn luồng 90s. Hầu hết các ngôn ngữ lập trình đều hỗ trợ đa luồng. Nhưng khi thực hiện đồng thời thì có vấn đề xảy ra, threading-locking, race conditions và deadlocks.Những điều đó làm cho việc tạo ra một ứng dụng đa luông trên những ngôn ngữ đó trở nên khó khăn.

Ví dụ, thêm một luồng mới trong Java không phải là bộ nhớ hiệu quả. Vì mỗi luồng tiêu thụ khoảng 1MB bộ heap và cuối cùng nếu bạn bắt đầu lặp lại hàng nghìn luồng, chúng sẽ gây quá tải lên heap và heap  đóng cửa do hết bộ nhớ. Cũng như thế, nếu bạn muốn giao tiếp giữa 2 hoặc nhiều luồng điều đó rất .

Mắt khác, Go đã phát hành năm 2009 khi bộ sử lý đa nhân đã  có sẵn. Đó là lý do tại sao Go được xây dựng. Go có  goroutines thay cho luồng. Nó chiếm gần 2KB bộ nhớ. Vì vậy, bạn có lặp lại hàng triệu goroutines bất cứ lúc nào.

![][16]

Cách Goroutines hoạt động?  [Reffrance]( http://golangtutorials.blogspot.in/2011/06/goroutines.html)

**Các lợi ích khác là:**

* Goroutines có ngăn xếp phân đoạn và có thể phát triển.Diều đó có nghĩa là nó sẽ chỉ sử dụng nhiều bộ nhớ hơn khi cần thiết.
* Goroutines có thời gian khởi động nhanh hơn luồng.
* Goroutines xây dựng cùng với primitives để giao tiếp an toàn giữa các kênh.
* Goroutines cho phép bạn tránh phải sử dụng khóa mutex khi chia sể cấu trúc dữ liệu.
* Mặc dù, goroutines và  luồng OS không có ánh xạ 1:1.  Một goroutine  đơn có thể chạy trên nhiều luồng. Nhiều Goroutine được ghép thành số lượng nhỏ các luồng OS.

> Ban có thể xem Rob Pike's nói  [Đồng thời không phải là song song][17] để hiểu sâu hơn về điều này.

Ở tất cả các điểm , cho thấy Go rất mạnh mễ để sử lý đồng thời giống như Java, C và C++ đồng thời giữ cho đoạn mã thực hiện đồng thời và đẹp như Erlang.

![][18]

Go là tốt cả hai công việc. Dễ dàng viết đồng thời và hiệu quả để quản lý đồng thời 
* * *

### Go chạy trực tiếp trên phần cứng cơ bản.

Một lợi ích đáng kể nhất khi sử dụng C, C++ so với các ngôn ngữ bậc cao hiện đại khác như  Java/Python là hiệu suất của chúng. Bởi vì C/C++ chúng được biên dịch và không thông dịch.

Bộ sử lý hiểu các mã nhị phân. Nói chung là, khi bạn xây dựng một ứng dụng sử dụng Java hoặc các ngôn ngữ dựa trên JVM khác khi bạn biên dịch dự án của mình, chúng biên dịch  mã mà con người đọc được thành byte cái mà JVM hoặc máy ảo khác chạy trên các hệ điều hành cơ bản có thể hiểu được . Trong khi thực hiện, VM diễn giải các bytecode đó và chuyển đổi chúng thành các tập tin nhị phân mà bộ xử lý có thể hiểu được.

![][19]

Các bước thực hiện cho các ngôn ngữ dựa trên máy ảo

Trong khi đó, C/C++ không sử dụng máy ảo và điều đó loại bỏ một bước khỏi chu kỳ thực hiện và tăng hiệu suất. Nó trực tiếp biên dịch mã mà con người có thể đọc được thành mã nhị phân.

![][20]

Nhưng giải phóng và phân bố biến trong những ngôn ngữ đó là một nỗi đau đớn. Trong khi hầu hết các ngôn ngữ lập trình xử lý phân bổ và loại bỏ đối tượng bằng cách sử dụng các trình thu thập rác hoặc các thuật toán đếm tham chiếu

* * *

### Code được viết bằng Go rất dễ bảo trì.

Hãy để tôi nói với bạn một điều. Go không có cú pháp lập trình hỗn loạn như các ngôn ngữ lập trình khác. Nó có cú pháp gọn gàng và sạch sẽ.

Nhà thiết kế của Go tại Google có suy nghĩ như vậy khi tạo ra Go. Vì Google  có một lượng lớn code-base and và hàng nghìn lập trình viên  đang làn việc trên code-base, mã nên đơn giản để các lập trình viên khác có thể hiểu và một đoạn mã nên có tác dụng phụ tối thiểu trên một đoạn mã khác. Điều đó sẽ làm cho code dễ bảo trì và dễ sửa đổi.

Go cố tình bỏ qu nhiều tính năng của ngôn ngữ OOP hiện đại.

* **Không có những classe.** Mọi thứ chỉ được chia thành các package. Go chỉ có các struct thay vì các lớp classe.
* **Không hỗ  trợ kế thừa.** Điều đõ sẽ làm cho code đễ sửa đổi. Trong những ngôn ngữ khác như Java/Python, nếu class ABC kế thừa class XYZ  và bạn thực hiện một số thay đổi ở Calss XYZ, nó có thể tạo ra một số tác dụng phụ trong các class kế thừa XYZ. Bằng cách loại bỏ thừa kế, Go giúp dễ hiểu code  also  _(vì không  super class để xét trong khi nhìn vào một đoạn )_. 
* Không có constructors.
* Không có  annotations.
* Không có  generics.
* Không có  exceptions.

Tất cả thay đổi làm cho Go rất khác với những ngôn ngữ khác và làm cho lập trình Go cũng khác. Bạn có thể không thích một số điểm trên. Nhưng bạn có thể code ứng dụng của bạn khi không có những tính năng trên. Tất cả những gì bạn phải làm là viết 2-3 dòng nữa. Nhưng về mặt tích cực, nó sẽ làm cho mã của bạn sạch hơn và thêm rõ ràng hơn cho mã của bạn.

![][21]

Code readability vs, Efficiency.

Biểu đồ trên hiển thị rằng Go gần như hiệu quả như C / C ++, trong khi vẫn giữ cú pháp mã đơn giản như Ruby, Python và các ngôn ngữ khác. Đó là một tình huống có lợi cho cả con người và bộ vi xử lý !!!   
[Không giống như các ngôn ngữ mới khác như Swift][22],  cú pháp của Go rất ổn định. Nó vẫn như cũ kể từ khi phát hành công khai ban đầu 1.0, trở lại trong năm 2012. Điều đó làm cho nó tương thích ngược.

### Go được hỗ trợ bởi Google.

* Tôi biết đây không phải là một lợi thế kỹ thuật trực tiếp. Tuy nhiên, Go được thiết kế và hỗ trợ bởi Google. Google có một trong những cơ sở hạ tầng đám mây lớn nhất trên thế giới và nó được mở rộng quy mô. Go được thiết kế bởi Google để giải quyết các vấn đề của họ về hỗ trợ khả năng mở rộng và hiệu quả. Đó là những vấn đề tương tự bạn sẽ phải đối mặt trong khi tạo ra các máy chủ của riêng bạn.

* Thêm vào đó Go cũng được sử dụng bởi một số công ty lớn như Adobe, BBC, IBM, Intel và thậm chí [Medium][23].  _([Source]( https://github.com/golang/go/wiki/GoUsers))_

### **Kết:**

*Mặc dù Go rất khác với các ngôn ngữ hướng đối tượng khác, nó vẫn là cùng một bản . Go cung cấp cho bạn hiệu suất cao như C / C ++, xử lý đồng thời siêu hiệu quả như Java và thú vị với mã như Python / Perl.
* Nếu bạn không có bất kỳ kế hoạch để tìm hiểu Go, tôi vẫn sẽ nói giới hạn phần cứng đặt áp lực cho chúng tôi, các nhà phát triển phần mềm để viết mã siêu hiệu quả. Nhà phát triển cần hiểu phần cứng và làm cho chương trình của họ tối ưu hóa phù hợp. **Phần mềm được tối ưu hóa có thể chạy trên phần cứng rẻ hơn và chậm hơn (như thiết bị **[**_IOT_**][24]**)và tác động tổng thể tốt hơn đến trải nghiệm người dùng cuối.**
* * *


![][27]


   ### Credits: * _GoLang or the future of the dev_ from [Edoardo Paolo Scalafiotti][28] * [Program your next server in Go][29] * [Concurrency Is Not Parallelism][30] by Rob Pike * [Why Go?][31] * [Golang][32] * [Software Development][33] * [Web Development][34] * [Programming][35] * [Software][36] 41K 123 * BlockedUnblockFollowFollowing ![Go to the profile of Keval Patel][5] ### [Keval Patel][37] Medium member since Sep 2018 [www.kevalpatel2106.com][38] | Android Developer | Machine learner | Gopher | Open Source Contributor * Follow ![Exploring Code][39] ### [Exploring Code][40] Explore the new areas of software tech * 41K * * * [1]: https://medium.com/
  [2]: https://medium.com/exploring-code?source=logo-lo_W6HjYQfXaXJE---12450c50a426
  [3]: https://medium.com/m/signin?redirect=https%3A%2F%2Fmedium.com%2Fexploring-code%2Fwhy-should-you-learn-go-f607681fad65&source=--------------------------nav_reg&operation=login
  [4]: https://medium.com/m/signin?redirect=https%3A%2F%2Fmedium.com%2Fexploring-code%2Fwhy-should-you-learn-go-f607681fad65&source=--------------------------nav_reg&operation=register
  [5]: https://cdn-images-1.medium.com/fit/c/120/120/1*Nj-bY5v0-iBgsf3boes5Wg.png
  [6]: https://medium.com/@kevalpatel2106?source=post_header_lockup
  [7]: https://cdn-images-1.medium.com/max/1600/1*vHUiXvBE0p0fLRwFHZuAYw.gif
  [8]: https://twitter.com/tobi/status/326086379207536640
  [9]: https://golang.org/
  [10]: http://www.investopedia.com/terms/m/mooreslaw.asp
  [11]: http://www.informit.com/articles/article.aspx?p=339073
  [12]: http://www.apple.com/macbook-pro/specs/
  [13]: https://cdn-images-1.medium.com/max/1600/1*Azz7YwzYYR6lDKFj8iIGZg.png
  [14]: https://www.quora.com/What-is-Quantum-Tunneling-Limit-How-does-it-limit-the-size-of-a-transistor
  [15]: https://en.wikipedia.org/wiki/David_Ungar
  [16]: https://cdn-images-1.medium.com/max/1600/1*NFojvbkdRkxz0ZDbu4ysNA.jpeg
  [17]: https://blog.golang.org/concurrency-is-not-parallelism
  [18]: https://cdn-images-1.medium.com/max/1600/1*xbsHBQJReC5l_VO4XgNSIQ.png
  [19]: https://cdn-images-1.medium.com/max/1600/1*TVR-VLVg68KwCOLjqQmQAw.png
  [20]: https://cdn-images-1.medium.com/max/1600/1*ii6xUkU_PchybiG8_GnOjA.png
  [21]: https://cdn-images-1.medium.com/max/1600/1*nlpYI256BR71xMBWd1nlfg.png
  [22]: https://www.quora.com/Is-Swifts-syntax-still-changing
  [23]: https://medium.engineering/how-medium-goes-social-b7dbefa6d413#.r8nqjxjpk
  [24]: https://en.wikipedia.org/wiki/Internet_of_things
  [25]: http://bit.ly/2h9p8o2
  [26]: http://bit.ly/2iTjfui
  [27]: https://cdn-images-1.medium.com/max/2000/1*8Mc_aN82rWqW56PAY5-5mg.jpeg
  [28]: https://medium.com/@edoardo849
  [29]: https://www.youtube.com/watch?v=5bYO60-qYOI
  [30]: https://vimeo.com/49718712
  [31]: https://nathany.com/why-go/
  [32]: https://medium.com/tag/golang?source=post
  [33]: https://medium.com/tag/software-development?source=post
  [34]: https://medium.com/tag/web-development?source=post
  [35]: https://medium.com/tag/programming?source=post
  [36]: https://medium.com/tag/software?source=post
  [37]: https://medium.com/@kevalpatel2106 "Go to the profile of Keval Patel"
  [38]: http://www.kevalpatel2106.com
  [39]: https://cdn-images-1.medium.com/fit/c/120/120/1*H9-m42Ii0l95BDzAqULR9A.png
  [40]: https://medium.com/exploring-code?source=footer_card
