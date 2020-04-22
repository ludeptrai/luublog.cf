---
title: 12 Thuật toán phân cụm (clustering) với python (Phần 1)
date: 2020-04-20T10:16:19.493Z
thumb_img_path: /images/clustering-algorithms.jpg
content_img_path: /images/clustering-algorithms.jpg
excerpt: Có rất nhiều thuật toán phân cụm để lựa chọn và không có thuật toán
  phân cụm tốt nhất cho tất cả các trường hợp. Chính vì thế, sẽ tốt hơn nếu ta
  khám phá một loạt các thuật toán phân cụm và điều chỉnh khác nhau cho mỗi
  thuật toán.
canonical_url: /images/clustering-algorithms.jpg
layout: post
---
Thuật toán phân cụm hay clustering là một bài toán học không giám sát.

Nó thường được sử dụng như một kỹ thuật phân tích dữ liệu để khám phá các đặc tính trong dữ liệu, chẳng hạn như các nhóm khách hàng dựa trên hành vi của họ.

Có rất nhiều thuật toán phân cụm để lựa chọn và không có thuật toán phân cụm tốt nhất cho tất cả các trường hợp. Chính vì thế, sẽ tốt hơn nếu ta khám phá một loạt các thuật toán phân cụm và điều chỉnh khác nhau cho mỗi thuật toán.

Trong hướng dẫn này, bạn sẽ khám phá cách điều chỉnh và sử dụng các thuật toán phân cụm hàng đầu trong python.

Sau khi hoàn thành hướng dẫn này, bạn sẽ biết:

*   Phân cụm là một bài toán học không giám sát trong việc tìm các cụm trong không gian của dữ liệu đầu vào.
*   Có nhiều thuật toán phân cụm khác nhau và không có phương pháp tốt nhất cho tất cả các bộ dữ liệu.
*   Cách triển khai, phù hợp và sử dụng các thuật toán phân cụm trong Python với thư viện máy học scikit-learn.

Let’s get started.

## Tổng quan:

Bài viết này được chia làm 2 phần:

1.  Bài toán phân cụm
2.  Các thuật toán phân cụm
3.  Các ví dụ
    1.  Library Installation
    2.  Clustering Dataset
    3.  Affinity Propagation
    4.  Agglomerative Clustering
    5.  BIRCH
    6.  DBSCAN **(Kết thúc phần 1)**
    7.  K-Means
    8.  Mini-Batch K-Means
    9.  Mean Shift
    10.  OPTICS
    11.  Spectral Clustering
    12.  Gaussian Mixture Model **(Kết thúc phần 2)**

## Bài toán phân cụm

Phân cụm hay clustering là một bài toán machine learning học không giám sát.

Nó liên quan đến việc tự động khám phá các cụm tự nhiên trong dữ liệu. Không giống như học có giám sát (như mô hình dự đoán), thuật toán phân cụm chỉ phân tích dữ liệu đầu vào và tìm các nhóm hoặc cụm tự nhiên trong không gian đặc trưng.

> Clustering techniques apply when there is no class to be predicted but rather when the instances are to be divided into natural groups.

