# ELK-Learning

## Tổng quan về ELK

Dưới đây là tổng hợp nội dung bài học về Elasticsearch:

### Giới thiệu về Elastic Stack

- **2010**: Elasticsearch ra mắt dưới dạng mã nguồn mở.
- **2012**: Thành lập công ty Elasticsearch.
- **2015**: Đổi tên thành Elastic.
- **Elastic Stack**: Bao gồm Elasticsearch, Logstash, Kibana, Beats và X-Pack.

### Khái niệm cơ bản về Elasticsearch

- **Tài liệu (Documents)**: Dữ liệu JSON cấu trúc, mỗi tài liệu có ID và kiểu riêng.
- **Chỉ mục (Indices)**: Tập hợp các tài liệu có cấu trúc tương tự, chứa các chỉ mục ngược.
- **Kiểu (Types)**: Định nghĩa lược đồ và ánh xạ của các tài liệu cùng loại.

### Kiến trúc và khả năng mở rộng của Elasticsearch

- Elasticsearch là hệ thống tìm kiếm thời gian gần thực (NRT).
- Một cụm Elasticsearch bao gồm các nút có thể là Master, Data, Coordinating, Ingest và Machine Learning.
- Chia cụm để tránh "split brain" bằng cách thiết lập `minimum_master_nodes`.

### RESTful API và các công cụ hỗ trợ

- **Curl**: Công cụ dòng lệnh để gửi yêu cầu HTTP.
- **Httpie**: Công cụ dòng lệnh với cú pháp đơn giản hơn Curl.

### Chỉ mục và phân mảnh

- **Phân mảnh chính và sao lưu**: Chia chỉ mục thành các mảnh chính và sao lưu để tăng cường hiệu suất và khả năng chịu lỗi.
- **Quiz**: Số mảnh của chỉ mục với 5 mảnh chính và 3 sao lưu là 20.

### Các thao tác với Elasticsearch

- **Thêm, cập nhật, xóa tài liệu**: Sử dụng các phương thức HTTP tương ứng như PUT, POST, DELETE.
- **Kiểm soát đồng bộ**: Sử dụng `retry_on_conflicts` để xử lý xung đột phiên bản.

### Các loại truy vấn và bộ lọc

- **Query DSL**: Ngôn ngữ truy vấn JSON của Elasticsearch.
- **Bộ lọc**: Hỏi các câu hỏi có/không, nhanh hơn và có thể lưu cache.
- **Truy vấn**: Trả về dữ liệu dựa trên độ liên quan.

### Nâng cao tìm kiếm và tối ưu hóa

- **Fuzzy matches**: Cho phép sai số trong truy vấn để xử lý lỗi chính tả.
- **Pagination**: Phân trang kết quả để tránh làm giảm hiệu suất.
- **Sorting**: Sắp xếp kết quả, sử dụng trường `keyword` để sắp xếp dữ liệu không được phân tích.


## Giới thiệu về mô hình kết hợp Elasticsearch và ES-Hadoop

**Elasticsearch**:
- Elasticsearch là một công cụ tìm kiếm và phân tích dữ liệu mạnh mẽ, được thiết kế để làm việc với dữ liệu lớn và phức tạp. Nó cho phép tìm kiếm và phân tích dữ liệu theo thời gian gần thực (near real-time) và hỗ trợ nhiều loại truy vấn phong phú.

**Hadoop**:
- Hadoop là một hệ sinh thái mã nguồn mở cho việc xử lý và lưu trữ dữ liệu lớn. Nó bao gồm HDFS (Hadoop Distributed File System) để lưu trữ dữ liệu và MapReduce để xử lý dữ liệu song song trên các cụm máy tính lớn.

**ES-Hadoop**:
- ES-Hadoop là một module kết hợp giữa Elasticsearch và Hadoop, cho phép tích hợp và tương tác giữa hai hệ thống này. Nó cho phép lưu trữ và tìm kiếm dữ liệu lớn trên Elasticsearch trong khi vẫn sử dụng khả năng lưu trữ và xử lý dữ liệu phân tán của Hadoop.

### Các Thành Phần Chính

1. **HDFS (Hadoop Distributed File System)**:
   - HDFS được sử dụng để lưu trữ dữ liệu lớn dưới dạng phân tán trên nhiều nút trong cụm Hadoop. Nó cung cấp khả năng chịu lỗi và mở rộng quy mô.

2. **MapReduce**:
   - MapReduce là mô hình lập trình và cũng là một công cụ trong Hadoop để xử lý dữ liệu lớn. Nó chia công việc thành các tác vụ nhỏ, xử lý song song và kết hợp kết quả cuối cùng.

3. **ES-Hadoop Connector**:
   - Đây là cầu nối giữa Hadoop và Elasticsearch. Nó cho phép dữ liệu từ HDFS được lập chỉ mục vào Elasticsearch và ngược lại. ES-Hadoop Connector hỗ trợ nhiều công cụ trong hệ sinh thái Hadoop như Hive, Pig, và Spark.

### Mô Hình Hoạt Động

1. **Lưu Trữ Dữ Liệu**:
   - Dữ liệu lớn được lưu trữ trên HDFS, nơi nó được phân tán và sao lưu trên nhiều nút trong cụm Hadoop.

2. **Chuyển Dữ Liệu Sang Elasticsearch**:
   - Sử dụng ES-Hadoop Connector, dữ liệu từ HDFS được chuyển sang Elasticsearch để lập chỉ mục và tìm kiếm. Quá trình này có thể sử dụng MapReduce, Spark, hoặc các công cụ khác để xử lý dữ liệu trước khi gửi đến Elasticsearch.

