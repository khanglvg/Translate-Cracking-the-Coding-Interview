# Kiểm thử (Testing)
## Concepts and Algorithms: Solutions

> **Ví dụ 1:**
	Tìm (những) lỗi trong đoạn code sau:
  ```
  unsigned int i;
  for (i = 100; i >= 0; --i)
    printf("%d\n", i);
  ```

#### **Giải Pháp**

Có 2 lỗi trong đoạn code trên.

_Một_ là `unsigned int`, theo định nghĩa, 1 biến có kiểu `unsigned int` thì có giá trị lớn hơn hoặc bằng 0. Vòng lặp điều kiện `for` sẽ luôn đúng, do đó, nó sẽ thực hiện lặp vô tận.

=> Code đúng để in tất cả các số từ 100 về 1 là `i > 0`. Nếu ta muốn in ra số 0 thì có thể thêm câu lệnh `printf` sau vòng lặp.

   ```
  unsigned int i;
  for (i = 100; i > 0; --i)
    printf("%d\n", i);
  ```
  _Hai_ Chỉnh sửa thêm 1 chỗ nữa là sử dụng `%u` thay cho `%d`, ta sẽ in ra kiểu `unsigned int`:
  
  ```
  unsigned int i;
  for (i = 100; i > 0; --i)
    printf("%u\n", i);
  ```
 :purple_heart: Vậy là đoạn code sẽ in ra danh sách các số từ 100 về 1 theo đúng mong muốn. :purple_heart:
  
  ___
  
  > **Ví dụ 2:** 
  Bạn nhận được một mã nguồn cho một ứng dụng mà mỗi lần chạy đều bị ~~crash~~. Sau khi chạy 10 lần ở chế độ debug, bạn nhận ra rằng ứng dụng sẽ không bị ~~crash~~ ở cùng 1 nơi. Ứng dụng chạy đơn luồng và chỉ sử dụng thư viện chuẩn C. Vậy lý do dẫn đến lỗi ~~crash~~ ứng dụng là gì? Ứng với mỗi lần như vậy bạn sẽ kiểm tra như thế nào?
  
  #### **Giải Pháp**
  
  Độ khó của câu hỏi phụ thuộc vào loại ứng dụng được chuẩn đoán. Tuy nhiên, ta có thể đưa ra một vài nguyên nhân chung dẫn đến việc ~~crash~~ ứng dụng ngẫu nhiên như sau: 
  1. _"Biến ngẫu nhiên:"_ Ứng dụng có thể sử dụng vài con số hoặc thành phần biến ngẫu nhiên mà những thành phần đó có thể không được xử lý trong mỗi lần thực thi chương trình. 
      - Những ví dụ bao gồm: Nhập liệu người dùng, một số được sinh tự động ngẫu nhiên hoặc thời gian trong ngày.
  2. _Biến chưa được khởi tạo:_ Ứng dụng có thể có một biến chưa được khởi tạo, trong một số ngôn ngữ lập trình, có thể dẫn đến lỗi là do nó nhận một giá trị tùy ý. Giá trị của biến này có thể dẫn đến trong code có sự khác biệt nhỏ trong đường dẫn ở mỗi lần chạy.
  3. _Memory Leak:_ Ứng dụng có thể bị tràn bộ nhớ. Những nguyên nhân khác hoàn toàn ngẫu nhiên cho mỗi lần thực thi chương trình, nó phụ thuộc vào số lượng quá trình (process) được chạy ở từng thời điểm cụ thể. Cũng có thể là do tràn bộ nhớ đệm (heap overflow) hoặc dữ liệu bị hỏng.
  4. _Sự phụ thuộc ngoài:_ Ứng dụng có thể có sự phụ thuộc vào những ứng dụng khác. Nếu có nhiều sự phụ thuộc, ứng dụng có thể bị ~~crash~~ ở nhiều điểm.
  
  Để theo dõi và bắt được những lỗi này, ta nên bắt đầu tìm hiểu và học nhiều nhất có thể về ứng dụng. :joy::joy::joy:
  - "Ai sẽ chạy ứng dụng?"
  - "Họ làm vậy vì điều gì?"
  - "Loại ứng dụng này là gì?"
  - ...
  
