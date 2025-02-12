# Hướng dẫn khai thác lỗ hổng XSS với Phantom Script #

## 1 Giới thiệu về Phantom Script
- Phantom Script là một thử thách web đơn giản, giúp người chơi học về Cross-Site Scripting (XSS) thông qua trải nghiệm thực tế. Khi thực hiện thử thách này, học viên sẽ được:
  - Hiểu cách một ứng dụng web có thể bị tấn công thông qua XSS.
  - Biết cách nhận diện mã nguồn bị lỗi.
  - Biết cách khai thác và thực hành các payload XSS khác nhau.
 
## 2 Tìm hiểu giao diện bài tập
Khi truy cập vào thử thách, chúng ta sẽ thấy giao diện gồm 3 phần chính:
  - Web App – Mô phỏng một trang web có chức năng tìm kiếm.
  - Vulnerable Code – Hiển thị đoạn mã dễ bị tấn công XSS.
  - Documentation – Cung cấp hướng dẫn về cách khai thác.
![image](https://github.com/user-attachments/assets/8afdc4c2-08e2-4a7b-9a53-913b48b0498a)

Khi nhập nội dung vào ô tìm kiếm, phần Vulnerable Code sẽ cập nhật, giúp chúng ta quan sát cách dữ liệu được xử lý.

## 3 Thực hành khai thác XSS
### Bước 1: Kiểm tra đầu vào có bị lọc hay không
Trước tiên, chúng ta thử nhập một đoạn HTML cơ bản vào ô tìm kiếm để kiểm tra xem ứng dụng có xử lý thẻ HTML không:

``` <b>Test</b>```

Do format kết quả trả về là in đậm nên chưa hiển thị rõ kết quả cho nên hãy thử payload bên dưới. 

![image](https://github.com/user-attachments/assets/aa6b89c4-5f84-47f9-b805-e48d29dcc780)


Nếu kết quả hiển thị chữ Test được in đậm, nghĩa là ứng dụng không chặn thẻ HTML. Điều này là dấu hiệu cho thấy trang web có thể bị tấn công XSS.

Hoặc chúng ta chèn 

```<i>test</i>```

![image](https://github.com/user-attachments/assets/0c425403-7063-4747-9ada-25be6e36c3bd)

Nếu 2 kết quả hiển thị chữ Test được in đậm, in nghiêng, nghĩa là ứng dụng không chặn thẻ HTML. Điều này là dấu hiệu cho thấy trang web có thể bị tấn công XSS.

### Bước 2: Thử chèn JavaScript đơn giản

Bây giờ, chúng ta sẽ thử chèn một đoạn script đơn giản để kiểm tra xem JavaScript có thể thực thi hay không:

``` <script>alert('XSS')</script> ```

Nếu một hộp thoại (alert box) hiện lên với nội dung "XSS", điều đó có nghĩa là trang web dễ bị tấn công XSS. (Có thể bị chặn **<script>**)

### Bước 3: Sử dụng payload dựa trên thuộc tính HTML

Một số trang web chặn thẻ ```<script>```, vì vậy chúng ta có thể thử một cách khác, chẳng hạn như sử dụng sự kiện **onerror**:

```<img src=x onerror="alert(1)">```

Khi trình duyệt tải ảnh với **src=x **(không tồn tại), sự kiện onerror sẽ kích hoạt và thực thi đoạn mã **alert(1).**

![image](https://github.com/user-attachments/assets/dd26565a-199d-4fcd-a627-4e61b5f2be97)

Nếu một hộp thoại (alert box) hiện lên với nội dung "1", điều đó có nghĩa là trang web dễ bị tấn công XSS.

### Bước 4: Tìm kiếm cách khai thác sâu hơn

Nếu trang web vẫn lọc các payload trên, ta có thể thử một số cách khác, như:

```<svg onload=alert(1)>```

Hoặc:

```<iframe src="javascript:alert(1)"></iframe>```

![image](https://github.com/user-attachments/assets/4daa61a9-fbca-4383-a2e4-113a7e46de3a)

Tùy vào cách trang web xử lý đầu vào, chúng ta có thể thử nhiều phương pháp khác nhau.

## 4. Nhận Flag và hoàn thành thử thách

Khi chúng ta tìm ra payload phù hợp và kích hoạt được alert box, sau một thời gian ngắn, flag sẽ xuất hiện trên màn hình như hình dưới:

![image](https://github.com/user-attachments/assets/33c9dae6-7202-46af-b3db-285619e739fc)

Xin chúc mừng! Bạn đã hoàn thành thử thách và học được cách khai thác Cross-Site Scripting (XSS)! 🎉

## 5. Kết luận

- XSS là một lỗ hổng phổ biến trong bảo mật web, có thể gây nguy hiểm nếu không được kiểm soát chặt chẽ.
- Học cách khai thác XSS giúp chúng ta hiểu rõ hơn về cách phòng chống nó.
- Luôn kiểm tra và lọc đầu vào của người dùng để ngăn chặn các cuộc tấn công XSS trong thực tế.