3. **Tìm Kiếm và Phân Tích**:
   - Sau khi dữ liệu được lập chỉ mục trong Elasticsearch, người dùng có thể sử dụng các API tìm kiếm và phân tích mạnh mẽ của Elasticsearch để truy vấn và phân tích dữ liệu. Kibana, công cụ giao diện người dùng của Elastic Stack, có thể được sử dụng để tạo các biểu đồ, bảng điều khiển và báo cáo dựa trên dữ liệu trong Elasticsearch.

4. **Tương Tác Ngược**:
   - ES-Hadoop cũng cho phép dữ liệu từ Elasticsearch được chuyển ngược lại vào HDFS hoặc các công cụ khác trong hệ sinh thái Hadoop để xử lý thêm hoặc lưu trữ dài hạn.

### Ưu Điểm của Mô Hình Kết Hợp

- **Mở Rộng và Linh Hoạt**:
  - Sử dụng HDFS để lưu trữ dữ liệu lớn và Elasticsearch để tìm kiếm và phân tích cho phép hệ thống mở rộng linh hoạt, tận dụng tối đa tài nguyên của cả hai hệ thống.

- **Hiệu Suất Tìm Kiếm Cao**:
  - Elasticsearch cung cấp khả năng tìm kiếm và phân tích dữ liệu gần như tức thì, phù hợp cho các ứng dụng yêu cầu phản hồi nhanh.

- **Xử Lý Dữ Liệu Lớn**:
  - Hadoop cung cấp khả năng xử lý dữ liệu lớn mạnh mẽ, đặc biệt là khi kết hợp với các công cụ như MapReduce và Spark.

### Ứng Dụng Thực Tế

- **Phân Tích Nhật Ký (Log Analysis)**:
  - Sử dụng Logstash để thu thập và chuyển đổi nhật ký từ nhiều nguồn khác nhau, sau đó lập chỉ mục vào Elasticsearch và lưu trữ dài hạn trên HDFS.

- **E-commerce Search**:
  - Lưu trữ thông tin sản phẩm trên HDFS, lập chỉ mục vào Elasticsearch để hỗ trợ tìm kiếm và phân tích hành vi mua sắm của khách hàng.

- **IoT (Internet of Things)**:
  - Lưu trữ dữ liệu từ các thiết bị IoT trên HDFS, lập chỉ mục vào Elasticsearch để giám sát và phân tích dữ liệu thời gian thực.

Với mô hình này, người dùng có thể tận dụng tối đa sức mạnh của cả Elasticsearch và Hadoop để quản lý và phân tích dữ liệu lớn một cách hiệu quả và linh hoạt.

## Các khái niệm logic cơ bản của Elasticsearch:

### 1. Tài liệu (Documents)
- **Định nghĩa**: Tài liệu là đơn vị dữ liệu cơ bản nhất mà bạn tìm kiếm và lưu trữ trong Elasticsearch. Tài liệu được biểu diễn dưới dạng JSON, có thể chứa nhiều kiểu dữ liệu như văn bản, số, ngày tháng, và các đối tượng JSON phức tạp khác.
- **ID**: Mỗi tài liệu có một ID duy nhất, giúp phân biệt tài liệu này với tài liệu khác trong cùng một chỉ mục.
- **Loại (Type)**: Trước Elasticsearch 7.0, mỗi tài liệu được gán một loại (type). Tuy nhiên, từ phiên bản 7.0 trở đi, khái niệm loại đã bị loại bỏ, mỗi chỉ mục chỉ chứa một loại tài liệu duy nhất.

### 2. Chỉ mục (Indices)
- **Định nghĩa**: Chỉ mục là một tập hợp các tài liệu có cấu trúc tương tự. Một chỉ mục tương tự như một cơ sở dữ liệu trong hệ quản trị cơ sở dữ liệu truyền thống.
- **Chức năng**: Chỉ mục chứa các chỉ mục ngược (inverted indices), cho phép tìm kiếm nhanh chóng và hiệu quả trên tất cả các tài liệu trong chỉ mục đó.

### 3. Loại (Types) (đã bị loại bỏ từ Elasticsearch 7.0)
- **Định nghĩa**: Loại định nghĩa lược đồ (schema) và ánh xạ (mapping) được chia sẻ bởi các tài liệu cùng loại. 
- **Chuyển đổi**: Từ Elasticsearch 7.0, khái niệm loại đã bị loại bỏ, và mỗi chỉ mục chỉ chứa một loại tài liệu duy nhất. Điều này nhằm đơn giản hóa và tránh các vấn đề tiềm ẩn về hiệu suất và quản lý.

### 4. Chỉ mục ngược (Inverted Index)
- **Định nghĩa**: Chỉ mục ngược là cấu trúc dữ liệu được sử dụng để lập chỉ mục toàn văn bản (full-text search). Nó ánh xạ các thuật ngữ (terms) đến các tài liệu chứa chúng.
- **Cách hoạt động**: Khi một tài liệu được thêm vào Elasticsearch, nó được phân tích thành các thuật ngữ và mỗi thuật ngữ được thêm vào chỉ mục ngược cùng với thông tin về tài liệu chứa thuật ngữ đó. Điều này giúp tìm kiếm nhanh chóng và hiệu quả.