:point_right:  Thêm vào đó, mặc dù ứng dụng có thể không ~~crash~~ ở chính xác cùng chỗ nhưng nó cũng có thể được liên kết với những thành phần (components) hoặc những sự kiện (scenarios) riêng biệt.
- Cho một ví dụ đơn giản: Ứng dụng sẽ không bao giờ ~~crash~~ nếu nó khởi chạy một cách đơn giản và không được động đến. Sau đó nó xảy ra lỗi ở một vài chỗ sau khi loading 1 file. Hoặc nó có thể bị ~~crash~~ ở những thành phần (component) thấp hơn như là việc nhập xuất file (I/O file).

:point_right:  Phép loại trừ cũng khá hữu dụng trong việc giải quyết vấn đề này. Đóng tất cả các ứng dụng trong hệ thống. Theo dõi các tài nguyên một cách cẩn thận. Nếu cảm thấy phần nào đó của ứng dụng có thể tắt đi thì hãy thực hiện (và đừng suy nghĩ thêm :stuck_out_tongue_closed_eyes::stuck_out_tongue_closed_eyes::stuck_out_tongue_closed_eyes:). Thử chạy ứng dụng ở một thiết bị khác và xem thử nó có bị cùng một lỗi hay không. Thực hiện việc loại trừ càng nhiều thì càng dễ tìm ra được lỗi và giải quyết nó.

:point_right:  Hơn thế nữa, ta có thể dùng những công cụ (tools) hỗ trợ trong một số trường hợp cụ thể.
	       - Ví dụ: để kiểm tra lỗi #2, ta có thể sử dụng công cụ (tool) runtime để kiểm tra lỗi _biến chưa được khởi tạo_.

___

> **Ví dụ 3:** 
 Ta có phương pháp sau đây có thể sử dụng trong trò chơi cờ vua: boolean canMoveTo(int x, int y). Phương pháp này là một phần của lớp Piece và trả về có thể đi hay không tới vị trí (x,y). Giải thích rằng bạn sẽ kiểm tra phương pháp này như thế nào.

   
#### **Giải Pháp**

Ở vấn đề này, có 2 loại kiểm thử chính: xác thực trường hợp cực đoan (đảm bảo rằng chương trình sẽ không bị lỗi khi nhập vào dữ liệu xấu) và kiểm tra trường hợp chung. Ta sẽ bắt đầu với trường hợp đầu tiên:

**Kiểm thử loại #1: Kiểm thử cực đoan**

Ta cần đảm bảo rằng chương trình xử lý thông tin đầu vào xấu hoặc không bình thường. Điều này có nghĩa là kiểm tra các điều kiện sau:
- Kiểm tra với x và y là số âm.
- Kiểm tra giá trị x lớn hơn chiều rộng.
- Kiểm tra giá trị y lớn hơn chiều dài.
- Kiểm tra với bàn cờ bị đầy (không còn chỗ trống).
- Kiểm tra với bàn cờ có một chỗ trống hoặc hầu như bàn cờ trống.
- Kiểm tra với việc ô trắng nhiều hơn ô đen.
- Kiểm tra với việc ô đen nhiều hơn ô trắng.

Đối với những lỗi ở trên, ta có thể hỏi người phỏng vấn muốn ta trả về false hay quăng ra biệt lệ và ta nên kiểm tra tương ứng.

**Kiểm thử loại #2: Kiểm thử chung*

Kiểm thử chung rộng hơn rất nhiều. Lý tưởng nhất là ta nên kiểm tra mỗi bàn cờ có thể nhưng có quá nhiều bàn cờ. Tuy nhiên, ta có thể thực hiện đối với phạm vi hợp lý có thể của các bàn cờ khác nhau. Có 6 mảnh trong bộ cờ, do đó ta có thể kiểm trả từng mảnh so với các mảnh còn lại theo mọi hướng có thể. Việc này trông nhưng đoạn mã giả dưới đây:
```
foreach piece a: 
  foreach other type of piece b (6 types + empty space ) 
    foreach direction d
      Create a board with piece a.
      Place piece b in direction d.
      Try to move - check return value.
```
Chìa khóa để giải quyết vấn đề này là ta nhận ra rằng ta không thể kiểm tra tất cả các trường hợp có thể xảy ra ngay cả khi ta mong muốn. Chính vì vậy, thay vào đó, ta nên tập trung vào những vùng thiết yếu.

___

> **Ví dụ 4:**
  Bạn sẽ kiểm tra tải một trang web như thế nào nếu không sử dụng bất kì công cụ kiểm thử nào?
     
