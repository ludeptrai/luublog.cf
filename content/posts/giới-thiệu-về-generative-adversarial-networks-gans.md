---
title: Giới thiệu về Generative Adversarial Networks (GANs)
date: 2020-09-01T07:59:51.344Z
thumb_img_path: /images/gan-–-ai-generująca-rzeczywistość-1024x536.png
excerpt: GANs  là một thuật toán học không giám sát (Unsupersived Learning) giải
  quyết các bài toán như Image Super Resolution, Image Translation,...
canonical_url: /images/gan-–-ai-generująca-rzeczywistość-1024x536.png
layout: post
---
<!--StartFragment-->

Generative Adversarial Networks, hay GANs, là một cách tiếp cận generator model (mô hình tạo ra dữ liệu mới) bằng các phương pháp deep learning, ví dụ như convolutional neural networks.

Generative modeling là một bài toán học không giám sát trong machine learning liên quan đến việc tự động tìm ra và học những thói quen hoặc sự lặp lại trong dữ liệu input từ đó mô hình có thể tạo ra những dữ liệu mới hợp lý với những quy tắc trong tập dữ liệu gốc.

GANs là một cách thông minh để train một generative model bằng việc đóng khung các vấn đề thành một bài toán supervised learning với 2 model con: generator model để tạo ra dữ liệu mới, và một discriminator model để xác định một dữ liệu là thật (từ dữ liệu gốc) hay giả (được tạo ra). Cả 2 models sẽ được train cùng nhau trong một hộp kín, cho tới khi discriminator không thể phân biệt được nữa, giữa thật và giả, có nghĩa là generator model đang tạo ra những dữ liệu gần như giống thật.

GAN là một lĩnh vực thú vị và thay đổi nhanh chóng, mang đến hứa hẹn về các mô hình tổng quát với khả năng tạo ra các ví dụ thực tế trên nhiều lĩnh vực, đặc biệt nhất là trong các nhiệm vụ dịch từ ảnh sang ảnh như chuyển đổi ảnh từ mùa hè sang mùa đông hoặc ngày sang đêm và tạo ra các bức ảnh chân thực về những đồ vật, cảnh vật và con người mà ngay cả con người cũng không thể biết được là giả.

Trong bài đăng này, bạn sẽ khám phá phần giới thiệu cơ bản về Generative Adversarial Networks, hay GANs.

Những kiến thức trong bài:

* Chỉ định GANs, bao gồm supervised và unsupervised learning, mô hình tách rời và generative model.
* GANs là một kiến trúc sử dụng để training một generative model bằng cách coi một bài toán unsupervised như một bài toán supervised và sử dụng cả generative model và mô hình rời rạc, cụ thể hơn, bài viết sẽ trình bày.
* GANs cho ta một cách thức để nâng cao độ tinh vi cho dữ liệu nhất định và một phương án cho những bài toán yêu cầu một giải pháp chung, như bài toán chuyển đổi ảnh>ảnh.

## Tổng quan

Bài viết này được chia làm 3 phần

1. Generative Models là gì?
2. Generative Adversarial Networks là gì?
3. Tại sao Generative Adversarial Networks?

## Generative Models là gì?

Trong phần này, chúng ta sẽ xem xét ý tưởng về generative models, vượt qua các mô hình học tập có giám sát và không giám sát và mô hình rời rạc so với mô hình tổng thể.

### Supervised và Unsupervised Learning

Một vấn đề học máy điển hình liên quan đến việc sử dụng một mô hình để đưa ra dự đoán, ví dụ như mô hình **dự đoán**.

Mô hình này yêu cầu một tập dữ liệu training được sử dụng để train một model, bao gồm nhiều dữ liệu, được gọi là một mẫu, mỗi điểm dữ liệu có các biến đầu vào (X) và label lớp đầu ra (y). Một model được train bằng cách đưa ra các dữ liệu input, để nó dự đoán đầu ra và điều chỉnh model để làm cho đầu ra giống với đầu ra mong đợi hơn.

> In the predictive or supervised learning approach, the goal is to learn a mapping from inputs x to outputs y, given a labeled set of input-output pairs …