### 5. Phân mảnh (Shards)
- **Định nghĩa**: Một chỉ mục có thể được chia thành nhiều phân mảnh nhỏ hơn (shards) để tăng cường hiệu suất và khả năng mở rộng. Mỗi phân mảnh là một chỉ mục Lucene độc lập, chứa một phần dữ liệu của chỉ mục gốc.
- **Phân loại**:
  - **Phân mảnh chính (Primary Shard)**: Chứa dữ liệu gốc của chỉ mục.
  - **Phân mảnh sao lưu (Replica Shard)**: Bản sao của phân mảnh chính, giúp tăng cường khả năng chịu lỗi và cải thiện hiệu suất đọc.

### 6. Cụm (Cluster)
- **Định nghĩa**: Cụm là tập hợp các nút (nodes) làm việc cùng nhau để lưu trữ dữ liệu và cung cấp khả năng tìm kiếm trên dữ liệu đó.
- **Chức năng**: Mỗi cụm có một tên duy nhất để phân biệt với các cụm khác. Một cụm có thể chứa nhiều chỉ mục, và mỗi chỉ mục có thể được chia thành nhiều phân mảnh và sao lưu trên các nút khác nhau.

### 7. Nút (Nodes)
- **Định nghĩa**: Một nút là một máy chủ chạy một phiên bản Elasticsearch. Mỗi nút thuộc về một cụm và có thể đóng vai trò khác nhau như nút chính, nút dữ liệu, nút điều phối, hoặc nút ingest.
- **Vai trò**:
  - **Nút chính (Master Node)**: Quản lý các hành động ở cấp cụm như tạo/xóa chỉ mục, theo dõi các nút trong cụm, và quyết định phân phối các phân mảnh.
  - **Nút dữ liệu (Data Node)**: Chứa các phân mảnh và thực hiện các hoạt động liên quan đến dữ liệu như CRUD, tìm kiếm, và gộp.
  - **Nút điều phối (Coordinating Node)**: Định tuyến các yêu cầu, xử lý giai đoạn giảm tìm kiếm, và phân phối các thao tác bulk indexing.
  - **Nút ingest (Ingest Node)**: Thực hiện các pipelines xử lý dữ liệu trước khi lập chỉ mục.

### 8. Mappings
- **Định nghĩa**: Mapping là định nghĩa lược đồ cho các tài liệu trong một chỉ mục. Nó xác định cách các trường trong tài liệu được lưu trữ và lập chỉ mục.
- **Chức năng**: Mapping bao gồm các loại trường (text, keyword, date, long, double, boolean, etc.), các bộ phân tích (analyzers), và các cài đặt lập chỉ mục khác.

### 9. Bộ phân tích (Analyzers)
- **Định nghĩa**: Bộ phân tích là thành phần phân tích các trường văn bản thành các thuật ngữ trong quá trình lập chỉ mục và tìm kiếm.
- **Thành phần**: Gồm các bộ lọc ký tự (character filters), bộ phân tách (tokenizers), và bộ lọc thuật ngữ (token filters).

## Chỉ mục ngược (Inverted Index)

**Định nghĩa**:
- Chỉ mục ngược là một cấu trúc dữ liệu được sử dụng để tăng cường hiệu suất tìm kiếm toàn văn bản (full-text search). Nó ánh xạ các thuật ngữ (terms) đến các tài liệu chứa các thuật ngữ đó.

**Cách hoạt động**:
- Khi một tài liệu được thêm vào Elasticsearch, nó được phân tích thành các thuật ngữ (tokens). Mỗi thuật ngữ được thêm vào chỉ mục ngược cùng với thông tin về tài liệu chứa thuật ngữ đó.
- **Ví dụ đơn giản**: 
  - Giả sử có hai tài liệu:
    - Tài liệu 1: "Space: The final frontier. These are the voyages..."
    - Tài liệu 2: "He’s bad, he’s number one. He’s the space cowboy with the lasergun!"
  - Các từ trong các tài liệu này sẽ được phân tích và lưu trữ trong chỉ mục ngược như sau:
    - `space`: [Tài liệu 1, Tài liệu 2]
    - `the`: [Tài liệu 1, Tài liệu 2]
    - `final`: [Tài liệu 1]
    - `frontier`: [Tài liệu 1]
    - `bad`: [Tài liệu 2]
    - `number`: [Tài liệu 2]
    - `one`: [Tài liệu 2]
    - `cowboy`: [Tài liệu 2]
    - `lasergun`: [Tài liệu 2]

**Lợi ích của Chỉ mục ngược**:
1. **Tìm kiếm nhanh chóng**: 
   - Thay vì duyệt qua tất cả các tài liệu để tìm một thuật ngữ, chỉ mục ngược cho phép Elasticsearch nhanh chóng xác định tài liệu nào chứa thuật ngữ đó.
   
2. **Hiệu suất cao**:
   - Chỉ mục ngược được tối ưu hóa cho các truy vấn tìm kiếm toàn văn bản, giúp cải thiện hiệu suất đáng kể so với các phương pháp tìm kiếm truyền thống.

3. **Tính khả dụng cao**:
   - Chỉ mục ngược lưu trữ thông tin về các thuật ngữ và vị trí của chúng trong tài liệu, giúp hệ thống tìm kiếm mạnh mẽ và dễ dàng mở rộng.

### Các khái niệm liên quan đến Chỉ mục ngược:

1. **Term Frequency (TF)**:
   - Là số lần một thuật ngữ xuất hiện trong một tài liệu.
   - **Ví dụ**: Trong Tài liệu 1, thuật ngữ `the` xuất hiện 2 lần, TF của `the` trong Tài liệu 1 là 2.