#### **Giải Pháp**

Kiểm tra tải giúp xác định khả năng hoạt động tối đa của một ứng dụng web, cũng như bất kỳ sực tắc nghẽn nào có thể ảnh hưởng đến hiệu suất hoạt động của ứng dụng đó. Tương tự, có thể kiểm tra cách ứng dụng phản hồi với các biến thể trong khi tải. Để thực hiện việc kiểm tra tải, trước hết, ta phải xác định các tình huống quan trọng về hiệu suất và các chỉ số đáp ứng các mục tiêu hiệu suất. Tiêu chí điển hình bao gồm:
- Thời gian phản hồi.
- Năng suất.
- Sử dụng tài nguyên.
- Tốc độ tải tối đa mà hệ thống có thể chịu đựng. 

:point_right:  Sau đó, ta thiết kế kiểm tra tải giả lập, cẩn thận đo lường với mỗi tiêu chí.

:point_right:  Trong trường hợp không có các công cụ kiểm tra chính thức, ta về cơ bản có thể tạo ra công cụ của riêng mình. 
- Cho ví du: ta có thể giả lập người dùng đồng thời bằng cách tạo ra hàng nghìn người dùng ảo. Ta có thể viết một chương trình đa luồng với vài nghìn luồng, trong đó mỗi luồng sẽ hoạt động như một người dùng thực tế để tải trang. Với mỗi người dùng, ta sẽ lập trình đo thời gian phản hồi, dữ liệu, đọc ghi, v.v.
 
:point_right:   Ta cũng có thể phân tích kết quả dựa trên dữ liệu thu thập được trong quá trình thử nghiệm và so sánh chúng với các giá trị có thể chấp nhận.

___

> **Ví dụ 5:**
  Bạn sẽ kiểm tra một cây viết mực như thế nào?
        
#### **Giải Pháp**

Độ khó của câu hỏi là việc hiểu được các ràng buộc và cách tiếp cận vấn đề một cách có cấu trúc.
Để hiểu được các ràng buộc, bạn nên đặt ra nhiều câu hỏi để hiểu như "ai, cái gì, khi nào, ở đâu, như thế nào và tại sao?" của một vấn đề (hoặc có thể hỏi những dạng câu hỏi như vậy áp dụng chúng cho vấn đề này). Hãy nhớ rằng, một người kiểm thử giỏi sẽ hiểu được chính xác người đó đang kiểm tra thứ gì trước khi bắt tay vào công việc. 

Để minh họa phương pháp trong vấn đề này, ta xem qua một đoạn hội thoại giả định sau:

**Người phỏng vấn**: Bạn sẽ kiểm tra một cây viết mực như thế nào?

**Người ứng cử**: Để tôi tìm hiểu một chút về cây viết này. Ai sẽ sử dụng viết?

**Người phỏng vấn**: Hầu hết là trẻ em. 

**Người ứng cử**: Okay, thú vị đấy. Họ sẽ làm gì với chúng? Viết, vẽ, hoặc làm gì khác?

**Người phỏng vấn**: Vẽ. 

**Người ứng cử**: Ồ tuyệt, Chúng sẽ vẽ trên gì? Giấy? Quần áo? Tường?

**Người phỏng vấn**: Trên quần áo. 

**Người ứng cử**: Hay. Loại đầu mực của cây viết là gì? Bằng nỉ (viết lông) hay là đầu bi? Mực lâu phai hay mực dễ xóa?

**Người phỏng vấn**: Mực dễ xóa. 

Nhiều câu hỏi trôi qua, bạn có thể nhận được kết luận:

**Người ứng cử**: Okay, tôi đã hiểu rồi. Chúng ta có một cây viết cho trẻ em từ 5 đến 10 tuổi. Là loại viết lông và màu đỏ, xanh lá, xanh dương và đen, loại dễ phai, khi viết lên quần áo có thể giặt sạch, phải không?

:point_right:  Ứng cử viên đã nắm được vấn đề một cách rõ ràng, khác biệt rất nhiều so với lúc đầu. Điều này không phải hiếm gặp. Trong thực tế, rất nhiều người phỏng vấn cố tình đưa ra những vấn đề trông có vẻ rõ ràng (ai mà chả biết cây viết là gì ?!?), nhưng chỉ khi bạn khám phá ra rằng vấn đề khá là khác so với những gì bạn nghĩ. Họ tin rằng những người dùng làm những việc giống nhau mặc dù người dùng làm một cách ngẫu nhiên.

