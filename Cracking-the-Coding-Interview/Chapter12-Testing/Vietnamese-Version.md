# Kiểm thử (Testing)

> Trước khi bạn lướt qua phần này và nói rằng “tôi không phải là một tester”, hãy dừng lại một chút và suy nghĩ. Testing là một khâu quan trọng đối với một kĩ sư phần mềm, bởi lí do này nên những câu hỏi liên quan đến testing có thể xuất hiện trong cuộc phỏng vấn của bạn. Dĩ nhiên, nếu bạn ứng cử bản thân cho vị trí Tester thì đây là lúc bạn nên chú ý đó!
Những vấn đề của Testing thường rơi vào 1 trong 4 hạng mục: 
> 1. Test 1 vật thể thực tại (ví dụ như 1 cây bút bi).
> 2. Test 1 phần của phần mềm. 
> 3. Viết test code cho một chức năng.
> 4. Sửa chữa một vấn đề đang hiện hữu. 

> Chúng ta sẽ cùng tiếp cận từng vấn đề trong 4 loại nêu trên.
> Hãy nhớ rằng 4 loại nêu trên yêu cầu bạn đừng cho rằng input hay user sẽ hoạt động tốt. Hãy trông chờ vào những lỗi có thể xuất hiện và lên kế hoạch cho chúng.


## Definitions

### **Người phỏng vấn đang tìm kiếm những gì từ bạn?**

Bề ngoài, những câu hỏi testing dường như chỉ là những danh sách test case phổ thông, và đúng rồi đó thêm một chút mở rộng nữa! Bạn cần phải có một danh sách test case hợp lý.
Hơn nữa, người phỏng vấn muốn kiểm tra những điều sau:
- _Big Picture Understanding (hiểu biết về bức tranh toàn cảnh):_ Bạn có phải là một người hiểu rõ thực sự phần mềm là gì không? Bạn có thể ưu tiên những test case đúng cách? Ví dụ, giả sử bạn được yêu cầu kiểm thử hệ thống e-commerce như Amazon. Thật tuyệt khi chắc rằng những hình ảnh của sản phẩm xuất hiện đúng chỗ, nhưng thậm chí quan trọng hơn là việc thanh toán hoạt động tin một cách đáng tin cậy, những sản phẩm được thêm vào hàng đợi vận chuyển và những khách hàng sẽ không bao giờ bị tính phí gấp đôi.
- _Knowing How the Pieces Fit Together (Hiểu biết về những mảnh ghép sẽ chắp nối với nhau như thế nào):_ Bạn có hiểu cách hoạt động của phần mềm và nó có thể sẽ tương thích với một hệ sinh thái lớn hơn? Giả sử bạn được yêu cầu test Google Spreadsheets. Việc quan trọng là bạn test phần mở đầu, lưu trữ và chỉnh sửa tài liệu. Nhưng Google Spreadsheets là một phần của 1 hệ sinh thái lớn hơn. Bạn cần phải test sự tương tác với Gmail, với plug-ins và một số các thành phần khác.
- _Organization (Tổ chức):_ Bạn có tiếp cận vấn đề bằng một cách thức có cấu trúc hay bạn chỉ trút ra những gì nghĩ ra trong đầu? Một số ứng viên khi được yêu cầu đưa ra những test case cho 1 camera sẽ chỉ viết ra bất kì điều gì và tất cả những gì họ có thể nghĩ ra. Một ứng viên giỏi sẽ chia các phần ra thành các hạng mục như Chụp hình, Quản lí hình ảnh, Cài đặt,… Cách tiếp cận có cấu trúc này cũng sẽ giúp bạn làm một cách triệt để hơn với việc tạo ra những test case.
- _Practicality(Tính thực tiễn):_ Bạn có thể thực sự tạo ra một kế hoạch testing hợp lý? Ví dụ, nếu 1 user báo rằng phần mềm bị hỏng khi họ mở một bức ảnh nhất định và bạn chỉ nói với họ rằng hãy cài đặt lại phần mềm, nó thường là không thực tế cho lắm. Kế hoạch testing của bạn phải khả thi và thực tế cho công ty có thể triển khai.