2. **Document Frequency (DF)**:
   - Là số tài liệu chứa một thuật ngữ cụ thể.
   - **Ví dụ**: Thuật ngữ `space` xuất hiện trong cả Tài liệu 1 và Tài liệu 2, DF của `space` là 2.

3. **TF-IDF (Term Frequency - Inverse Document Frequency)**:
   - Một chỉ số đo lường mức độ quan trọng của một thuật ngữ trong một tài liệu dựa trên tần suất của thuật ngữ đó và tần suất xuất hiện của nó trong tất cả các tài liệu.
   - **Công thức**: TF-IDF = TF * log(N / DF), trong đó N là tổng số tài liệu.
   - **Ý nghĩa**: Thuật ngữ có TF cao trong một tài liệu cụ thể nhưng DF thấp (ít xuất hiện trong các tài liệu khác) sẽ có TF-IDF cao, cho thấy thuật ngữ đó có ý nghĩa đặc biệt đối với tài liệu đó.

**Kết luận**:
- Chỉ mục ngược là thành phần cốt lõi giúp Elasticsearch thực hiện các truy vấn tìm kiếm toàn văn bản một cách nhanh chóng và hiệu quả. Bằng cách lưu trữ ánh xạ giữa các thuật ngữ và tài liệu chứa chúng, chỉ mục ngược giúp cải thiện hiệu suất và độ chính xác của các truy vấn tìm kiếm.

## Near Real-Time (NRT) của Elasticsearch

**Định nghĩa**:
- **Near Real-Time (NRT)** trong Elasticsearch có nghĩa là hệ thống cung cấp khả năng tìm kiếm và lập chỉ mục gần như ngay lập tức. Có một độ trễ nhỏ (thường là khoảng một giây) giữa thời điểm một tài liệu được lập chỉ mục và thời điểm nó có thể tìm kiếm được.

### Cách Hoạt Động của NRT:

1. **Indexing (Lập chỉ mục)**:
   - Khi một tài liệu mới được thêm vào Elasticsearch, nó trước tiên được lưu trữ trong bộ nhớ đệm (in-memory buffer).
   - Tài liệu này sau đó được thêm vào một cấu trúc dữ liệu tạm thời gọi là **translog** (transaction log) để đảm bảo rằng dữ liệu không bị mất nếu hệ thống gặp sự cố.

2. **Refresh Interval (Khoảng thời gian làm mới)**:
   - Elasticsearch mặc định có một khoảng thời gian làm mới (refresh interval) là 1 giây.
   - Cứ mỗi giây, Elasticsearch sẽ tự động làm mới các phân mảnh (shards) của chỉ mục, di chuyển dữ liệu từ bộ nhớ đệm vào một phân đoạn (segment) mới của chỉ mục.
   - Sau khi phân đoạn này được tạo, nó sẽ trở nên có thể tìm kiếm được.

3. **Segments (Phân đoạn)**:
   - Một phân đoạn là một chỉ mục con của Lucene, và nó là đơn vị cơ bản của việc lưu trữ và tìm kiếm trong Elasticsearch.
   - Khi dữ liệu được làm mới và di chuyển vào phân đoạn, phân đoạn này sẽ được thêm vào chỉ mục và trở nên có thể tìm kiếm được.
   - Các phân đoạn cũ hơn sẽ được hợp nhất định kỳ để tối ưu hóa hiệu suất và sử dụng không gian lưu trữ.

### Ưu Điểm của NRT:

1. **Tìm Kiếm Gần Như Thời Gian Thực**:
   - Cho phép người dùng tìm kiếm dữ liệu mới được lập chỉ mục gần như ngay lập tức, điều này rất quan trọng đối với các ứng dụng yêu cầu phản hồi nhanh, như tìm kiếm sản phẩm trong e-commerce hay phân tích log thời gian thực.

2. **Hiệu Suất Cao**:
   - Sử dụng bộ nhớ đệm và translog giúp tăng cường hiệu suất lập chỉ mục và đảm bảo tính toàn vẹn của dữ liệu.

3. **Độ Tin Cậy Cao**:
   - Translog đảm bảo rằng dữ liệu không bị mất trong trường hợp hệ thống gặp sự cố, giúp Elasticsearch đáng tin cậy trong môi trường sản xuất.

### Tối Ưu Hóa NRT:

1. **Điều Chỉnh Refresh Interval**:
   - Khoảng thời gian làm mới có thể được điều chỉnh để phù hợp với yêu cầu cụ thể của ứng dụng. Ví dụ, trong môi trường phát triển, có thể đặt khoảng thời gian làm mới ngắn hơn để phản hồi nhanh hơn, trong khi trong môi trường sản xuất, có thể kéo dài khoảng thời gian này để tối ưu hóa hiệu suất.

2. **Sử Dụng API Refresh Thủ Công**:
   - Trong một số trường hợp, người dùng có thể muốn kiểm soát khi nào dữ liệu mới trở nên có thể tìm kiếm được bằng cách sử dụng API refresh thủ công thay vì dựa vào khoảng thời gian làm mới tự động.

3. **Quản Lý Phân Đoạn**:
   - Việc quản lý và hợp nhất phân đoạn một cách hiệu quả có thể cải thiện hiệu suất tìm kiếm và lập chỉ mục. Elasticsearch cung cấp các công cụ và cài đặt để kiểm soát quá trình này.

