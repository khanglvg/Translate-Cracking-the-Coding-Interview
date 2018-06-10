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
 We have the following method used in a chess game: boolean canMoveTo(int x, int y). This method is part of the Piece class and returns whether or not the piece can move to position (x, y). Explain how you would test this method. 
   
#### **Giải Pháp**

In this problem, there are two primary types of testing: extreme case validation (ensuring that the program doesn't crash on bad input), and general case testing. We'll start with the first type.

**Testing Type #1: Extreme Case Validation**

We need to ensure that the program handles bad or unusual input gracefully. This means checking the following conditions:
- Test with negative numbers for x and y.
- Test with x larger than the width.
- Test withy larger than the heigh.
- Test with a completely full board.
- Test with an empty or nearly empty board.
- Test with far more white pieces than black.
- Test with far more black pieces than white.
For the error cases above, we should ask our interviewer whether we want to return false or throw an exception, and we should test accordingly. 

**Testing Type #2: General Testing**

General testing is much more expansive. Ideally, we would tes t every possible board, but there are far too many boards. We can, however, perform a reasonable coverage of different boards . 
There are 6 pieces in chess, so we can test each piece against every other piece, in every possible direction.This would look something like the below code: 
```
foreach piece a: 
  foreach other type of piece b (6 types + empty space ) 
    foreach direction d
      Create a board with piece a.
      Place piece b in direction d.
      Try to move - check return value.
```
The key to this problem is recognizing that we can't test every possible scenario, even if we would like to. So, instead, we must focus on the essential areas.

___

> **Ví dụ 4:**
  How would you load test a webpage without using any test tools?
     
#### **Giải Pháp**

Load testing helps to identify a web application's maximum operating capacity, as well as any bottlenecks that may interfere with its performance. Similarly, it can check how an application responds to variations in load.
To perform load testing, we must first identify the performance critical scenarios and the metrics which fulfill our performance objectives. Typical criteria include:
- Response time
- Throughput
- Resource utilization
- Maximum load that the system can bear. 

:point_right:  Then, we design tests to simulate the load, taking care to measure each of these criteria.

:point_right:  In the absence of formal testing tools, we can basically create our own.
- For example: we could simulate concurrent users by creating thousands of virtual users. We would write a multi-threaded program with thousands of threads, where each thread acts as a real-world user loading the page. For each user, we would programmatically measure response time, data I/O, etc.
 
:point_right:   We would then analyze the results based on the data gathered during the tests and compare it with the accepted values.

___

> **Ví dụ 5:**
  How would you test a pen?
        
#### **Giải Pháp**

This problem is largely about understanding the constraints and approaching the problem in a structured manner.
To understand the constraints, you should ask a lot of questions to understand the "who, what , where, when, how and why" of a problem (or as many of those as apply to the problem). Remember that a good tester understands exactly what he is testing before starting the work. 
To illustrate the technique in this problem, let us guide you through a mock conversation.

**Interviewer**: How would you test a pen?

**Candidate**: Let me find out a bit about the pen. Who is going to use the pen? 

**Interviewer**: Probably children. 

**Candidate**: Okay, that's interesting. What will they be doing with it? Will they be writing, drawing, or doing something else with it? 

**Interviewer**: Drawing. 

**Candidate**: Ok, great. On what? Paper? Clothing? Walls? 

**Interviewer**: On clothing. 

**Candidate**: Great. What kind of tip does the pen have? Felt? Ball point? Is it intended to wash off, or is it intended to be permanent? 

**Interviewer**: It's intended to wash off. 

Many questions later, you may get to this:

**Candidate**: Okay, so as I understand it , we have a pen that is being targeted at 5 to 10 year olds. The pen has a felt tip and comes in red, green, blue and black. It's intended to wash off when clothing is washed. Is that correct?

:point_right:  The candidate now has a problem that is significantly different from what it initially seemed to be. This is not uncommon. In fact, many interviewers intentionall y give a problem that seems clear (everyone knows what a pen is!), only to let you discover that it's quite a different problem from what it seemed. Their belief is that users do the same thing, though users do so accidentally.

Now that you understand what you're testing, it's time to come up with a plan of attack. The key here is structure. 

Consider what the different components of the object or problem, and go from there. In this case, the components might be:
- _Fact check_: Verify that the pen is felt tip and that the ink is one of the allowed colors. 
- _Intended use_: Drawing. Does the pen write properly on clothing?
- _Intended use_: Washing. Does it wash off of clothing (even if it's been there for an extended period of time)? Does it wash off in hot, warm and cold water? 
- _Safety_: Is the pen safe (non-toxic) for children?
- _Unintended uses_: How else might children use the pen? They might write on other surfaces, so you need to check whether the behavior there is correct. They might also stomp on the pen , throw it , and so on. You'll need to make sure that the pen holds up under these conditions.

:point_right:  Remember that in any testing question, you need to test both the intended and unintended scenarios. People don't always use the product the way you want them to.

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