:point_right:  Chứng minh những khía cạnh trên sẽ thế hiện rằng bạn sẽ là một thành viên giá trị của một team testing.

### **Testing một vật thể trong thế giới thực**

Một số ứng viên bị bất ngờ khi được hỏi rằng test một cây bút mực như thế nào. Sau tất cả thì bạn sẽ phải testing phần mềm đúng không? Có thể lắm, nhưng những câu hỏi “đời thực” vẫn rất phổ biến. Hãy cùng giải quyết nó với một ví dụ sau.

:question: Bạn test 1 cái kẹp giấy như thế nào? :question:

**_Bước 1:_** Ai sẽ sử dụng nó? Tại sao?
- Bạn cần phải thảo luận với người phỏng vấn rằng ai đang sử dụng sản phẩm đó và mục đích của họ là gì. Câu trả lời có thể không giống như những gì bạn nghĩ. Câu trả lời có thể là “những giáo viên, dùng để kẹp giữ giấy tờ với nhau”, hoặc cũng có thể “những nghệ sĩ, dùng để bẻ thành hình dáng của con vật” hoặc là cả hai. Câu trả lời của câu hỏi này sẽ định hình cách trả lời của bạn cho những câu sau. 

**_Bước 2:_** Những trường hợp sử dụng (use case)?
- Sẽ rất hữu ích nếu bạn tạo một danh sách use case. Trong trường hợp này, use case có thể là đơn giản giữ các tờ giấy với nhau mà không làm hư giấy.
- Với một số câu hỏi khác, có thể sẽ có nhiều use case. Ví dụ như là sản phẩm đó cần có khả năng gửi và nhận nội dung hoặc viết hoặc tẩy xóa,…

**_Bước 3:_** Việc sử dụng nằm trong khuôn khổ nào?
- Khuôn khổ sử dụng nghĩa là giữ một lúc 30 tờ giấy mà không gây tổn hại (ví dụ như bị bẻ cong) và 50 tờ giấy với việc bị cong 1 phần nhỏ vĩnh viễn.
- Khuôn khổ cũng được mở rộng ra các nhân tố môi trường. Ví dụ, cái kẹp giấy có thể sử dụng trong nhiệt độ ấm (90 – 110 độ F)? Còn nếu rất lạnh thì thế nào?

**_Bước 4:_** Những điều kiện thất bại?
- Không có sản phẩm “không thể hỏng”, vì vậy việc phân tích các điều kiện dẫn tới hỏng hóc là một phần thiết yếu của việc testing. Sẽ tốt hơn nếu bạn có thể thảo luận với người phỏng vấn rằng khi nào sự hỏng hóc đó có thể chấp nhận được (thậm chí là cần thiết) và sự hỏng hóc đó có ý nghĩa gì.
- Ví dụ, nếu bạn đang test một cái máy giặt, có thể bạn quyết định rằng cái máy đó có thể xử lý ít nhất 30 cái áo hoặc quần. 30-45 cái có thể dẫn đến 1 số hệ quả nhỏ như là quần áo không được giặt sạch. Trong trường hợp nhiều hơn 45 cái áo quần, hệ quả cực lớn có thể được chấp nhận. Tuy nhiên, hệ quả cực lớn trong trường hợp này chỉ nên có thể là máy giặt không cung cấp nước chứ không phải là “lửa hay lụt”.

**_Bước 5:_** Bạn sẽ thực hiện việc testing như thế nào?
- Trong một số trường hợp, nó cũng có thể liên quan đến việc thảo luận về chi tiết việc thực hiện testing. Ví dụ, nếu bạn có thể đảm bảo rằng một cái ghế có thể chịu được việc sử dụng bình thường trong 5 năm, ắt hẳn rằng bạn không thể để nó trong nhà và chờ 5 năm sau. Thay vào đó, bạn sẽ cần phải tính toán việc sử dụng “bình thường” là gì (Sẽ có bao nhiều lần “ngồi” trên cái ghế đó hàng năm? Tay vịn thì sao?). Sau đó, để có thế testing bằng tay, bạn sẽ muốn có một cái máy tự động làm những điều đó.

