# Kiểm thử (Testing)
## Concepts and Algorithms: Solutions

> Ví dụ 1:
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
  
  > Ví dụ 2:
  Bạn nhận được một mã nguồn cho một ứng dụng mà mỗi lần chạy đều bị crash. Sau khi chạy 10 lần ở chế độ debug, bạn nhận ra rằng ứng dụng sẽ không bị crash ở cùng 1 nơi. Ứng dụng chạy đơn luồng và chỉ sử dụng thư viện chuẩn C. Vậy lý do dẫn đến lỗi crash ứng dụng là gì? Ứng với mỗi lần như vậy bạn sẽ kiểm tra như thế nào?
  
  #### **Giải Pháp**
  
  Độ khó của câu hỏi phụ thuộc vào loại ứng dụng được chuẩn đoán. Tuy nhiên, ta có thể đưa ra một vài nguyên nhân chung dẫn đến việc crash ứng dụng ngẫu nhiên như sau: 
  1. _"Biến ngẫu nhiên:"_ Ứng dụng có thể sử dụng vài con số hoặc thành phần biến ngẫu nhiên mà những thành phần đó có thể không được xử lý trong mỗi lần thực thi chương trình. 
      - Những ví dụ bao gồm: Nhập liệu người dùng, một số được sinh tự động ngẫu nhiên hoặc thời gian trong ngày.
  2. _Biến chưa được khởi tạo:_ Ứng dụng có thể có một biến chưa được khởi tạo, trong một số ngôn ngữ lập trình, có thể dẫn đến lỗi là do nó nhận một giá trị tùy ý. Giá trị của biến này có thể dẫn đến trong code có sự khác biệt nhỏ trong đường dẫn ở mỗi lần chạy.
  3. _Memory Leak:_ Ứng dụng có thể bị tràn bộ nhớ. Những nguyên nhân khác hoàn toàn ngẫu nhiên cho mỗi lần thực thi chương trình, nó phụ thuộc vào số lượng quá trình (process) được chạy ở từng thời điểm cụ thể. Cũng có thể là do tràn bộ nhớ đệm (heap overflow) hoặc dữ liệu bị hỏng.
  4. _Sự phụ thuộc ngoài:_ Ứng dụng có thể có sự phụ thuộc vào những ứng dụng khác. Nếu có nhiều sự phụ thuộc, ứng dụng có thể bị crash ở nhiều điểm.
  
  Để theo dõi và bắt được những lỗi này, ta nên bắt đầu tìm hiểu và học nhiều nhất có thể về ứng dụng. :joy::joy::joy:
  - "Ai sẽ chạy ứng dụng?"
  - "Họ làm vậy vì điều gì?"
  - "Loại ứng dụng này là gì?"
  - ...
  
:point_right:  Thêm vào đó, mặc dù ứng dụng có thể không crash ở chính xác cùng chỗ nhưng nó cũng có thể được liên kết với những thành phần (components) hoặc những sự kiện (scenarios) riêng biệt.
  