Bây giờ bạn đã hiểu bạn đã kiểm tra thứ gì rồi, đã đến lúc đặt ra kế hoạch cho việc bắt đầu. Chìa khóa ở đây là một cấu trúc.

Cân nhắc xem sự khác biệt giữa các thành phần của vật thể hay vấn đề, xuất phát từ đó. Trong trường hợp này, những thành phần có thể là:
- _Kiểm tra nhanh:_ Thẩm định cây viết là viết lông và loại màu mực.
- _Ý định sử dụng:_ Vẽ. Có chắc rằng chỉ viết trên quần áo?
- _Ý định sử dụng:_ Giặt. Khi vẽ lên quần áo rất dễ giặt ra mặc dù để thời gian dài? Giặt sạch bằng nước ấm hay nước lạnh?
- _Sự an toàn:_ Cây viết không có chất độc hại cho trẻ em?
- _Không có định hướng:_ Trẻ em còn dùng viết vào mục đích khác? Có thể viết lên bề mặt khác, bạn có thể kiểm tra trạng thái đó là đúng. Họ cũng có thể giẫm mạnh lên viết, quăng nó đi, v.v. Bạn cần đảm bảo rằng cây viết vẫn "sống sót" qua những điều kiện trên.

:point_right:  Hãy nhớ rằng trong bất kì câu hỏi nào, bạn cần kiểm tra cả trường hợp có định hướng và không có định hướng. Người dùng không phải lúc nào cũng sử dụng sản phẩm theo cách mà bạn mong muốn họ sử dụng.

___

> **Ví dụ 6:**
  Bạn sẽ kiểm tra một cây ATM trong hệ thống ngân hàng được phân bố như thế nào?
        
#### **Giải Pháp**

Việc đầu tiên cần làm để trả lời câu hỏi này là làm cho nó được rõ nghĩa. Hỏi theo trình tự sau: 
- Ai là người sử dụng cây ATM? Có thể là mọi người, hoặc người mù, hoặc nhiều câu học khác.
- Họ sử dụng cây ATM vào mục đích gì? Có thể là rút tiền, chuyển khoản, hoặc đơn giản là kiểm tra số tiền còn trong tài khoản hoặc làm gì đó khác.
- Công cụ gì để ta có thể kiểm tra được? Ta có thể truy cập vào code hoặc cây ATM được hay không? 

Hãy nhớ rằng: Một người kiểm thử viên tốt là một người biết rõ người đó đang kiểm tra thứ gì!

Một khi ta hiểu được hệ thống trông như thế nào, ta sẽ muốn giải quyết hết các vấn đề liên quan đến các thành phần có thể kiểm tra được khác nhau. Những thành phần đó bao gồm:
- Đăng nhập.
- Rút tiền.
- Gửi tiền. 
- Kiểm tra tài khoản.
- Giao dịch.

Ta hầu như chắc chắn sẽ muốn sử dụng cả kiểm tra tự động và kiểm tra bằng tay.

:point_right:  Kiểm tra bằng tay sẽ bao gồm các bước bên trên, chắc chắn rằng kiểm tra tất cả các lỗi xảy ra (số dư thấp, tài khoản mới, tài khoản không tồn tại, v.v). 

:point_right:  Kiểm tra tự động thì hơi phức tạp hơn tí. Ta cũng muốn tự động hóa tất cả những sự kiện chuẩn như trên, và cũng muốn tìm kiếm một vài vấn đề riêng biệt, như là [Race Condition](https://en.wikipedia.org/wiki/Race_condition). Ý tưởng là ta sẽ cài đặt một hệ thống đóng với những tài khoản giả và đảm bảo rằng cho dù ai đó rút, gửi tiền ở những nơi khác thì người đó cũng sẽ không mất hay nhận được tiền như là điều người đó không mong muốn. 

:point_right:  Trên hết, ta cần ưu tiên cao cho việc bảo mật và đáng tin cậy. Người dùng phải luôn được bảo vệ và ta phải đảm bảo rằng tiền luôn luôn còn nguyên :laughing::laughing::laughing:. Không ai muốn một ngày đẹp trời kiểm tra tài khoản và toàn bộ số tiền không cánh mà bay! Một người kiểm thử tốt phải hiểu được độ ưu tiên của hệ thống.