### **Testing một mảnh của phần mềm**
Thực ra việc testing một mảnh của phần mềm rất giống với testing một thực thể. Điều khác biệt lớn đó là testing phần mềm thường nhấn mạnh vào các chi tiết việc thực hiện testing.

Ghi nhớ rằng testing phần mềm có 2 mặt trọng tâm:
- Testing thủ công và tự động (Manual vs. Automated Testing): Trong một thế giới lý tưởng, chúng ta có thể thích mọi thứ đều tự động, nhưng mức độ khả thi của nó thì hiếm lắm. Một số thứ đơn giản là sẽ hiệu quả hơn với testing thủ công vì những đặc tính của nó quá là cảm tính để một máy tính có thể kiểm tra được hiệu quả (ví dụ như những nội dung đại diện cho nội dung khiêu dâm ). Hơn nữa, trong khi một máy tính thường chỉ có thể xác định những vấn đề đã được dạy, việc quan sát của con người có thể tiết lộ ra những vấn đề mới chưa được kiểm tra một cách đặc biệt. Cả con người và máy tính định hình một phần thiết yếu trong quá trình testing.
- Testing hộp đen vs. Testing hộp trắng (Black Box Testing vs. White Box Testing): Sự phân biệt này dựa vào mức độ can thiệp vào phần mềm. Với testing hộp đen, ta chỉ được nhận các lỗi tiềm ẩn của phần mềm và test nó. Với hộp trắng testing, ta có thêm quyền can thiệp vào chương trình để test một số chức năng độc lập. Ta cũng có thể cho chạy tự động hộp đen mặc dù chắc chắn việc đó khó hơn nhiều.

:triangular_flag_on_post: Chúng ta hãy cùng tóm lược lại nhé. :triangular_flag_on_post:

**_Bước 1:_ Chúng ta đang sử dụng Black Box hay White Box testing?**
- Mặc dù câu hỏi này có thể bị hoãn lại tới các bước sau nhưng tôi thích loại bỏ chúng ra sớm hơn. Hãy chắc rằng bạn đang làm việc với black box hay white box testing, hoặc cả hai.

**_Bước 2:_ Ai sẽ sử dụng nó, tại sao?**
- Phần mềm thường có một hoặc nhiều người dùng chiến lược và những đặc tính được thiết kế theo họ. Ví dụ, nếu bạn được yêu cầu test phần mềm phụ huynh quản lý trên một trình duyệt web, người dùng chính của bạn bao gồm phụ huynh (người chặn) và trẻ em (người bị chặn). Bạn có thể có “khách” (người mà không nên bị chặn hay được chặn).

**_Bước 3:_ Những trường hợp sử dụng?**
- Trong trường hợp phần mềm chặn trẻ em, use cases của phụ huynh bao gồm cài đặt phần mềm, cập nhật điều khiển, xóa điều khiển và tất nhiên là việc sử dụng internet riêng tư của họ. Đối với trẻ em, uses case bao gồm truy cập vào những nội dung hợp lệ cũng như “không hợp lệ”.
- Hãy nhớ rằng không phải một điều kỳ diệu nào đó mà bạn quyết định các use cases, mà đó là một cuộc đối thoại giữa bạn với người phỏng vấn.

**_Bước 4:_ Phạm vi sử dụng?**
- Bây giờ chúng ta đã có định nghĩa mơ hồ về use cases, ta cần phải tìm ra ý nghĩa của nó. 1 website bị chặn là như thế nào? Có phải chỉ trang “không hợp lệ” bị chặn, hay là cả website? Có phải thiết bị được cho là “học” như thế nào là nội dung xấu, hay nó chỉ dựa trên danh sách trắng hoặc đen? Nếu nó được học những nội dung không phù hợp, mức độ không phù hợp tiêu cực hay tích cực như thế nào là có thể chấp nhận?

