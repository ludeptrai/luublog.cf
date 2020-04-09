---
title: Neural Network là gì?, Activation function là gì?
author: admin
layout: post
date: 2020-03-31T08:44:51+00:00
excerpt: 'Activation functions trong Neural Network là một thành phần quan trọng trong Deep Learning. Các  Activation function xác định đầu ra của một mô hình Deep Learning, độ chính xác cũng như hiệu quả tính toán của việc training model '
url: /posts/neural-network-and-activation-function/
thumb_img_path: /images/uploads/2020/04/ai-paper-880-x-440-article-.jpg
categories:
  - 'AI - my works'
  - Data Science
tags:
  - activation function
  - deep learning
  - machine learning
  - neural network

---
Activation functions trong Neural Network là một thành phần quan trọng trong Deep Learning. Các Activation function xác định đầu ra của một mô hình Deep Learning, độ chính xác cũng như hiệu quả tính toán của việc training model &#8211; thứ quyết dịnh thành công hay thất bại của một hệ thống Neural Network. Activation function cũng có ảnh hưởng lớn đến khả năng hội tụ và tốc độ hội tụ của mạng nơ-ron, hoặc trong một số trường hợp, các Activation function có thể ngăn các mạng thần kinh hội tụ ngay từ đầu.

Bài viết này là một phần của MissingLink’s&nbsp;<a rel="noreferrer noopener" href="https://missinglink.ai/guides/neural-network-concepts/" target="_blank">Neural Network Guide</a>, tập trung vào giải thích thực tế về các khái niệm và quy trình, bỏ qua nền tảng lý thuyết. Mình sẽ cung giải thích tổng quan về chủ đề này, các mẹo để chọn Activation function phù hợp.

## Tổng quan:

  * [Neural Network Activation Function là gì?][1]
  * [Vai trò của activation functions trong một Model Neural Network][2] 

## Neural Network Activation Function là gì?

Activation functions là các phương trình toán học xác định đầu ra của mạng nơ ron. Hàm này được gắn vào mỗi nơ-ron trong mạng và xác định xem nó có nên được kích hoạt hay không, dựa trên việc dữ liệu đầu vào có phù hợp với dự đoán mô hình hay không. Activation functions cũng giúp chuẩn hóa đầu ra của mỗi nơ ron đến phạm vi từ 1 đến 0 hoặc giữa -1 và 1.

Một khía cạnh nữa của activation functions đó là chúng phải có hiệu quả tính toán vì chúng được tính toán qua hàng ngàn hoặc thậm chí hàng triệu tế bào thần kinh cho mỗi mẫu dữ liệu. Các mạng nơ ron hiện đại sử dụng một kỹ thuật gọi là **backpropagation** để huấn luyện mô hình.

Nhu cầu về tốc độ tính toán đã dẫn đến sự phát triển của các chức năng mới như ReLu và Swish

<div class="wp-block-image">
  <figure class="aligncenter"><img src="https://missinglink.ai/wp-content/uploads/2018/11/graph1.png" alt="Two Common Activation Functions: Sigmoid and TanH" class="wp-image-947" /></figure>
</div>

### Artificial Neural Networks và Deep Neural Networks là gì?

Artificial Neural Networks&nbsp;(ANN) bao gồm một số lượng lớn các thành phầnđược gọi là nơ-ron, mỗi nơ-ron đưa ra quyết định đơn giản. Cùng với nhau, các nơ-ron có thể cung cấp câu trả lời chính xác cho một số vấn đề phức tạp, chẳng hạn như xử lý ngôn ngữ tự nhiên, thị giác máy tính và AI.

Một neural network cạn (“shallow”), có nghĩa là nó có một lớp nơ-ron đầu vào, chỉ có một “hidden layer” xử lý các inputs, và một lớp đầu ra cung cấp đầu ra cuối cùng của mô hình. Deep Neural Network (DNN) thường có từ 2-8 layer. Nghiên cứu từ&nbsp;[Goodfellow, Bengio and Courville][3]&nbsp;và những chuyên gia khác khuyên rằng độ chính xác của một neural networks tăng dần theo số hidden layers.<figure class="wp-block-image">

![non-deep feedforward neural network][4]</figure> 

### &#8220;Non-deep&#8221; feedforward neural network<figure class="wp-block-image">

![Deep neural network][5]</figure> 

### Deep neural network

<hr class="wp-block-separator" />

## Vai trò của Activation Function trong một Model Neural Network

Trong một mạng nơ-ron, các dữ liệu đầu vào (inputs), được đưa vào các nơ-ron trong lớp input. Mỗi nơ-ron có một trọng số và nhân số đầu vào với trọng số cho ra đầu ra của nơ-ron, sau đó được chuyển sang lớp tiếp theo.

Hàm kích hoạt là một &#8220;cổng&#8221; toán học với input đi vào và output của nó đi vào nơ ron tiếp theo. Nó có thể hiểu đơn giản như là một công tắc bật và tắt đầu ra của nơ-ron, dựa trên quy luật nào đó. Hoặc nó có thể là một phép biến đổi ánh xạ các tín hiệu đầu vào thành các tín hiệu đầu ra cần thiết cho mạng nơ ron hoạt động..

<div class="wp-block-image">
  <figure class="aligncenter"><img src="https://missinglink.ai/wp-content/uploads/2018/11/activationfunction-1.png" alt="Activation function input and output in neural networks" class="wp-image-950" /></figure>
</div>

Neural networks sử dụng các hàm kích hoạt phi tuyến tính, có thể giúp mạng tìm học từ những dữ liệu phức tạp, tính toán và hiểu được bài toán và đưa ra dự đoán chính xác.

**Quá trình cơ bản được thực hiện bởi một tế bào thần kinh trong mạng lưới thần kinh là:**

<div class="wp-block-image">
  <figure class="aligncenter"><img src="https://missinglink.ai/wp-content/uploads/2018/11/Basic-process-carried-out-by-a-neuron-in-a-neural-network.png" alt="Basic process carried out by a neuron in a neural network " class="wp-image-951" /></figure>
</div>

Trong [bài viết tiếp theo][6], mình sẽ đi vào các vấn đề sâu hơn liên quan đến activation function. 

Đọc bài viết tiếp theo: [Tất tần tật về Activation function trong Neural Network][7]

Nguồn: https://missinglink.ai/guides/neural-network-concepts/7-types-neural-network-activation-functions-right

 [1]: https://missinglink.ai/guides/neural-network-concepts/7-types-neural-network-activation-functions-right/#section1
 [2]: https://missinglink.ai/guides/neural-network-concepts/7-types-neural-network-activation-functions-right/#section2
 [3]: http://www.deeplearningbook.org/
 [4]: https://missinglink.ai/wp-content/uploads/2018/11/non-deep-feedforward-1.png
 [5]: https://missinglink.ai/wp-content/uploads/2018/11/deep-neural-network.png
 [6]: https://luublog97.cf/activation-function-trong-neural-network/
 [7]: https://luublog97.cf/activation-function-trong-neural-network