— Page 2, [Machine Learning: A Probabilistic Perspective](https://amzn.to/2HV6cYx), 2012.

Việc hiệu chỉnh mô hình này thường được gọi là một hình thức học tập có giám sát, hay supervised learning.

![Example of Supervised Learning](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2019/04/Example-of-Supervised-Learning.png)

Ví dụ về các bài toán supervised learning bao gồm phân loại và hồi quy, và các ví dụ về thuật toán supervised learning bao gồm hồi quy logistic và random forrest.

Có một mô hình học tập khác, trong đó mô hình chỉ được cung cấp các input (X) và bài toán không có bất kỳ output nào (y).

Model này được xây dựng bằng cách trích xuất hoặc tóm tắt các đặc điểm trên tập dữ liệu input. Không có sự điều chỉnh model, vì model này không dự đoán bất cứ điều gì.

> The second main type of machine learning is the descriptive or unsupervised learning approach. Here we are only given inputs, and the goal is to find “interesting patterns” in the data. \[…] This is a much less well-defined problem, since we are not told what kinds of patterns to look for, and there is no obvious error metric to use (unlike supervised learning, where we can compare our prediction of y for a given x to the observed value).

— Page 2, [Machine Learning: A Probabilistic Perspective](https://amzn.to/2HV6cYx), 2012.

![Example of Unsupervised Learning](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2019/04/Example-of-Unsupervised-Learning.png)

Ví dụ về các bài toán unsupervised learning bao gồm phân cụm và generative modeling, và ví dụ về các thuật toán học tập không giám sát là K-means và Generative Adversarial Networks

### Discriminative và Generative Modeling

Trong supervised learning, ta tạo ra một model để dự đoán một class label từ một biến đầu vào, bài toán dự đoán này được gọi là bài toán classification.

Classification cũng được gọi là discriminative modeling.

> … we use the training data to find a discriminant function f(x) that maps each x directly onto a class label, thereby combining the inference and decision stages into a single learning problem.

— Page 44, [Pattern Recognition and Machine Learning](https://amzn.to/2K3EcE3), 2006.

Điều này là do một model tách cách dữ liệu đầu vào thành các class; và phải quyết định1 điểm dữ liệu sẽ phải thuộc vào class nào.

![Example of Discriminative Modeling](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2019/04/Example-of-Discriminative-Modeling.png)

Discriminative Modeling

Mặt khác, unsupervised model tìm ra sự phân phối của các biến đầu vào có thể được sử dụng để tạo ra các dữ liệu mới trong phân phối đầu vào..

Và những model như vậy được gọi là [generative models](https://en.wikipedia.org/wiki/Generative_model).

![Example of Generative Modeling](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2019/04/Example-of-Generative-Modeling.png)

ví dụ, một biến dữ liệu có thể tuân theo một phân phối đã biết,chẳng hạn như phân phối Gaussian, hay phân phối hình chuông. Một generative model có thể tóm tắt đầy đủ phân phối dữ liệu này, và sau đó được sử dụng để tạo ra các biến mới phù hợp một cách hợp lý với phân phối của biến đầu vào.

> Approaches that explicitly or implicitly model the distribution of inputs as well as outputs are known as generative models, because by sampling from them it is possible to generate synthetic data points in the input space.

— Page 43, [Pattern Recognition and Machine Learning](https://amzn.to/2K3EcE3), 2006.

Trên thực tế, một mô hình generative tốt có thể tạo ra các dữ liệu mới không chỉ hợp lý mà còn khiến ta không thể phân biệt được với các dữ liệu thực tế.

### Ví dụ Generative Models

[Naive Bayes](https://machinelearningmastery.com/naive-bayes-for-machine-learning/) là một ví dụ về generative model nhưng thường được sử dụng làm discriminative model hơn.

Ví dụ, Naive Bayes hoạt động bằng cách tóm tắt phân phối xác suất của mỗi biến đầu vào và class output. Khi dự đoán được đưa ra, xác suất cho mỗi kết quả có thể xảy ra được tính theo mỗi biến, các xác suất này độc lập và được kết hợp, kết quả được dự đoán là kết quả có khả năng xảy ra nhất. Ngược lại, phân phối xác suất của mỗi biến đầu vào có thể được dùng để tạo ra các giá trị phù hợp (độc lập) mới.

Các ví dụ khác về mô hình tổng quát bao gồm Latent Dirichlet Allocation, hoặc LDA, và Gaussian Mixture Model GMM.

Deep learning cũng có thể được sử dụng như một generative models. Hai ví dụ phổ biến là Restricted Boltzmann Machine, hay RBM, và Deep Belief Network, hay DBN.

Hai ví dụ hiện đại về các mô hình deep learning generative modeling là Variational Autoencoder, hay VAE, và Generative Adversarial Network, hay GAN.

## Generative Adversarial Networks là gì?

Generative Adversarial Networks, hay GANs, là một deep-learning-based generative model.

Nói một cách tổng quát hơn, GAN là một kiến ​​trúc để huấn luyện một generative model và người ta thường sử dụng các mô hình deep learning trong kiến ​​trúc này

Kiến trúc GAN lần đầu tiên được mô tả trong bài báo năm 2014 bởi [Ian Goodfellow](https://www.iangoodfellow.com/), et al. với tiêu đề “[Generative Adversarial Networks](https://arxiv.org/abs/1406.2661).”

Một approach chuẩn khác được gọi là Deep Convolutional Generative Adversarial Networks, hay DCGAN, ổn định hơn, đã được công bố sau đó bởi [Alec Radford](https://github.com/Newmu), et al. trong 1 paper năm 2015 gọi là “[Unsupervised Representation Learning with Deep Convolutional Generative Adversarial Networks](https://arxiv.org/abs/1511.06434)“.

> Most GANs today are at least loosely based on the DCGAN architecture …

— [NIPS 2016 Tutorial: Generative Adversarial Networks](https://arxiv.org/abs/1701.00160), 2016.

Kiến trúc mô hình GAN liên quan đến hai mô hình con: một *generator model* để sản xuất dữ liệu mới và một *discriminator model* để phân lớp dữ liệu vừa được tạo ra là dữ liệu gốc hay dữ liệu giả (fake)

* **Generator**. để sản xuất dữ liệu mới
* **Discriminator**. phân lớp dữ liệu vừa được tạo ra là dữ liệu gốc (*from the domain*) hay dữ liệu giả (*generated*).

> Generative adversarial networks are based on a game theoretic scenario in which the generator network must compete against an adversary. The generator network directly produces samples. Its adversary, the discriminator network, attempts to distinguish between samples drawn from the training data and samples drawn from the generator.

— Page 699, [Deep Learning](https://amzn.to/2YuwVjL), 2016.

### The Generator Model (Mô hình sản xuất)

Generator model nhận input là một vector ngẫu nhiên có độ dài cố định và tạo ra một điểm dữ liệu mới

Vectơ được lấy ngẫu nhiên từ phân bố Gaussian, và được đưa vào quá trình sản xuất. Sau khi training, các điểm trong không gian vectơ nhiều chiều này sẽ tương ứng với các điểm trong bài toán, tạo thành một biểu diễn nén của phân phối dữ liệu.

Không gian vectơ này được gọi là không gian tiềm ẩn, hoặc không gian vectơ bao gồm các biến tiềm ẩn. Biến tiềm ẩn, hoặc biến ẩn, là những biến quan trọng đối nhưng không thể quan sát trực tiếp.

> A latent variable is a random variable that we cannot observe directly.

— Page 67, [Deep Learning](https://amzn.to/2YuwVjL), 2016.

Chúng tôi thường đề cập đến các biến tiềm ẩn, hoặc không gian tiềm ẩn, như một phép chiếu hoặc nén phân phối dữ liệu. Có nghĩa là, một không gian tiềm ẩn thể hiện cách thức dữ liệu thô được quan sát, chẳng hạn như phân phối dữ liệu đầu vào. Trong trường hợp GAN, generator model biểu diễn các điểm trong không gian tiềm ẩn, sao cho các điểm mới được vẽ từ không gian tiềm có thể được đưa vào generator model và tiếp tục được sử dụng để tạo ra các điểm dữ liệu mới

> Machine-learning models can learn the statistical latent space of images, music, and stories, and they can then sample from this space, creating new artworks with characteristics similar to those the model has seen in its training data.

— Page 270, [Deep Learning with Python](https://amzn.to/2U2bHuP), 2017.

Sau khi training, the generator model được lưu lại và sử dụng để tạo ra các dữ liệu mới..![Example of the GAN Generator Model](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2019/04/Example-of-the-GAN-Generator-Model.png)

GAN Generator Model

### The Discriminator Model (Mô hình phân định)

Discriminator model lấy input là một điểm dữ liệu (real hoặc generated) và dự đoán một binary class label là real hay fake (generated).

Các điểm dữ liệu real lấy từ training dataset. Các điểm dữ liệu fake, hay generated lấy từ output của generator model.

Discriminator model là một classification model thông thường.

Sau quá trình training, discriminator model bị loại bỏ, vởi vì chúng ra chỉ quan tâm tới việc sản xuẩt dữ liệu.

> We propose that one way to build good image representations is by training Generative Adversarial Networks (GANs), and later reusing parts of the generator and discriminator networks as feature extractors for supervised tasks

— [Unsupervised Representation Learning with Deep Convolutional Generative Adversarial Networks](https://arxiv.org/abs/1511.06434), 2015.

![Example of the GAN Discriminator Model](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2019/04/Example-of-the-GAN-Discriminator-Model.png)

GAN Discriminator Model

### GANs: Trò chơi hai người

Generative modeling là một bài toán học không giám sát, như đã nói ở phần trước, although a clever property of the GAN architecture is that the training of the generative model is framed as a supervised learning problem.

The two models, the generator and discriminator, are trained together. The generator generates a batch of samples, and these, along with real examples from the domain, are provided to the discriminator and classified as real or fake.

Sau đó, Discriminator được cập nhật để có thể phân biệt thật và giả tốt hơn trong lần tiếp theo, và quan trọng hơn, Generator cũng được cập nhật dựa trên khả năng đánh lừa discriminator.

> We can think of the generator as being like a counterfeiter, trying to make fake money, and the discriminator as being like police, trying to allow legitimate money and catch counterfeit money. To succeed in this game, the counterfeiter must learn to make money that is indistinguishable from genuine money, and the generator network must learn to create samples that are drawn from the same distribution as the training data.

— [NIPS 2016 Tutorial: Generative Adversarial Networks](https://arxiv.org/abs/1701.00160), 2016.

Theo cách này, hai mô hình đang cạnh tranh với nhau, chúng đối nghịch nhau theo nghĩa lý thuyết trò chơi, và đang chơi trò chơi được gọi là [zero-sum game](https://en.wikipedia.org/wiki/Zero-sum_game).

> Because the GAN framework can naturally be analyzed with the tools of game theory, we call GANs “adversarial”.

— [NIPS 2016 Tutorial: Generative Adversarial Networks](https://arxiv.org/abs/1701.00160), 2016.

Trong trường hợp này, tổng bằng không có nghĩa là khi Discriminator xác định thành công mẫu thật và mẫu giả, nó được thưởng, hay không cần thay đổi các tham số model, trong khi generator bị phạt và phải cập nhật cho các tham số model.

Mặt khác, khi generator đánh lừa discriminator, nó sẽ được thưởng hoặc không cần thay đổi các thông số model, nhưng discriminator bị phạt và các thông số model của nó được cập nhật.

Trong trường hợp lý tưởng, generator luôn tạo ra các bản sao hoàn hảo từ input domain, và discriminator không thể phân biệt được và dự đoán “không chắc chắn ” (unsure) (ví dụ 50% thật 50% giả) trong mọi trường hợp. Đây chỉ là một ví dụ về một trường hợp lý tưởng hóa; chúng ta không cần phải đi đến điểm này để generator model trở nên hữu ích.![Example of the Generative Adversarial Network Model Architecture](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2019/04/Example-of-the-Generative-Adversarial-Network-Model-Architecture.png)

Generative Adversarial Network Model Architecture

> \[training] drives the discriminator to attempt to learn to correctly classify samples as real or fake. Simultaneously, the generator attempts to fool the classifier into believing its samples are real. At convergence, the generator’s samples are indistinguishable from real data, and the discriminator outputs 1/2 everywhere. The discriminator may then be discarded.

— Page 700, [Deep Learning](https://amzn.to/2YuwVjL), 2016.

### GANs và Convolutional Neural Networks

GANs thường làm việc tốt với dữ liệu hình ảnh và sử dụng Convolutional Neural Networks, hay CNNs làm generator và discriminator models.

Lý do là vì tác giả đã chú thích lĩnh vực computer vision và sử dụng CNNs cùng với dữ liệu ảnh, và vì những tiến bộ đáng kể đã được thấy trong những năm gần đây khi sử dụng CNN nói chung để đạt được kết quả state-of-the-art trên những bài toán computer vision tasks như object detection và face recognition.

Mô hình hóa dữ liệu hình ảnh có nghĩa là không gian tiềm ẩn – input của generator, cung cấp một bản mã hóa của ảnh được sử dụng để train model. Cũng có nghĩa là generator sẽ tạo ra hình ảnh mới, có thể được quan sát bởi người tạo ra model.

INhưng quan trọng hơn hết, khả năng đánh giá trực quan chất lượng của output được tạo ra, đã dẫn đến sự tập trung của các ứng dụng computer vision vào CNNs và tạo ra bước nhảy vọt về khả năng của GAN so với các mô hình chung khác, dựa trên học deep-learning hay bất cứ phương pháp nào.

### Conditional GANs

Một mở rộng quan trọng của GAN là nó được sử dụng để tạo ra output kèm theo điều kiện.

Generative model có thể được train để tạo ra dữ liệu mới, trong khi input, một vectơ ngẫu nhiên từ không gian tiềm ẩn, được điều kiện bởi những input bổ sung.

những input bổ sung này có thể là class label, chẳng hạn như nam hoặc nữ trong việc tạo ra các bức ảnh của người, hoặc một chữ số, trong trường hợp tạo ảnh của các chữ số viết tay.

> Generative adversarial nets can be extended to a conditional model if both the generator and discriminator are conditioned on some extra information y. y could be any kind of auxiliary information, such as class labels or data from other modalities. We can perform the conditioning by feeding y into the both the discriminator and generator as \[an] additional input layer.

— [Conditional Generative Adversarial Nets](https://arxiv.org/abs/1411.1784), 2014.

Discriminator model cũng được điều kiện hóa, có nghĩa là nó được cung cấp cả hình ảnh đầu vào là thật hay giả và input bổ sung. Trong trường hợp nhãn của một class là input điều kiện, discriminator sẽ mong đợi rằng input sẽ thuộc class đó, và tới lượt nó dạy cho generator cách tạo ra những dữ liệu cho class đó để đánh lừa discriminator.

Trong trường hợp này, conditional GAN có thể được sử dụng để sản xuất ra một kiểu dữ liệu nhất định.

Một bước xa hơn, GAN models có thể được quy định trên một kiểu dữ liệu, như là ảnh. Do đó, GAN có khả năng như như dịch văn bản sang hình ảnh hoặc dịch hình ảnh sang hình ảnh. Điều này cho phép một số ứng dụng ấn tượng hơn của GAN, chẳng hạn như chuyển kiểu, chỉnh màu ảnh, chuyển ảnh từ mùa hè sang mùa đông hoặc ngày sang đêm, v.v.

Trong trường hợp GAN có điều kiện để chuyển đổi hình ảnh sang hình ảnh, chẳng hạn như chuyển đổi từ ngày sang đêm, discriminator được cung cấp input là các dữ liệu của hình ảnh ban đêm thật và hình ảnh được tạo ra với các điều kiện từ hình ảnh ban ngày. Còn Generator được cung cấp input là một vectơ ngẫy nhiên từ không gian tiềm ẩn (có điều kiện) của ảnh ban ngày.![Example of a Conditional Generative Adversarial Network Model Architecture](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2019/04/Example-of-a-Conditional-Generative-Adversarial-Network-Model-Architecture.png)

Conditional Generative Adversarial Network Model Architecture

## Tại sao Generative Adversarial Networks?

Một trong nhiều tiến bộ lớn trong việc sử dụng các phương pháp deep learning trong các lĩnh vực như thị giác máy tính là một kỹ thuật được gọi là tăng cường dữ liệu: [data augmentation](https://machinelearningmastery.com/image-augmentation-deep-learning-keras/).

Data augmentation có thể khiến cho các mô hình hoạt động tốt hơn, vừa tăng hiệu quả của mô hình vừa mang lại hiệu ứng điều chỉnh, giảm lỗi. Nó hoạt động bằng cách tạo ra các dữ liệu mới, nhân tạo nhưng phù hợp dựa trên dữ liệu đầu vào mà mô hình được đào tạo.

Với dữ liệu hình ảnh, các kĩ thuật này có nguồn gốc liên quan đến việc cắt, lật, thu phóng và các biến đổi đơn giản khác của hình ảnh hiện có trong tập dữ liệu đào tạo.

Successful generative modeling provides an alternative and potentially more domain-specific approach for data augmentation. In fact, data augmentation is a simplified version of generative modeling, although it is rarely described this way.

> … enlarging the sample with latent (unobserved) data. This is called data augmentation. \[…] In other problems, the latent data are actual data that should have been observed but are missing.

— Page 276, [The Elements of Statistical Learning](https://amzn.to/2UcPeva), 2016.

Trong các lĩnh vực phức tạp hoặc các lĩnh vực có lượng dữ liệu hạn chế, generative model cung cấp một hướng đi hướng tới training nhiều hơn cho mô hình. GAN đã đạt được nhiều thành công trong trường hợp này trong các lĩnh vực như deep reinforcement learning

Có lẽ ứng dụng hấp dẫn nhất của GAN là trong GAN có điều kiện cho các tác vụ yêu cầu tạo ra các ví dụ mới. Đây ba ví dụ chính:

* **Image Super-Resolution**. Khả năng tạo các phiên bản hình ảnh đầu vào có độ phân giải cao.
* **Creating Art**. Khả năng tạo ra những hình ảnh, bản phác thảo, hội họa mới và nghệ thuật, v.v.
* **Image-to-Image Translation**. Khả năng biến đổi ảnh, chẳng hạn như ngày sang đêm, mùa hè sang mùa đông, v.v.

Có lẽ lý do thuyết phục nhất mà GAN ​​được nghiên cứu, phát triển và sử dụng rộng rãi là vì thành công của chúng. GAN đã có thể tạo ra những bức ảnh chân thực đến mức con người không thể biết rằng đó là những vật thể, cảnh vật và con người không tồn tại trong cuộc sống thực.

Kinh ngạc không phải là một tính từ đủ cho khả năng và thành công của chúng.![Example of the Progression in the Capabilities of GANs from 2014 to 2017](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2019/04/Example-of-the-Progression-in-the-Capabilities-of-GANs-from-2014-to-2017.png)

Ví dụ về sự tiến bộ trong khả năng của GANs From 2014 to 2017. Taken from [The Malicious Use of Artificial Intelligence: Forecasting, Prevention, and Mitigation](https://arxiv.org/abs/1802.07228), 2018.

### Posts

* [Best Resources for Getting Started With Generative Adversarial Networks (GANs)](https://machinelearningmastery.com/resources-for-getting-started-with-generative-adversarial-networks/)
* [18 Impressive Applications of Generative Adversarial Networks (GANs)](https://machinelearningmastery.com/impressive-applications-of-generative-adversarial-networks/)

### Books

* [Chapter 20. Deep Generative Models, Deep Learning](https://amzn.to/2YuwVjL), 2016.
* [Chapter 8. Generative Deep Learning, Deep Learning with Python](https://amzn.to/2U2bHuP), 2017.
* [Machine Learning: A Probabilistic Perspective](https://amzn.to/2HV6cYx), 2012.
* [Pattern Recognition and Machine Learning](https://amzn.to/2K3EcE3), 2006.
* [The Elements of Statistical Learning](https://amzn.to/2UcPeva), 2016.

### Papers

* [Generative Adversarial Networks](https://arxiv.org/abs/1406.2661), 2014.
* [Unsupervised Representation Learning with Deep Convolutional Generative Adversarial Networks](https://arxiv.org/abs/1701.00160), 2015.
* [NIPS 2016 Tutorial: Generative Adversarial Networks](https://arxiv.org/abs/1701.00160), 2016.
* [Conditional Generative Adversarial Nets](https://arxiv.org/abs/1411.1784), 2014.
* [The Malicious Use of Artificial Intelligence: Forecasting, Prevention, and Mitigation](https://arxiv.org/abs/1802.07228), 2018.

### Articles

* [Generative model, Wikipedia](https://en.wikipedia.org/wiki/Generative_model).
* [Latent Variable, Wikipedia](https://en.wikipedia.org/wiki/Latent_variable).
* [Generative Adversarial Network, Wikipedia](https://en.wikipedia.org/wiki/Generative_adversarial_network).

nguồn dịch:

https://machinelearningmastery.com/what-are-generative-adversarial-networks-gans/

Người dịch:

Lưu Phan

<!--EndFragment-->