**_Bước 5:_ Những điều kiện thất bại, xảy ra lỗi**
- Khi một phần mềm hỏng – một điều không tránh khỏi – lúc bấy giờ trông nó sẽ như thế nào? Rõ ràng, lỗi của phần mềm không nào phá hỏng cả máy tính. Thay vào đó, nó nên chỉ là cho phép một trang bị chặn, hoặc chặn một trang được phép. Trong trường hợp sau này, bạn có thể sẽ muốn bàn bạc về khả năng ghi đè với một mật khẩu từ phụ huynh.

**_Bước 6:_ Test cases là gì? Bạn thực hiện việc testing như thế nào?**
- Đây là nơi mà sự phân biệt giữa testing thủ công và tự động, giữa black box và white box testing thực sự xảy ra.

:point_right:  Bước 3 và bước 4 đã gần như định nghĩa use cases. Ở bước 6, ta đã định nghĩa xa hơn và tranh luận làm thế nào để thực hiện testing. Bạn đang testing những tình huống cụ thể nào? Những bước nào trong đây có thể tự động hóa? Bước nào cần sự can thiệp của con người?

:point_right:  Hãy nhớ rằng trong khi tự động hóa cho phép bạn làm rất nhiều việc, nó vẫn có một số hạn chế nhất định. Testing thủ công thường trở thành 1 phần trong phương pháp test.

:point_right:  Khi bạn đi qua cái danh sách này, đừng kể liền một hơi về những viễn cảnh bạn có thể nghĩ ra. Nó thật sự là không có tổ chức và chắc hẳn bạn sẽ bỏ lỡ những hạng mục quan trọng. Thay vào đó, tiếp cận nó với một phương thức có tổ chức. Chia phần testing của bạn ra các thành phần chính và bắt đầu từ đó. Điều đó sẽ không chỉ giúp bạn có một danh sách test cases hoàn thiện hơn mà nó còn thể hiện bạn là một người có tổ chức, một người làm việc có phương pháp!

### **Kiểm tra một chức năng (Testing a Function)**
Trong nhiều trường hợp, testing một chức năng là kiểu testing dễ dàng nhất. Cuộc đối thoại thường sẽ ngắn gọn hơn và ít mơ hồ vì đối với việc testing thường bị hạn chế về mặt xác thực input và output.

Tuy nhiên, đừng bỏ lơ giá trị của một số cuộc đối thoại với người phỏng vấn bạn. Bạn nên tranh luận bất kỳ tình huống giả định nào với họ, đặc biệt là bạn nên xử lý những tình huống cụ thể với sự tôn trọng.

Giả sử rằng bạn được yêu cầu viết code để test sort(int[] array) tức sắp xếp một mảng các số nguyên. Bạn có thể thực hiện theo dưới các bước sau.

**_Bước 1:_** Định nghĩa test case
Thông thường, bạn nên nghĩ về những loại test case sau:
- _Case thông thường:_ Nó có tạo ra output đúng với các input đưa vào không? Hãy nhớ rằng có những vấn đề tiềm ẩn. Ví dụ, vì việc sắp xếp thường yêu cầu một số phân đoạn, có lý khi mà một thuật toán có thể hỏng vì các mảng có một số lẻ các phần tử, từ đó nó không thể được phân chia đều nhau. Test case của bạn nên liệt kê cả 2 ví dụ.
- _Case khó đỡ (The extremes):_ Chuyện gì sẽ xảy ra khi bạn nhận một cái mảng rỗng? hay một cái rất nhỏ (mảng 1 phần tử)? hoặc là một cái rất lớn?
- _Input rỗng và “không hợp lệ” (Nulls and “illegal” input):_ Thật đáng giá để nghĩ về việc code sẽ thể hiện như thế nào khi được nhận một input không hợp lệ. Ví dụ, nếu bạn đang test một chức năng để tạo một dãy n số Fibonacci, test case của bạn chắc hẳn nên chứa cả trường hợp n là số âm.
- _Input “lạ” (Strange input):_ Một dạng input thứ tư đôi lúc xuất hiện: strange input. Chuyện gì xảy ra khi bạn nhận một mảng đã được sắp xếp? hay một mảng được sắp với chiều ngược lại?
Tạo ra những test này đòi hỏi kiến thức về các chức năng bạn đang viết. Nếu bạn còn chưa rõ về những ràng buộc, bạn sẽ cần phải hỏi người phỏng vấn bạn đầu tiên. 