### Kết Luận:
- NRT là một tính năng quan trọng của Elasticsearch, cho phép hệ thống cung cấp khả năng tìm kiếm dữ liệu mới gần như ngay lập tức. Bằng cách kết hợp bộ nhớ đệm, translog, và quá trình làm mới phân đoạn, Elasticsearch đảm bảo rằng dữ liệu mới có thể tìm kiếm được với độ trễ tối thiểu, đồng thời duy trì hiệu suất và độ tin cậy cao.

## Giới thiệu về cụm Elasticsearch (Elasticsearch cluster):

### 1. Giới thiệu về Cụm Elasticsearch

Cụm Elasticsearch là một tập hợp các nút (nodes) hoạt động cùng nhau để lưu trữ và quản lý dữ liệu, cung cấp khả năng tìm kiếm và phân tích. Mỗi cụm có một tên duy nhất để phân biệt với các cụm khác. Mục tiêu của cụm là cung cấp tính sẵn sàng cao, khả năng chịu lỗi và hiệu suất tốt.

### 2. Thành phần của Cụm Elasticsearch

#### Nút (Node)
- **Master-Eligible Node**: Quản lý trạng thái cụm và thực hiện các tác vụ quản trị như tạo/xóa chỉ mục, phân phối phân mảnh. Mặc định, tất cả các nút đều là master-eligible trừ khi được cấu hình khác.
- **Data Node**: Chứa dữ liệu và thực hiện các hoạt động liên quan đến dữ liệu như CRUD, tìm kiếm, và gộp.
- **Ingest Node**: Xử lý dữ liệu trước khi lưu trữ, sử dụng các pipeline ingest để biến đổi dữ liệu.
- **Coordinating Node**: Định tuyến các yêu cầu từ người dùng đến các nút dữ liệu phù hợp, giảm tải các truy vấn và phân phối các thao tác bulk indexing.
- **Machine Learning Node**: Chạy các tác vụ học máy, yêu cầu X-Pack.
- **Alerting Node**: Chạy các tác vụ cảnh báo.

#### Phân mảnh (Shard)
- **Primary Shard**: Mỗi chỉ mục được chia thành một hoặc nhiều primary shard. Đây là nơi lưu trữ dữ liệu chính.
- **Replica Shard**: Bản sao của primary shard, giúp tăng khả năng chịu lỗi và cải thiện hiệu suất đọc. Số lượng replica shard có thể cấu hình được.

### 3. Kiến trúc Cụm Elasticsearch

#### Quá trình bầu cử Master
- Khi cụm khởi động, các nút sẽ bầu chọn một master node để quản lý trạng thái cụm. 
- **Tránh Split-Brain**: Để ngăn chặn tình trạng split-brain, cài đặt `minimum_master_nodes` nên được thiết lập đúng cách. Đối với một cụm có N master-eligible nodes, giá trị `minimum_master_nodes` nên là (N/2) + 1.

#### Phân phối và Sao lưu dữ liệu
- Elasticsearch tự động phân phối dữ liệu trên các nút khác nhau để tối ưu hóa hiệu suất và khả năng chịu lỗi.
- Các replica shard được sử dụng để sao lưu dữ liệu, đảm bảo dữ liệu không bị mất khi một nút bị lỗi.

### 4. Cài đặt và Quản lý Cụm Elasticsearch

#### Cài đặt Elasticsearch
1. **Tải xuống và cài đặt**: Tải Elasticsearch từ trang web chính thức và cài đặt nó.
2. **Cấu hình**: Cấu hình tệp `elasticsearch.yml` để thiết lập tên cụm (`cluster.name`), tên nút (`node.name`), và các cài đặt mạng (`network.host`).

#### Thêm nút vào Cụm
1. **Cấu hình mạng**: Đảm bảo các nút có thể giao tiếp với nhau qua mạng. Cấu hình `discovery.seed_hosts` để liệt kê các nút khác trong cụm.
2. **Khởi động nút**: Khởi động các nút Elasticsearch. 
3. **Kiểm tra trạng thái cụm**: Sử dụng API `_cat/nodes` hoặc `_cluster/health` để kiểm tra trạng thái cụm và xác nhận các nút đã tham gia cụm thành công.

### 5. Quản lý và Giám sát Cụm

#### Giám sát
1. **API Quản lý Cụm**:
   - Sử dụng `_cat/indices` để liệt kê các chỉ mục.
   - Sử dụng `_cluster/health` để kiểm tra trạng thái sức khỏe của cụm.
   - Sử dụng `_cluster/stats` để lấy thông tin chi tiết về cụm.

2. **Sử dụng Kibana**: Kibana cung cấp giao diện đồ họa giúp giám sát và quản lý cụm dễ dàng hơn. Bạn có thể tạo các bảng điều khiển (dashboard) để theo dõi các chỉ số hiệu suất.

#### Tối ưu hóa
1. **Điều chỉnh phân mảnh**:
   - Số lượng phân mảnh nên được điều chỉnh dựa trên kích thước dữ liệu và tải công việc. Quá nhiều hoặc quá ít phân mảnh đều có thể ảnh hưởng đến hiệu suất.
   - Sử dụng API `_forcemerge` để hợp nhất các phân mảnh nhỏ, giúp cải thiện hiệu suất tìm kiếm.

2. **Quản lý hợp nhất phân mảnh (Segment Merging)**:
   - Quá trình hợp nhất phân mảnh là tự động, nhưng bạn có thể điều chỉnh các cài đặt như `index.merge.scheduler.max_thread_count` để tối ưu hóa hiệu suất.

### 6. Bảo trì và Bảo mật

