---
layout: post
title: Các giao dịch bitcoin (phần 1)
category: []
tags: [blockchain, transaction]
---

### Mua một ly cà phê

Một ngày cuối tuần, bạn đến quán cà phê quen thuộc. Đến quầy order thức uống, đập vào mắt bạn là thông báo: "Chấp nhận thanh toán bằng bitcoin". Có lẽ chủ quán thấy được cách mạng công nghiệp 4.0 nên bổ sung bitcoin vào lựa chọn thanh toán của quán :v. Giá của thức uống vẫn được liệt kê theo VND, nhưng tại quầy thanh toán, khách hàng có thể lựa chọn trả bằng tiền mặt hoặc bitcoin. Bạn gọi 1 ly cà phê và nhân viên nhập vào máy tính như thường lệ. Sau đó, hệ thống máy bán hàng tự động quy đổi tổng giá tiền từ VND sang bitcoin theo tỉ giá hiện hành và hiển thị giá bằng cả 2 loại tiền:

<p style="text-align:center">Tổng: 30,000 VND - 0,0002 BTC</p>

Hệ thống thanh toán cũng tự động tạo ra một mã QR đặc biệt chứa một _yêu cầu thanh toán_. Khác với mã QR đơn thuần chỉ chứa địa chỉ bicoin đích, yêu cầu thanh toán là 1 URL được mã hóa dưới dạng QR trong đó chứa 1 địa chỉ bitcoin, khoản tiền cần thanh toán và 1 dữ liệu mô tả chung, chẳng hạn như "Quán cà phê XYZ".

Bạn dùng điện thoại, mở app bitcoin (ví di động) và quét mã QR trên màn hình, ví di động của bạn hiển thị một khoản thanh toán với nội dung "Send 0,0002BTC to XYZ Coffee", bạn chỉ việc nhấn Send để thực hiện thanh toán. Vày giây sau, nhân viên nhìn thấy thông báo trên máy, giao dịch hoàn tất.

Trên đây là một ví dụ nhỏ về quá trình thực hiện giao dịch bitcoin. Chúng ta sẽ tìm hiểu về những gì thật sự diễn ra bên dưới. Nói 1 cách đơn giản, khi bạn thực hiện 1 giao dịch, [phần mềm ví bitcoin]({{ site.baseurl }}{% post_url 2018-10-18-phan-loai-vi-bitcoin %}){:target="\_blank"} sẽ phát ra 1 thông báo cho mạng lưới biết rằng chủ sở hữu của 1 lượng bitcoin đã cho phép chuyển giao lượng bitcoin đó cho người khác.

### Đầu vào và đầu ra giao dịch

Các giao dịch được ghi lại giống như các dòng trong 1 [sổ cái kép]({{ site.baseurl }}{% post_url 2018-10-27-ke-toan-tam-phan %}){:target="\_blank"}. Mỗi giao dịch chứa một hoặc nhiều "đầu vào", ở đầu kia của giao dịch, có một hoặc nhiều "đầu ra". Những đầu vào và đầu ra này không nhất thiết phải có tổng bằng nhau. Tổng các đầu ra luôn nhỏ hơn tổng các đầu vào, phần chênh lệch này thể hiện mức "_phí giao dịch_" ngầm định, phần phí này sẽ được trả cho các thợ đào khi họ đưa các giao dịch vào sổ cái (blockchain).

Giao dịch này còn chứa bằng chứng quyền sở hữu đối với từng lượng bitcoin (đầu vào) đang được chi tiêu, bằng chứng này được thể hiện dưới dạng chữ ký số của chủ sở hữu và có thể được xác nhận bởi bất cứ ai.

Khoản thanh toán 0,0002 BTC của bạn cho quán cà phê lấy đầu ra của giao dịch trước đó làm đầu vào của nó. Giả sử bạn dùng tiền mặt mua bitcoin từ trước, giao dịch này tạo ra 1 giá trị bitcoin bằng khóa của bạn. Giao dịch mới của bạn với quán cà phê sẽ được tham chiếu đến giao dịch này, lấy đó làm đầu vào và tạo các đầu ra, đồng thời nhận tiền thừa trả lại (nếu có). Cụ thể hơn, giao dịch "Mua cà phê tại XYZ" sẽ có các đầu vào tham chiếu đến địa chỉ bitcoin của bạn, còn đầu ra tham chiếu đến địa chỉ của quán.

Đến đây có thể bạn sẽ thắc mắc: tiền mã hóa vẫn phải tạo tiền thừa trả lại sao? Các giao dịch được thiết kế khá tương đồng với tiền giấy. Nếu bạn mua một món đồ có giá 20k và dùng tờ 50k để trả, người bán sẽ trả lại cho bạn 30k. Quá trình này được áp dụng cho các đầu vào của giao dịch bitcoin: nếu bạn mua một món đồ với giá 5 BTC, nhưng bạn chỉ có một đầu vào 20 BTC để sử dụng, ví bitcoin sẽ tạo ra một đầu ra trị giá 5 BTC cho cửa hàng và một đầu ra 15 BTC gửi về cho chính bạn (trừ đi phần phí giao dịch nếu có). Điều quan trọng cần lưu ý: địa chỉ tiền thừa trả lại không nhất thiết phải là địa chỉ đầu vào, vì các lý do bảo mật. Thông thường, các phần mềm ví bitcoin sẽ tạo ra các địa chỉ mới khác nhau cho từng giao dịch (quá trình tạo địa chỉ sẽ bàn chi tiết hơn ở các bài viết sau).

### Chuỗi giao dịch

Các giao dịch này tạo thành 1 chuỗi, trong đó đầu ra của giao dịch trước tương ứng với đầu vào của các giao dịch mới hơn. Khóa của bạn cung cấp chữ ký để mở khóa đầu ra của các giao dịch trước, qua đó chứng minh với mạng bitcoin rằng bạn sở hữu số tiền này. Khi bạn dùng bitcoin để trả cho ly cà phê, lượng tiền này trở thành đầu ra của bạn và là đầu vào của quán cà phê, được gán bởi địa chỉ của quán, hành động này "ràng buộc" đầu vào đó chỉ có thể tiếp tục được chi tiêu khi chủ quán cung cấp một chữ ký hợp lệ.

### Các dạng giao dịch thường gặp

Dạng giao dịch phổ biến nhất là một khoản thanh toán đơn giản từ địa chỉ này đến địa chỉ khác, thường bao gồm tiền thừa trả lại cho chủ sở hữu ban đầu. Dạng giao dịch này có 1 đầu vào và 2 đầu ra.

Dạng giao dịch phổ biến khác là gộp nhiều đầu vào thành một đầu ra duy nhất. Dạng này tương ứng với tình huống bạn gom nhiều tờ tiền với mệnh giá nhỏ để trả cho một món hàng có giá trị lớn hơn.

Một dạng giao dịch thường thấy khác là phân phối một đầu vào cho nhiều đầu ra đại diện cho nhiều người nhận. Các thực thể thương mại thường sử dụng dạng giao dịch này để phân phối tiền, chẳng hạn như trả lương cho nhân viên.