— Trang 141, [Data Mining: Practical Machine Learning Tools and Techniques](https://amzn.to/2R0G3uG), 2016.

Một cụm thường là một khu vực có mật độ nơi các các điểm dữ liệu gần với một cụm hơn các cụm khác trong không gian dữ liệu. Cụm có thể có một trung tâm (tâm) là một điểm dữ liệu hoặc một điểm trong không gian dữ liệu và có thể có một ranh giới hoặc phạm vi nhất định.

> These clusters presumably reflect some mechanism at work in the domain from which instances are drawn, a mechanism that causes some instances to bear a stronger resemblance to each other than they do to the remaining instances.

— Trang 141-142, [Data Mining: Practical Machine Learning Tools and Techniques](https://amzn.to/2R0G3uG), 2016.

Phân cụm có giúp hoạt động phân tích dữ liệu để tìm hiểu thêm về một vấn đề, được gọi là khai phá dữ liệu.

Ví dụ:

*   Cây tiến hóa có thể được coi là kết quả của phân tích phân cụm thủ công.
*   Tách dữ liệu bình thường khỏi các ngoại lệ hoặc dị thường có thể được coi là một bài toán phân cụm.
*   Tách các cụm dựa trên đặc điểm tự nhiên của chúng là một bài toán phân cụm, được gọi là phân khúc thị trường.

Phân cụm cũng có thể được sử dụng như một phương pháp feature engineering, trong đó các điểm dữ liệu hiện có và mới có thể được ánh xạ và gắn nhãn là thuộc về một trong các cụm được xác định trong dữ liệu.

Đánh giá các cụm xác định là chủ quan và có thể cần một chuyên gia, mặc dù nhiều biện pháp định lượng cụ thể theo cụm tồn tại. Thông thường, các thuật toán phân cụm được so sánh về mặt học thuật trên các bộ dữ liệu tổng hợp với các cụm được xác định trước, và thuật toán sẽ tìm ra chúng.

> Clustering is an unsupervised learning technique, so it is hard to evaluate the quality of the output of any given method.

— Trang 534, [Machine Learning: A Probabilistic Perspective](https://amzn.to/2TwpXuC), 2012.

## Các thuật toán phân cụm

Có nhiều loại thuật toán phân cụm.

Nhiều thuật toán sử dụng các phép đo độ giống nhau hoặc khoảng cách giữa các điểm dữ liệu trong không gian dữ liệu để tìm ra các vùng dữ liệu dày đặc. Vì vậy, thông thường nên chia tỷ lệ dữ liệu trước khi sử dụng thuật toán phân cụm.

> Central to all of the goals of cluster analysis is the notion of the degree of similarity (or dissimilarity) between the individual objects being clustered. A clustering method attempts to group the objects based on the definition of similarity supplied to it.

— Trang 502, [The Elements of Statistical Learning: Data Mining, Inference, and Prediction](https://amzn.to/38bbWGH), 2016.

Một số thuật toán phân cụm yêu cầu bạn chỉ định hoặc đoán số lượng cụm cần phân tách, trong khi các thuật toán khác yêu cầu đặc các điểm kỹ thuật của một số khoảng cách tối thiểu giữa các điểm dữ liệu trong đó các điểm có thể được coi là “gần” hoặc “được kết nối” với nhau.

Như vậy, phân tích cụm là một quá trình lặp đi lặp lại trong đó việc đánh giá chủ quan các cụm xác định được đưa trở lại vào các thay đổi đối với cấu hình thuật toán cho đến khi đạt được kết quả mong muốn hoặc phù hợp.

Thư viện scikit-learn cung cấp một bộ các thuật toán phân cụm khác nhau để lựa chọn.

10 thuật toán phân cụm phổ biến:

*   Affinity Propagation
*   Agglomerative Clustering
*   BIRCH
*   DBSCAN
*   K-Means
*   Mini-Batch K-Means
*   Mean Shift
*   OPTICS
*   Spectral Clustering
*   Mixture of Gaussians

Mỗi thuật toán cung cấp một cách tiếp cận khác nhau cho thách thức khám phá các nhóm tự nhiên trong dữ liệu.

Không có thuật toán phân cụm tốt nhất và không có cách dễ dàng để tìm thuật toán tốt nhất cho dữ liệu của bạn mà không cần thử nghiệm.

Trong bài viết này, chúng ta sẽ xem xét cách sử dụng từng thuật toán phân cụm phổ biến trong số 10 thuật toán này từ thư viện scikit-learn..

Các ví dụ sẽ cung cấp cơ sở để bạn chép-dán các ví dụ và kiểm tra các phương pháp trên dữ liệu của riêng bạn.

Chúng tôi sẽ không đi sâu vào lý thuyết đằng sau cách các thuật toán hoạt động hoặc so sánh chúng trực tiếp. Cụ thể, xem:

*   [Clustering, scikit-learn API](https://scikit-learn.org/stable/modules/clustering.html).

Oke lẹt gâu.

## Các ví dụ

Trong phần này, chúng ta sẽ xem xét cách sử dụng 10 thuật toán phân cụm phổ biến trong scikit-learn, bao gồm một ví dụ về việc khớp mô hình và một ví dụ về trực quan hóa kết quả.

Các ví dụ được thiết kế để bạn chép-dán vào dự án của riêng bạn và áp dụng các phương pháp cho dữ liệu của riêng bạn.

### Cài thư viện

Đừng bỏ qua bước này vì bạn sẽ cần phải đảm bảo đã cài đặt phiên bản mới nhất.

Bạn có thể cài đặt thư viện scikit-learn bằng trình cài đặt pip Python, như sau:  
`sudo pip install scikit-learn`  
Để biết thêm hướng dẫn cài đặt cụ thể cho nền tảng của bạn, hãy xem:

*   [Installing scikit-learn](https://scikit-learn.org/stable/install.html)

Tiếp theo, hãy xác nhận rằng thư viện đã được cài đặt và bạn đang sử dụng phiên bản mới nhất.

Chạy đoạn script sau để in số phiên bản thư viện.

    #check scikit-learn version
    import sklearn
    print(sklearn.__version__)

    0.22.1

### Clustering Dataset

Ta sẽ sử dụng hàm [make_classification()](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.make_classification.html) để tạo ra một tập dữ liệu gồm 2 class

Dataset sẽ chứa 1,000 điểm dữ liệu, mỗi điểm dữ liệu sẽ có 2 thuộc tính và thuộc về 1 lớp. Các cụm được hiển thị trực quan trên không gian hai chiều để chúng ta có thể vẽ dữ liệu với một biểu đồ phân tán và tô màu các điểm trong biểu đồ theo cụm được gán. Điều này sẽ giúp ta biết được độ hiệu quả của model phân cụm trên thí nghiệm.

Các cụm trong bài test này dựa trên một Gaussian đa biến và không phải tất cả các thuật toán phân cụm sẽ có hiệu quả trong việc xác định các loại cụm này. Như vậy, kết quả trong hướng dẫn này không nên được sử dụng làm cơ sở để so sánh các phương pháp nói chung.

Một ví dụ về việc tạo và tóm tắt bộ dữ liệu phân cụm tổng hợp được liệt kê dưới đây.

    # synthetic classification dataset
    from numpy import where
    from sklearn.datasets 
    import make_classification
    from matplotlib import pyplot
    # define dataset
    X, y = make_classification(n_samples=1000, n_features=2, n_informative=2, n_redundant=0, n_clusters_per_class=1, random_state=4)
    # create scatter plot for samples from each class
    for class_value in range(2):
    # get row indexes for samples with this class
    row_ix = where(y == class_value)
    # create scatter of these samples
    pyplot.scatter(X[row_ix, 0], X[row_ix, 1])
    # show the plot
    pyplot.show()

Chạy ví dụ này sẽ tạo ra tập dữ liệu phân cụm, sau đó vẽ một biểu đồ phân tán dữ liệu đầu vào với các điểm được tô màu bởi nhãn lớp (cụm lý tưởng).

Chúng ta có thể thấy rõ hai nhóm dữ liệu riêng biệt trên không gian hai chiều và hy vọng rằng thuật toán phân cụm tự động có thể phát hiện các nhóm này.

<div class="wp-block-image is-style-default">

![Sơ đồ phân tán của bộ dữ liệu phân cụm tổng hợp với các điểm được tô màu bởi cụm đã biết](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2020/04/Scatter-Plot-of-Synthetic-Clustering-Dataset-With-Points-Colored-By-Known-Cluster.png)

</div>

Sơ đồ phân tán của bộ dữ liệu phân cụm tổng hợp với các điểm được tô màu bởi cụm đã biết

Tiếp theo, chúng ta có thể bắt đầu xem xét các ví dụ về thuật toán phân cụm được áp dụng cho bộ dữ liệu này.

### Affinity Propagation

Affinity Propagation liên quan đến việc tìm ra một tập các điểm dữ liệu mô tả tốt nhất toàn bộ tập dữ liệu

> We devised a method called “affinity propagation,” which takes as input measures of similarity between pairs of data points. Real-valued messages are exchanged between data points until a high-quality set of exemplars and corresponding clusters gradually emerges

— [Clustering by Passing Messages Between Data Points](https://science.sciencemag.org/content/315/5814/972), 2007.

Ý tưởng thuật toán được mô tả trong paper:

*   [Clustering by Passing Messages Between Data Points](https://science.sciencemag.org/content/315/5814/972), 2007.

Ví dụ đầy đủ được liệt kê dưới đây.

    # affinity propagation clustering
    from numpy import unique
    from numpy import where
    from sklearn.datasets import make_classification
    from sklearn.cluster import AffinityPropagation
    from matplotlib import pyplot
    # define dataset
    X, _ = make_classification(n_samples=1000, n_features=2, n_informative=2, n_redundant=0, n_clusters_per_class=1, random_state=4)
    # define the model
    model = AffinityPropagation(damping=0.9)
    # fit the modelmodel.fit(X)
    # assign a cluster to each example
    yhat = model.predict(X)
    # retrieve unique clusters
    clusters = unique(yhat)
    # create scatter plot for samples from each cluster
    for cluster in clusters:
    # get row indexes for samples with this cluster
    row_ix = where(yhat == cluster)# create scatter of these samplespyplot.scatter(X[row_ix, 0], X[row_ix, 1])
    # show the plot
    pyplot.show()

Chạy ví dụ sẽ fit mô hình trên tập dữ liệu huấn luyện và dự đoán một cụm cho mỗi điểm dữ liệu trong tập dữ liệu. Một biểu đồ phân tán sau đó được tạo với các điểm được tô màu bởi cụm được gán.

Trong trường hợp này, ta không thể đạt được kết quả tốt.

<div class="wp-block-image">

![Sơ đồ phân tán dữ liệu với các cụm được xác định bằng cách sử dụng Affinity Propagation](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2020/04/Scatter-Plot-of-Dataset-With-Clusters-Identified-Using-Affinity-Propagation.png)

</div>

Sơ đồ phân tán dữ liệu với các cụm được xác định bằng cách sử dụng Affinity Propagation

### Agglomerative Clustering

Agglomerative clustering dựa trên việc hợp nhất các cụm dữ liệu cho tới khi đạt được số lượng cụm mong muốn.

Nó là một phần của lớp phương pháp phân cụm phân cấp rộng hơn và bạn có thể tìm hiểu thêm tại đây:

*   [Hierarchical clustering, Wikipedia](https://en.wikipedia.org/wiki/Hierarchical_clustering).

Thuật toán sử dụng class [Agglomerative Clustering](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.AgglomerativeClustering.html) và tham số cần quan tâm là “_n_clusters_”, tương ứng với số lượng cluster mong muốn, trong trường hợp này là 2.

Ví dụ đầy đủ được liệt kê dưới đây.

    # agglomerative clustering
    from numpy import unique
    from numpy import where
    from sklearn.datasets import make_classification
    from sklearn.cluster import AgglomerativeClustering
    from matplotlib import pyplot
    # define datasetX, _ = make_classification(n_samples=1000, n_features=2, n_informative=2, n_redundant=0, n_clusters_per_class=1, random_state=4)
    # define the model
    model = AgglomerativeClustering(n_clusters=2)
    # fit model and predict clusters
    yhat = model.fit_predict(X)
    # retrieve unique clusters
    clusters = unique(yhat)
    # create scatter plot for samples from each cluster
    for cluster in clusters:
    # get row indexes for samples with this cluster
    row_ix = where(yhat == cluster)
    # create scatter of these samples
    pyplot.scatter(X[row_ix, 0], X[row_ix, 1])
    # show the plot
    pyplot.show()

Chạy ví dụ sẽ fit mô hình trên tập dữ liệu huấn luyện và dự đoán một cụm cho mỗi điểm dữ liệu trong tập dữ liệu. Một biểu đồ phân tán sau đó được tạo với các điểm được tô màu bởi cụm được gán.

Trong trường hợp này, ta xác định được một nhóm hợp lý.

<div class="wp-block-image">

![Sơ đồ phân tán dữ liệu với các cụm được xác định bằng cách sử dụng Agglomerative Clustering](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2020/04/Scatter-Plot-of-Dataset-With-Clusters-Identified-Using-Agglomerative-Clustering.png)

</div>

Sơ đồ phân tán dữ liệu với các cụm được xác định bằng cách sử dụng Agglomerative Clustering

### BIRCH

BIRCH Clustering (BIRCH là viết tắt của Balanced Iterative Reducing and Clustering using  
Hierarchies) dựa trên việc tạo ra một cấu trúc cây dựa trên những trung tâm (centroid) được xác định trước

> BIRCH incrementally and dynamically clusters incoming multi-dimensional metric data points to try to produce the best quality clustering with the available resources (i. e., available memory and time constraints).

— [BIRCH: An efficient data clustering method for large databases](https://dl.acm.org/doi/10.1145/235968.233324), 1996.

Ý tưởng của thuật toán được mô tả trong paper:

*   [BIRCH: An efficient data clustering method for large databases](https://dl.acm.org/doi/10.1145/235968.233324), 1996.

Thuật toán được triển khai thông qua [class Birch](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.Birch.html), tham số chính cần chỉnh sửa là “_threshold_” và “_n_clusters_”

Ví dụ đầy đủ được liệt kê dưới đây.

    # birch clustering
    from numpy import unique
    from numpy import where
    from sklearn.datasets import make_classification
    from sklearn.cluster import Birch
    from matplotlib import pyplot
    # define dataset
    X, _ = make_classification(n_samples=1000, n_features=2, n_informative=2, n_redundant=0, n_clusters_per_class=1, random_state=4)
    # define the model
    model = Birch(threshold=0.01, n_clusters=2)
    # fit the model
    model.fit(X)
    # assign a cluster to each example
    yhat = model.predict(X)
    # retrieve unique clusters
    clusters = unique(yhat)
    # create scatter plot for samples from each cluster
    for cluster in clusters:
    # get row indexes for samples with this cluster
    row_ix = where(yhat == cluster)
    # create scatter of these samples
    pyplot.scatter(X[row_ix, 0], X[row_ix, 1])
    # show the plot
    pyplot.show()

Chạy ví dụ sẽ fit mô hình trên tập dữ liệu huấn luyện và dự đoán một cụm cho mỗi điểm dữ liệu trong tập dữ liệu. Một biểu đồ phân tán sau đó được tạo với các điểm được tô màu bởi cụm được gán.

Trong trường hợp này, thuật toán làm việc rất tốt.

<div class="wp-block-image">

![Sơ đồ phân tán dữ liệu với các cụm được xác định bằng cách sử dụng BIRCH Clustering](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2020/04/Scatter-Plot-of-Dataset-With-Clusters-Identified-Using-BIRCH-Clustering.png)

</div>

Sơ đồ phân tán dữ liệu với các cụm được xác định bằng cách sử dụng BIRCH Clustering

## DBSCAN

DBSCAN Clustering (DBSCAN là viết tắt của Density-Based Spatial Clustering of Applications with Noise) dựa trên việc tìm kiếm những khu vực có mật độ cao trên miền dữ liệu và tạo ra các cụm bằng việc mở rộng những khu vực đó ra xung quanh.

> … we present the new clustering algorithm DBSCAN relying on a density-based notion of clusters which is designed to discover clusters of arbitrary shape. DBSCAN requires only one input parameter and supports the user in determining an appropriate value for it

— [A Density-Based Algorithm for Discovering Clusters in Large Spatial Databases with Noise](https://www.osti.gov/biblio/421283), 1996.

Ý tưởng thuật toán được mô tả trong paper:

*   [A Density-Based Algorithm for Discovering Clusters in Large Spatial Databases with Noise](https://www.osti.gov/biblio/421283), 1996.

Thuật toán được triển khai thông qua [DBSCAN class](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.DBSCAN.html) và tham số chính cần điều chỉnh là “_eps_” và “_min_samples_”.

Ví dụ đầy đủ được liệt kê dưới đây.

    # dbscan clustering
    from numpy import unique
    from numpy import where
    from sklearn.datasets import make_classification
    from sklearn.cluster import DBSCAN
    from matplotlib import pyplot
    # define dataset
    X, _ = make_classification(n_samples=1000, n_features=2, n_informative=2, n_redundant=0, n_clusters_per_class=1, random_state=4)
    # define the model
    model = DBSCAN(eps=0.30, min_samples=9)
    # fit model and predict clusters
    yhat = model.fit_predict(X)
    # retrieve unique clusters
    clusters = unique(yhat)
    # create scatter plot for samples from each cluster
    for cluster in clusters:
        # get row indexes for samples with this cluster
        row_ix = where(yhat == cluster)
    # create scatter of these samples
    pyplot.scatter(X[row_ix, 0], X[row_ix, 1])
    # show the plot
    pyplot.show()

Chạy ví dụ sẽ fit mô hình trên tập dữ liệu huấn luyện và dự đoán một cụm cho mỗi điểm dữ liệu trong tập dữ liệu. Một biểu đồ phân tán sau đó được tạo với các điểm được tô màu bởi cụm được gán.

Trong trường hợp này, thậut toán tìm ra những cụm hợp lý, tuy nhiên vẫn cần phải điều chỉnh các tham số.

<div class="wp-block-image">

![Sơ đồ phân tán dữ liệu với các cụm được xác định bằng cách sử dụng Clustering](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2020/04/Scatter-Plot-of-Dataset-With-Clusters-Identified-Using-DBSCAN-Clustering.png)
</div>

Sơ đồ phân tán dữ liệu với các cụm được xác định bằng cách sử dụng Clustering

Vậy qua bài viết [12 Thuật toán phân cụm (clustering) với python (Phần 1)](https://luublog97.cf/12-clustering-algorithm-python-scikit-learn), chúng ta đã tìm hiểu khái niệm và sử dụng một số model để clustering với thư viện sklearn.

Trong phần 2, ta sẽ tiếp tục đi qua một số thuật toán phân cụm khác, bao gồm

1.  K-Means
2.  Mini-Batch K-Means
3.  Mean Shift
4.  OPTICS
5.  Spectral Clustering
6.  Gaussian Mixture Model

[12 Thuật toán phân cụm (clustering) với python (Phần 2)](https://luublog97.cf/12-clustering-algorithm-python-scikit-learn-phan-2)

Reference: https://machinelearningmastery.com/clustering-algorithms-with-python/