#### Bảo trì
1. **Sao lưu và phục hồi**: Thiết lập cơ chế sao lưu định kỳ để đảm bảo dữ liệu không bị mất. Sử dụng snapshot và restore để sao lưu và phục hồi dữ liệu.
2. **Nâng cấp**: Thực hiện nâng cấp phiên bản Elasticsearch định kỳ để tận dụng các tính năng mới và bản sửa lỗi bảo mật. Kiểm tra tài liệu nâng cấp để biết chi tiết.

#### Bảo mật
1. **X-Pack**: Sử dụng X-Pack để bảo mật cụm Elasticsearch. X-Pack cung cấp các tính năng bảo mật như xác thực, phân quyền, mã hóa giao tiếp, và giám sát.
2. **Cài đặt bảo mật cơ bản**:
   - Thiết lập xác thực và phân quyền cho người dùng.
   - Mã hóa giao tiếp giữa các nút và giữa nút với client.
   - Kiểm tra và cập nhật thường xuyên để vá các lỗ hổng bảo mật.

### 7. Thực hành Tối ưu hóa và Bảo trì Cụm

#### Tối ưu hóa phân mảnh
- Điều chỉnh số lượng phân mảnh phù hợp với kích thước và mô hình truy cập dữ liệu.
- Sử dụng API `_forcemerge` để hợp nhất các phân mảnh nhỏ, giúp cải thiện hiệu suất tìm kiếm.

#### Bảo trì
- Thực hiện kiểm tra sức khỏe cụm định kỳ bằng cách sử dụng các API quản lý cụm.
- Thực hiện sao lưu dữ liệu định kỳ và kiểm tra khả năng phục hồi dữ liệu từ các bản sao lưu.

#### Bảo mật
- Sử dụng các công cụ và tính năng bảo mật của Elasticsearch như X-Pack để bảo vệ dữ liệu.
- Thực hiện các biện pháp bảo mật như mã hóa giao tiếp, xác thực và phân quyền người dùng.

### Kết luận
- Cụm Elasticsearch là một hệ thống mạnh mẽ cho việc lưu trữ và tìm kiếm dữ liệu phân tán. Bằng cách thiết lập và quản lý cụm một cách hiệu quả, bạn có thể tận dụng tối đa sức mạnh của Elasticsearch để cung cấp các dịch vụ tìm kiếm và phân tích dữ liệu với hiệu suất cao và độ tin cậy.

## Elasticsearch Large Cluster (Cụm Elasticsearch lớn)

**Elasticsearch Large Cluster** là một cụm Elasticsearch với quy mô lớn, được thiết kế để quản lý và xử lý khối lượng dữ liệu khổng lồ và đáp ứng các yêu cầu tìm kiếm và phân tích phức tạp. Một cụm lớn thường bao gồm nhiều nút (nodes) và được cấu hình để đảm bảo hiệu suất cao, khả năng chịu lỗi và tính sẵn sàng cao.

### Thành phần và Kiến trúc của Cụm Elasticsearch lớn

1. **Master Nodes**:
   - **Vai trò**: Quản lý trạng thái cụm, thực hiện các tác vụ quản trị như tạo/xóa chỉ mục, phân phối phân mảnh và theo dõi tình trạng của các nút trong cụm.
   - **Cấu hình**: Thường có ít nhất 3 nút master để đảm bảo tính sẵn sàng cao và tránh tình trạng split-brain.
   - **Thiết lập**: Đặt `node.master: true` và `node.data: false`.

2. **Data Nodes**:
   - **Vai trò**: Chứa dữ liệu và thực hiện các hoạt động liên quan đến dữ liệu như CRUD (Create, Read, Update, Delete), tìm kiếm và gộp.
   - **Cấu hình**: Có nhiều data nodes để phân phối tải công việc và dữ liệu, đảm bảo khả năng mở rộng và chịu lỗi.
   - **Thiết lập**: Đặt `node.master: false` và `node.data: true`.

3. **Ingest Nodes**:
   - **Vai trò**: Xử lý dữ liệu trước khi lưu trữ, sử dụng các pipeline ingest để biến đổi dữ liệu.
   - **Cấu hình**: Được sử dụng để xử lý các yêu cầu nhập liệu (ingest) phức tạp trước khi dữ liệu được lưu trữ trong Elasticsearch.
   - **Thiết lập**: Đặt `node.master: false`, `node.data: false` và `node.ingest: true`.

4. **Coordinating Nodes**:
   - **Vai trò**: Định tuyến các yêu cầu từ người dùng đến các data nodes phù hợp, giảm tải các truy vấn và phân phối các thao tác bulk indexing.
   - **Cấu hình**: Không lưu trữ dữ liệu và không tham gia vào việc quản lý cụm, chỉ thực hiện vai trò định tuyến.
   - **Thiết lập**: Đặt `node.master: false`, `node.data: false` và `node.ingest: false`.

5. **Machine Learning Nodes**:
   - **Vai trò**: Chạy các tác vụ học máy, yêu cầu X-Pack.
   - **Cấu hình**: Được sử dụng để thực hiện các phân tích học máy nâng cao.
   - **Thiết lập**: Đặt `node.master: false`, `node.data: false` và `node.ml: true`.

### Kiến trúc Cụm Lớn

1. **Phân phối và Sao lưu dữ liệu**:
   - **Primary Shards và Replica Shards**: Dữ liệu được chia thành các phân mảnh chính (primary shards) và sao lưu (replica shards). Số lượng phân mảnh và bản sao được cấu hình dựa trên yêu cầu về khả năng chịu lỗi và hiệu suất.
   - **Phân phối trên nhiều nút**: Các phân mảnh được phân phối trên nhiều data nodes để đảm bảo tính sẵn sàng và hiệu suất.

