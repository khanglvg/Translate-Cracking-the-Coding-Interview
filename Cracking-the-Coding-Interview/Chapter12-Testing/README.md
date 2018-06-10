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
  Chỉnh sửa thêm 1 chỗ nữa là sử dụng `%u` thay cho `%d`, ta sẽ in ra kiểu `unsigned int`:
  
  ```
  unsigned int i;
  for (i = 100; i > 0; --i)
    printf("%u\n", i);
  ```
  Vậy là đoạn code sẽ in ra danh sách các số từ 100 về 1 theo đúng mong muốn.
  
  
