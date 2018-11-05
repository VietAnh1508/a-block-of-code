---
layout: post
title: Các giao dịch bitcoin (phần 2)
category: []
tags: [blockchain, bitcoin, transaction]
---

Ở [phần 1]({{ site.baseurl }}{% post_url 2018-10-30-cac-giao-dich-bitcoin-phan-1 %}){:target="\_blank"}, mình đã được giới thiệu một giao dịch blockchain cơ bản, mua cà phê. Phần này, ta sẽ tìm hiểu sâu hơn về quá trình tạo giao dịch từ các đầu vào và đầu ra.

### Giao dịch được tạo như thế nào?

Ứng dụng ví của bạn sẽ chứa toàn bộ các logic nhằm chọn các đầu vào và đầu ra phù hợp để tạo một giao dịch đúng yêu cầu. Bạn chỉ cần xác định địa chỉ đích và lượng tiền muốn chuyển, ví bitcoin sẽ lo phần còn lại. Điều quan trọng cần lưu ý, ví bitcoin có thể tạo ra giao dịch ngay cả khi không có kết nối mạng.

#### Chọn đầu vào

Bước đầu tiên, ứng dụng ví sẽ tìm các đầu vào có thể thanh toán được khoản tiền mà bạn phải trả cho ly cà phê. Hầu hết các ví đều theo dõi tất cả các đầu ra hiện có của địa chỉ trong ví (là khoản tiền mà bạn nhận được từ các giao dịch trước đó). Nếu ứng dụng bitcoin hoạt động như một [phần mềm nút đầy đủ]({{ site.baseurl }}{% post_url 2018-10-18-phan-loai-vi-bitcoin %}){:target="\_blank"}, nó sẽ chứa bản sao của mọi đầu ra chưa được chi tiêu từ mọi giao dịch trong blockchain, nhờ đó có thể nhanh chóng chọn ra các đầu vào hợp lệ. Tuy nhiên, nút đầy đủ tốn rất nhiều dung lượng, không phù hợp với các ứng dụng ví của người dùng, nên hầu hết các ví chỉ chạy phần mềm "rút gọn". Phần mềm rút gọn truy vấn mạng bitcoin để lấy các thông tin này thông qua API của các nhà cung cấp khác nhau (vì mọi giao dịch đã được lưu lại trong blockchain, sau đó được phân tán trên khắp mạng lưới). Các API này sẽ trả về tất cả các đầu ra giao dịch chưa chi tiêu của một địa chỉ. Ví dụ:

```bash
$ curl https://blockchain.info/unspent?active=1Cdid9KFAaatwczBwBttQcwXYCpvK8h7FK

{
    "unspent_outputs": [
        {
            "tx_hash": "f2c245c38672a5d8fba5a5caa44dcef277a52e916a0603272f91286f2b052706",
            "tx_hash_big_endian": "0627052b6f28912f2703066a912ea577f2ce4da4caa5a5fbd8a57286c345c2f2",
            "tx_index":  47854970,
            "tx_output_n": 1,
            "script": "76a9147f9b1a7fb68d60c536c2fd8aeaa53a8f3cc025a888ac",
            "value": 8450000,
            "value_hex": "0080efd0",
            "confirmations": 271567
        },
        ...
    ]
}
```

Ở ví dụ trên, ta dùng _cURL_ để lấy thông tin đầu ra chưa chi tiêu của địa chỉ 1Cdid9KFAaatwczBwBttQcwXYCpvK8h7FK từ máy chủ blockchain.info. Kết quả trả về bao gồm dữ liệu tham chiếu đến giao dịch chứa đầu ra chưa chi tiêu này và giá trị của nó tính bằng satoshi `"value": 8450000` ~ 0,0845 BTC. Với thông tin này, ứng dụng ví của bạn có thể tạo ra một giao dịch để chuyển khoản tiền này đến chủ sở hữu mới.

Đầu ra chưa chi tiêu này có đủ bitcoin để thanh toán cho ly cà phê có giá 0,0002 BTC. Nếu không đủ, ví sẽ phải tiếp tục tìm kiếm qua nhiều đầu ra chứa những chi tiêu khác, giống như bạn gom tiền lẻ trong túi cho tới khi đủ tiền để trả cho món hàng.

#### Tạo đầu ra

Đầu ra giao dịch được tạo dưới dạng một "kịch bản". Kịch bản này nói rằng "Đầu ra này sẽ thuộc về bất cứ ai có thể trình ra chữ ký tương ứng với địa chỉ công khai của quán cà phê XYZ". Do chủ quán có ví chứa các khóa tương ứng với địa chỉ đó, nên chỉ có chủ quán có thể nhận lượng tiền này.

Giao dịch này sẽ có một đầu ra thứ 2, bởi vì đầu vào 0,0845 BTC nhiều hơn giá của ly cà phê 0,0002 BTC, ta sẽ cần 0,0848 BTC tiền thừa trả lại. Ví của bạn sẽ tạo ra khoản thanh toán tiền thừa trong cùng một giao dịch. Về bản chất, phần mềm ví chia tiền thành 2 khoản thanh toán: một cho quán cà phê và một trả về cho chính nó. Bạn có thể sử dụng đầu ra này cho lần giao dịch sau.

Cuối cùng, để giao dịch bitcoin có thể được xử lý nhanh chóng, ứng dụng ví sẽ thêm vào một khoản phí nhỏ. Phí này không được ghi rõ trong giao dịch mà được ngầm định trong sự chênh lệch giữa đầu vào và đầu ra. Phần kết quả chênh lệch chính là _phí giao dịch_ được các thợ đào thu làm lệ phí xác thực và đưa giao dịch vào blockchain. Lưu ý rằng phần phí này không phụ thuộc vào số tiền giao dịch, nhưng dựa vào dung lượng dữ liệu của giao dịch.

### Thêm giao dịch vào blockchain

Giao dịch của bạn đã chứa mọi yếu tố cần thiết để xác nhận quyền sở hữu với số tiền trong đó và trao nó cho chủ sở hữu mới. Tiếp theo, giao dịch này phải được truyền tới mạng bitcoin, nơi nó sẽ trở thành một phần của blockchain.

#### Giao dịch được phán tán như thế nào

Ứng dụng ví của bạn có thể gửi giao dịch mới đến một node bất kỳ có kết nối với nó thông qua mọi hình thức: WiFi, dây cáp... Ví bitcoin của bạn không cần phải kết nối trực tiếp đến ví của chủ quán cà phê, cũng không cần phải sử dụng đường truyền Internet của quán. Khi một node bitcoin nhận được 1 giao dịch hợp lệ mà nó chưa từng thấy trước đây, nó sẽ lập tức chuyển giao dịch này đến tất cả các node có kết nối với nó, kỹ thuật phân tán này được gọi là [flooding](<https://en.wikipedia.org/wiki/Flooding_(computer_networking)>){:target="\_blank"}.

Nếu ứng dụng ví của chủ quán có kết nối trực tiếp với ứng dụng ví của bạn, có thể nó sẽ là node đầu tiên nhận được giao dịch. Tuy nhiên, nếu ví của bạn kết nối đến các node khác, giao dịch này cũng sẽ đến được ví của chủ quán trong vài giây. Ví của chủ quán có thể ngay lập tức xác nhận giao dịch này là thanh toán gửi đến cho mình, vì nó chứa các đầu ra có thể mở bằng khóa của chủ quán.

Lúc này, giao dịch của bạn đã được phán tán trên mạng bitcoin, nhưng phải đến khi được xác nhận và được đưa vào một block thông qua quá trình "đào" (mining) thì nó mới trở thành một phần của blockchain.