2. **Quản lý tài nguyên và hiệu suất**:
   - **Cân bằng tải (Load Balancing)**: Coordinating nodes giúp cân bằng tải giữa các data nodes, đảm bảo rằng không có nút nào bị quá tải.
   - **Quản lý bộ nhớ và CPU**: Cấu hình bộ nhớ và CPU phù hợp cho các nút để tối ưu hóa hiệu suất.

3. **Bảo mật và Giám sát**:
   - **X-Pack**: Sử dụng X-Pack để bảo mật cụm, bao gồm xác thực, phân quyền và mã hóa giao tiếp.
   - **Giám sát**: Sử dụng các công cụ giám sát như Kibana và các API quản lý cụm để theo dõi tình trạng cụm và phát hiện sớm các vấn đề.

### Cài đặt và Quản lý Cụm Elasticsearch lớn

1. **Cài đặt Elasticsearch**:
   - Tải xuống và cài đặt Elasticsearch trên các máy chủ.
   - Cấu hình tệp `elasticsearch.yml` trên mỗi máy chủ để thiết lập tên cụm (`cluster.name`), tên nút (`node.name`), và các cài đặt mạng (`network.host`).

2. **Cấu hình cụm**:
   - **Discovery and Cluster Formation**: Cấu hình `discovery.seed_hosts` và `cluster.initial_master_nodes` để các nút có thể tìm thấy nhau và hình thành cụm.
   - **Minimum Master Nodes**: Đặt `discovery.zen.minimum_master_nodes` để tránh split-brain. Đối với một cụm lớn, giá trị này thường là `(N/2) + 1`, trong đó N là số master-eligible nodes.

3. **Quản lý và giám sát cụm**:
   - Sử dụng các API quản lý cụm như `_cat/nodes`, `_cluster/health`, và `_cluster/stats` để kiểm tra trạng thái và hiệu suất của cụm.
   - Thiết lập giám sát với Kibana và các công cụ giám sát khác để theo dõi hiệu suất và sức khỏe của cụm.

## Primary và replica shard

**Cluster Elasticsearch** là một tập hợp các nút (nodes) làm việc cùng nhau để lưu trữ và quản lý dữ liệu, cung cấp khả năng tìm kiếm và phân tích dữ liệu. Mỗi cluster có một tên duy nhất để phân biệt với các cluster khác.

### Thành phần của Cluster Elasticsearch

#### 1. Nodes (Nút)

- **Master-Eligible Node**: Chịu trách nhiệm quản lý trạng thái của cluster và thực hiện các tác vụ quản trị như tạo/xóa chỉ mục và phân phối các shard.
- **Data Node**: Chứa dữ liệu và thực hiện các hoạt động liên quan đến dữ liệu như CRUD (Create, Read, Update, Delete), tìm kiếm, và gộp (aggregation).
- **Ingest Node**: Xử lý dữ liệu trước khi lưu trữ, sử dụng các pipeline ingest để biến đổi dữ liệu.
- **Coordinating Node**: Định tuyến các yêu cầu từ người dùng đến các data nodes phù hợp, giảm tải các truy vấn và phân phối các thao tác bulk indexing.
- **Machine Learning Node**: Chạy các tác vụ học máy, yêu cầu X-Pack.
- **Alerting Node**: Chạy các tác vụ cảnh báo.

### Primary và Replica Shards trong Cluster

#### 1. Primary Shard

- **Định nghĩa**: Primary Shard là phân mảnh chính chứa dữ liệu gốc của chỉ mục.
- **Vai trò**:
  - **Lưu trữ dữ liệu gốc**: Primary shard chứa bản sao gốc của dữ liệu.
  - **Phân phối dữ liệu**: Khi dữ liệu mới được thêm vào, nó được phân phối đến primary shard dựa trên thuật toán băm.
- **Số lượng**: Số lượng primary shard được thiết lập khi tạo chỉ mục và không thể thay đổi sau đó.

#### 2. Replica Shard

- **Định nghĩa**: Replica Shard là bản sao của primary shard, được tạo ra để tăng cường khả năng chịu lỗi và cải thiện hiệu suất đọc.
- **Vai trò**:
  - **Khả năng chịu lỗi**: Nếu một primary shard bị lỗi, replica shard có thể thay thế để đảm bảo dữ liệu vẫn truy cập được.
  - **Cải thiện hiệu suất đọc**: Các truy vấn tìm kiếm có thể được phân phối đến các replica shard, giảm tải cho primary shard và cải thiện thời gian phản hồi.
- **Số lượng**: Số lượng replica shard có thể thay đổi sau khi chỉ mục được tạo.

### Cách hoạt động của Primary và Replica Shard trong Nodes và Cluster

#### 1. Thêm Dữ liệu (Indexing)

- Khi một tài liệu mới được thêm vào chỉ mục, nó được gửi đến primary shard tương ứng dựa trên thuật toán băm.
- Primary shard lưu trữ tài liệu và sau đó sao chép dữ liệu đến các replica shard.
- **Quy trình**:
  1. Tài liệu được gửi đến một coordinating node.
  2. Coordinating node định tuyến yêu cầu đến primary shard.
  3. Primary shard lưu trữ tài liệu và gửi bản sao đến các replica shard.

