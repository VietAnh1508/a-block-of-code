---
layout: post
title: Phân biệt các loại ví Bitcoin
category: []
tags: [bitcoin, blockchain, wallet, coinbase]
---

Khi bước chân vào thế giới của bitcoin, dù là kiếm tiền online (MMO), trading, holding... bạn sẽ luôn được hướng dẫn tạo một ví để chứa bitcoin (và chứa nhiều loại tiền điện tử khác, thường thì ví bitcoin sẽ support nhiều loại cryptocurrency khác nhau, trong bài này sẽ gọi chung là ví bitcoin). Chọn ví bitcoin là một quá trình chủ quan, phụ thuộc vào mục đích sử dụng và mức độ am hiểu của người dùng. Vì vậy, khó có thể gợi ý cho người khác một thương hiệu hay dự án ví cụ thể nào. Tuy nhiên, vẫn có thể phân loại các ví bitcoin dựa vào nền tảng và chức năng của chúng, qua đó làm rõ hơn về các loại ví đang tồi tại hiện nay.

### Dựa vào nền tảng sử dụng

#### Ví desktop

Ví desktop là dạng ví bitcoin đầu tiên, được tạo ra với vai trò một bản thực thi tham chiếu và được nhiều người sử dụng bởi những tính năng, khả năng tự quản và khả năng tự kiểm soát mà nó mang lại. Tuy nhiên, việc chạy ví trên các hệ điều hành như Windows hay MacOS mang lại nhiều rủi ro bảo mật.

#### Ví di động

Ví di động là dạng ví phổ biến nhất của bitcoin, chạy trên cả 2 nền tảng Android và iOS, thường là lựa chọn thích hợp cho người dùng mới. Nhiều ví dạng này được thiết kế đơn giản và dễ sử dụng, nhưng vẫn có những ví di động với đầy đủ tính năng dành cho người dùng nâng cao.

#### Ví web

Ví web được truy cập thông qua 1 trình duyệt web và lưu trữ ví của người dùng trên máy chủ do 1 bên thứ 3 sở hữu, mô hình này tương tự như webmail. Một số dịch vụ này sử dụng mã lệnh trên máy khách chạy trên trình duyệt của người dùng, do đó giữ quyền kiểm soát các khóa bitcoin trong tay người dùng.

Ví dụ: khi đăng kí một ví [ETH](https://www.myetherwallet.com/), trình duyệt web sẽ generate ra 1 file chứa script mở khóa, file này được lưu trữ ở phía người dùng. Mỗi khi đăng nhập, ví web ETH yêu cầu cung cấp file để mở khóa.

Tuy nhiên, không phải mọi ví web đều có tính năng này, một số ví chỉ yêu cầu cung cấp mật khẩu dạng text (điển hình như [blockchain.info](https://www.blockchain.com) hay [coinbase.com](https://www.coinbase.com/)).

Một số quan điểm cho rằng ví web mang lại sự tiện dụng nhưng lại lấy đi quyền kiểm soát khóa bitcoin từ tay người dùng. Do đó, không nên lưu trữ một lượng lớn bitcoin trên hệ thống của bên thứ 3.

Ngoài ra, các sàn giao dịch cũng cung cấp ví bitcoin trực tiếp, nhằm tạo điều kiện thuận lợi cho khách hàng, các ví này cung cấp hầu hết mọi tính năng cần thiết mà một ví bitcoin cần có. Tuy nhiên, không nên trữ quá nhiều tiền tại sàn, chỉ nên giữ một lượng vừa đủ để mua bán, còn lại nên rút về ví (sàn sập thì mất tiền :v).

Một số ví web cung cấp tính năng như một trình duyệt blockchain, hỗ trợ tìm các địa chỉ, giao dịch và các block, đồng thời thấy được các mối quan hệ cũng như dòng chảy tương tác giữa chúng. Các trình duyệt blockchain phổ biến:

- Bitcoin Block Explorer
- BlockCypher Explorer
- blockchain.info
- BitPay Insight

Các trình duyệt trên đều có chức năng tìm kiếm theo địa chỉ bitcoin, mã băm giao dịch, số block, mã băm block và lấy về những thông tin tương ứng từ mạng bitcoin.

#### Ví phần cứng

Ví phần cứng là các thiết bị vận hành một ví bitcoin độc lập và bảo mật chạy trên 1 phần cứng chuyên dụng. Chúng được vận hành qua cổng usb với 1 trình duyệt web trên máy tính hoặc qua kết nối near-field communication (NFC) trên 1 thiết bị di động. Do xử lý tất cả các hoạt động liên quan đến bitcoin trên phần cứng chuyên dụng nên các ví này được cho là rất bảo mật và phù hợp để lưu trữ lượng lớn bitcoin.

#### Ví giấy

Có thể in các khóa kiểm soát bitcoin ra để lưu trữ lâu dài. Các ví dạng này được gọi là ví giấy. Ví giấy tuy sử dụng công nghệ thấp nhưng lại có tính an toàn cao. Lưu trữ ngoại tuyến còn được gọi là _lưu trữ lạnh_ (cold storage).

### Dựa vào cấp độ tự quản của ví và cách chúng tương tác với mạng bitcoin

#### Phần mềm nút đầy đủ (full node)

Phần mềm đầy đủ, hay "nút đầy đủ" là phần mềm lưu trữ toàn bộ lích sử các giao dịch bitcoin, quản lý ví của người dùng và có thể khởi tạo giao dịch trực tiếp trên mạng bitcoin. Một nút đầy đủ xử lý tất cả các khía cạnh của giao thức và có thể độc lập xác thực toàn bộ blockchain cũng như một giao dịch bất kỳ. Full node thường được chạy bởi các thợ đào (miner).

#### Phần mềm rút gọn (lightweight node)

Phần mềm rút gọn, hay "phần mềm xác minh giao dịch giản lược" (simple payment verification - SPV), kết nối đến những nút bitcoin đầy đủ để truy cập các thông tin giao dịch bitcoin, nhưng lưu trữ cục bộ ví của người dùng và độc lập khởi tạo, xác thực, chuyển giao các giao dịch. Các phần mềm rút gọn tương tác trực tiếp với mạng bitcoin, không thông qua trung gian.

#### Phần mềm API của bên thứ 3

Là phần mềm tương tác với bitcoin thông qua 1 hệ thống các API của bên thứ 3, thay vì kết nối trực tiếp đến mạng bitcoin. Ví có thể do người dùng hoặc các máy chủ của bên thứ 3 lưu trữ, nhưng tất cả giao dịch đều phải đi qua 1 bên thứ 3.
