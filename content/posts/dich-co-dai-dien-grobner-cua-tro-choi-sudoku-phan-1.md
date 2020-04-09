---
title: '[Dịch] Cơ sở đại diện Gröbner của trò chơi Sudoku (Phần 1)'
author: Duy Lưu
layout: post
date: 2017-10-07T15:58:01+00:00
url: /posts/dich-co-dai-dien-grobner-cua-tro-choi-sudoku-phan-1/
featured_image: /images/uploads/2020/04/tet-holiday-2016-slider-1024x533-1-768x400.png
categories:
  - Chưa được phân loại

---
<p style="text-align: center;">
  <strong>Tác giả:</strong><br /> Elizabeth Arnold, Stephen Lucas, and Laura Taalman
</p>

<p style="text-align: center;">
  Department of Mathematics and Statistics
</p>

<p style="text-align: center;">
  Trường đại học James Madison, Harrisonburg VA 22807<br /> 〈26-03-2009〉
</p>

## 1. Giới thiệu

Sudoku là một bảng gồm 9&#215;9 ô vuông Latin được chia thành các khối 3&#215;3. Đặc biệt, 81 ô vuông của một sudoku được điền vào bởi các con số từ 1-9 theo quy luật: không có hàng, cột hay khối 3&#215;3 được chia sẵn nào chứa các số trùng nhau. Chúng ta sẽ xem các hàng, cột hay khối này như là các khu vực.

Một câu đố Sudoku là một Sudoku bị lược bớt các con số với mục đích duy nhất là người chơi phải hoàn thành phần còn lại của bảng. Chẳng hạn, câu đố Sudoku bên dưới là một trong rất nhiều câu đố chỉ có một lời giải duy nhất, chính là Sudoku bên phải.

 <img class="size-medium wp-image-145 alignnone" src="http://luublog.cf/wp-content/uploads/2017/10/s-300x300.jpg" alt="" width="300" height="300" /><img class="size-medium wp-image-144 alignnone" src="http://luublog.cf/wp-content/uploads/2017/10/ss-297x300.jpg" alt="" width="297" height="300" />

<p style="text-align: center;">
  <strong>Hình 1</strong>: Câu đố Sudoku và lời giải
</p>

&nbsp;

Số lượng các Sudoku khả thi lớn hơn cả số ngôi sao mà ta thấy được trong vũ trụ. Felgenhauer và Jarvis đã cho thấy rằng có 6.670.903.752.021.072.936.960 (khoảng 6 ngàn 671 tỷ tỷ) Sudoku khác nhau. Kể cả khi chúng ta muốn đếm số Sudoku chỉ khác nhau về bản chất, không tương đương, Russell và Jarvis cũng đã cho thấy con số này rất lớn, chính xác là 5.472.730.538.

Để dễ hình dung, phần này sẽ thuận tiện hơn cho chúng ta khi nghiên cứu một phiên bản đơn giản hơn của Sudoku, được gọi là Shidoku. Một Shidoku, cũng tương tự như Sudoku, là một bảng gồm 4&#215;4 ô vuông có các khu vực (hàng, cột, các khối 2&#215;2 tương ứng được biểu thị) mà mỗi khu vực đều chứa các số nguyên từ 1-4 đúng 1 lần. Trong vũ trụ nhỏ hơn này, không khó để chúng ta tìm ra rằng có 288 Shidoku khác nhau tồn tại. Một trong những thứ mà phần này ta thảo luận đến chính là việc sử dụng Cơ sở Gröbner như là một phương án thay thế cho việc đếm số Sudoku và Shidoku.

Một câu đố Shidoku là một Shidoku được lược bớt các con số, với mục đích là người chơi phải hoàn thành phần còn lại của bảng. Ví dụ, hình bên trái là một câu đố Shidoku, chỉ có duy nhất một lời giải (Shidoku ở giữa). Shidoku phía bên phải là kí hiệu của từng ô vuông ta sẽ dùng để gọi các ô của Shidoku từ trang này trở đi.

 <img class="size-full wp-image-146 alignnone" src="http://luublog.cf/wp-content/uploads/2017/10/sh.jpg" alt="" width="195" height="196" /><img class="size-full wp-image-148 alignnone" src="http://luublog.cf/wp-content/uploads/2017/10/shs.jpg" alt="" width="195" height="196" /> <img class="size-full wp-image-147 alignnone" src="http://luublog.cf/wp-content/uploads/2017/10/sha.jpg" alt="" width="195" height="196" />

<p style="text-align: center;">
  <strong>Hình 2</strong>: Câu đố Shidoku, lời giải, và kí hiệu
</p>

Có rất nhiều thuật toán khác nhau để giải Shidoku đã được phát triển và cũng rất nhiều chương trình máy tính đã được viết ra bằng cách sử dụng những thuật toán này để giải, tạo và đánh giá độ khó của các câu đố Sudoku. Trang web Sudopedia là một nguồn tài nguyên tuyệt vời với tất cả những thứ liên quan đến Sudoku, và còn rất nhiều thuật toán với những độ tinh tế khác nhau. Tuy nhiên, trong bài này, chúng ta sẽ không quan tâm về những công nghệ để giải đố, mà là những cấu trúc vốn có của Shidoku và Sudoku.

Theo đó, chúng ta sẽ phát triển theo 3 hướng khác nhau của một Shidoku bằng một hệ thống các phương trình đa thức. Mặt khác, ta sẽ làm rõ bằng cách nào mà một cơ sở Gröbner có thể được sử dụng để trình bày các ràng buộc. Cơ sở  đại diện Gröbner có thể được dùng để tìm cách giải hoặc đếm số bảng.

mời xem tiếp [Dịch] Cơ sở đại diện Gröbner của trò chơi Sudoku (Phần 2)