#### 2. Tìm kiếm Dữ liệu (Searching)

- Các truy vấn tìm kiếm có thể được gửi đến cả primary và replica shard để cân bằng tải và cải thiện hiệu suất.
- Elasticsearch tự động quản lý việc phân phối các truy vấn đến các shard phù hợp để tối ưu hóa thời gian phản hồi.
- **Quy trình**:
  1. Yêu cầu tìm kiếm được gửi đến một coordinating node.
  2. Coordinating node định tuyến yêu cầu đến các primary và replica shard.
  3. Các shard thực hiện tìm kiếm và trả kết quả về coordinating node.
  4. Coordinating node tổng hợp kết quả và trả về cho người dùng.

### Quản lý Shard trong Cluster

#### 1. Kiểm tra Trạng thái Shard

- Sử dụng API `_cat/shards` để kiểm tra trạng thái và vị trí của các shard trong cluster.
- **Ví dụ**:
  ```sh
  GET /_cat/shards?v
  ```

#### 2. Cấu hình Số lượng Replica

- Bạn có thể thay đổi số lượng replica shard bằng cách sử dụng API `_settings` của chỉ mục.
- **Ví dụ**:
  ```json
  PUT /my_index/_settings
  {
    "number_of_replicas": 2
  }
  ```

#### 3. Chuyển Shard giữa các Nút

- Elasticsearch tự động quản lý việc chuyển các shard giữa các nút để đảm bảo phân phối đều và tối ưu hóa hiệu suất.
- Khi một nút mới được thêm vào cluster hoặc một nút bị lỗi, Elasticsearch sẽ tự động phân phối lại các shard để duy trì tính sẵn sàng và hiệu suất.

### Ví dụ về Cụm Lớn (Large Cluster)

#### 1. Kiến trúc

- **Master Nodes**: 3 master-eligible nodes để đảm bảo tính sẵn sàng cao và tránh tình trạng split-brain.
- **Data Nodes**: Nhiều data nodes để phân phối tải công việc và dữ liệu.
- **Ingest Nodes**: Sử dụng ingest nodes để xử lý các pipeline dữ liệu trước khi lập chỉ mục.
- **Coordinating Nodes**: Sử dụng coordinating nodes để định tuyến các yêu cầu và giảm tải cho data nodes.

#### 2. Phân phối và Sao lưu dữ liệu

- **Primary Shards và Replica Shards**: Dữ liệu được chia thành các primary shard và replica shard để đảm bảo khả năng chịu lỗi và hiệu suất cao.
- **Phân phối trên nhiều nút**: Các shard được phân phối trên nhiều data nodes để đảm bảo tính sẵn sàng và hiệu suất.

### Giải thích về Primary Shards và Replica Shards với Ví dụ

**Cấu hình**:
- **Số lượng Primary Shards**: 2
- **Số lượng Replica Shards**: 2 cho mỗi Primary Shard

#### 1.Tổ chức Shards trong Cụm

Với cấu hình trên, chỉ mục sẽ có tổng cộng 6 shards:
- 2 primary shards
- 4 replica shards (2 replica cho mỗi primary shard)

#### 2.Phân phối Shards trên Các Nút (Nodes)

Giả sử cụm có 3 nút (Node A, Node B, Node C), các shards có thể được phân phối như sau:

- **Node A**: Primary Shard 1, Replica Shard 2
- **Node B**: Primary Shard 2, Replica Shard 1
- **Node C**: Replica Shard 1, Replica Shard 2

#### 3.Vấn đề Round-Robin Requests

**Round-robin** là một kỹ thuật phân phối tải công việc một cách đều đặn giữa các nút để tối ưu hóa hiệu suất và tránh quá tải cho bất kỳ nút nào.

**Cách hoạt động**

3.1. **Khi thêm dữ liệu (Indexing)**:
   - Yêu cầu gửi dữ liệu sẽ được phân phối đến các nút chứa primary shard tương ứng với dữ liệu đó.
   - Ví dụ, một tài liệu được lập chỉ mục vào Primary Shard 1 sẽ được gửi đến Node A, sau đó dữ liệu sẽ được sao chép đến Replica Shard 1 trên Node B và Replica Shard 1 trên Node C.

3.2. **Khi tìm kiếm dữ liệu (Searching)**:
   - Các yêu cầu tìm kiếm sẽ được phân phối đồng đều đến các nút chứa cả primary và replica shard.
   - Ví dụ, nếu có một yêu cầu tìm kiếm, lần đầu yêu cầu này có thể được gửi đến Node A (chứa Primary Shard 1), lần tiếp theo có thể được gửi đến Node B (chứa Replica Shard 1), và lần sau nữa có thể được gửi đến Node C (chứa Replica Shard 1).

#### 4.Lợi ích của Round-Robin

4.1. **Cân bằng tải**:
   - Kỹ thuật round-robin giúp phân phối đều các yêu cầu đến các nút khác nhau trong cụm, tránh việc một nút bị quá tải trong khi các nút khác không được sử dụng hết công suất.

4.2. **Cải thiện hiệu suất**:
   - Bằng cách phân phối các yêu cầu đều đặn, hệ thống có thể sử dụng tài nguyên của các nút một cách hiệu quả hơn, từ đó cải thiện hiệu suất tổng thể của hệ thống.

4.3. **Tăng khả năng chịu lỗi**:
   - Nếu một nút bị lỗi, các yêu cầu vẫn có thể được xử lý bởi các nút khác chứa replica shard, đảm bảo hệ thống vẫn hoạt động bình thường.