**_Bước 2:_** Định nghĩa kết quả mong đợi
- Đôi lúc kết quả mong đợi thật là rõ ràng: một output đúng! Tuy nhiên, trong vài trường hợp bạn có thể muốn xác thực một số khía cạnh khác. Ví dụ, nếu phương thức sắp xếp trả về một bản copy của mảng thì bạn chắc hẳn phải xác thực rằng mảng nguyên thủy chưa bị tác động vào.

**_Bước 3:_** Viết code test
Một khi bạn đã có test case và định nghĩa kết quả thì việc viết code để bắt đầu việc test nên được bắt tay vào luôn. Code của bạn có thể sẽ như thế này:

```
	void testAddThreeSorted()
	{
		MyList list = new MyList();
		list.addThreeSorted(3,1,2); // Adds 3 items in sorted order
		assertEquals(list.getElement(0),1);
		assertEquals(list.getElement(1),2);
		assertEquals(list.getElement(2),3);
	}
```

### **Câu hỏi sửa chữa (Troubleshooting Questions)**
Một dạng câu hỏi cuối là hãy giải thích bạn sẽ debug hay sửa chữa một vấn đề đang hiện hữu như thế nào. Nhiều ứng viên thường lẩn tránh câu hỏi như đưa ra những câu trả lời không thực tế như “cài đặt lại phần mềm”. Bạn có thể tiếp cận những câu hỏi như thế này bằng một phương pháp có cấu trúc như mọi thứ khác thôi.
Hãy cùng bước qua bấn đề này với một ví dụ: Bạn đang làm việc cho Google Chrome và khi bạn nhận được một bug report: Chrome bị crash khi khởi động. Bạn sẽ làm gì?
Cài đặt lại browser có thể giải quyết vấn đề của người dùng, nhưng nó sẽ không giúp những người dùng khác có cùng vấn đề. Mục tiêu của bạn là hiểu rõ những gì đang thực sự xảy ra và như vậy các developer có thể sửa chữa nó.

**_Bước 1:_ Hiểu về những gì đang xảy ra**
- Điều đầu tiên bạn nên làm là hỏi để hiểu rõ về tình hình nhiều nhất có thể.
  - Người dùng đã phải trải qua vấn đề này bao lâu rồi?
  - Phiên bản browser là đang dùng là gì? Hệ điều hành đang dùng?
  - Lỗi này có xảy ra một cách hệ thống hay không, hoặc tần suất xảy ra lỗi? Nó xảy ra khi nào?
  - Có error report hiện ra không?

**_Bước 2:_ Chia nhỏ vấn đề**
- Bây giờ bạn đã hiểu chi tiết về những gì đang xảy ra, bạn muốn chia vấn đề ra thành các thành phần nhỏ có thể test được. Trong trường hợp này , bạn có thể tưởng tượng dòng chảy của nó như sau:

1. Đi đến cửa số Windows
2. Click biểu tượng Chrome
3. Browser instance starts
4. Browser loads settings
5. Browser issues HTTP request for homepage
6. Browser gets HTTP response
7. Browser parses webpage
8. Browser displays content

- Tại một số thời điểm trong quá trình này, một cái gì đó gây ra lỗi và nó gây ra hiện tượng crash cho browser. Một tester giỏi sẽ lặp lại những tác nhân này và chẩn đoán vấn đề.

**_Bước 3:_ Tạo ra các test cụ thể và dễ quản lý**
- Mỗi thành phần trên nên có một hướng dẫn thực tế - điều mà bạn có thể yêu cầu người dùng làm, hoặc những điều mà bạn có thể tự làm (như là lặp lại các bước trên máy móc của bạn). Trong thế giới thực, bạn sẽ thỏa thuận với khách hàng và bạn không thể đưa cho họ các hướng dẫn mà họ không thể hoặc không làm.


___
===== END PART 1 =====
___

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

**Kiểm thử loại #2: Kiểm thử chung**

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

===== THE END =====
