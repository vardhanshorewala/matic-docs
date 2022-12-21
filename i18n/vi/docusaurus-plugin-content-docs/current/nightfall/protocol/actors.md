---
id: actors
title: Tác nhân
sidebar_label: Actors
description: "Các loại Tác nhân trên Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - transactor
  - proposer
  - challenger
  - liquidity
  - provider
image: https://matic.network/banners/matic-network-16x9.png
---

Có bốn tác nhân tham gia vào mạng lưới:

- [Người giao dịch](#transactor)
- [Người đề xuất](#proposer)
- [Người tuyên bố](#challenger)

## Người giao dịch {#transactor}
Người giao dịch là khách hàng thông thường của dịch vụ. Họ muốn thực hiện giao dịch, ví dụ Nạp tiền, Chuyển nhượng và Rút tiền một cách riêng tư. Những khách hàng này thường sử dụng ví web hoặc một server chuyên dụng (Máy khách) thực hiện Bằng chứng ZK để tạo giao dịch.

## Người đề xuất {#proposer}
Người đề xuất thu thập giao dịch từ khách hàng và đề xuất các cập nhật mới cho trạng thái của hợp đồng Phòng vệ. Với thuật ngữ "trạng thái", chúng tôi đề cập cụ thể đến các biến lưu trữ liên quan tới Giao dịch ZKP: hàm triệt tiêu và gốc cam kết. Đề xuất cập nhật có chứa một số giao dịch, được đưa vào thành một Khối Lớp 2. Chỉ một hàm băm của trạng thái cuối cùng còn tồn tại sau khi đã xử lý tất cả giao dịch trong Khối sẽ được lưu lại trên chuỗi. Giao dịch sẽ trở thành giao dịch cuối sau kỳ hạn 1 tuần.

Ai cũng có thể trở thành Người đề xuất nhưng phải niêm yết một số cổ phần. Cổ phần là nhằm khuyến khích hành vi tốt. Người đề xuất kiếm tiền bằng cách cung cấp các Khối đúng và thu phí từ người giao dịch. Họ cũng phần nào tương tự như Thợ đào trong một blockchain thông thường.

## Người tuyên bố {#challenger}
Người tuyên bố sẽ giám sát tính chính xác của khối được đề xuất trong vòng một tuần sau khi khối được gửi đi. Ai cũng có thể là Người tuyên bố. Người tuyên bố lấy cổ phần mà người đề xuất đã niêm yết vào lúc xây dựng khối khi người tuyên bố gửi thành công một thử thách.


## Lưu ý {#notes}
Trong cài đặt chuẩn của Polygon, cả Người đề xuất và Người tuyên bố đều giảm tải một số chức năng thành một môđun thông thường gọi là Optimist. Môđun Optimist này cung cấp dịch vụ cho một số Người đề xuất và Người tuyên bố, ví dụ tạo và thử thách các khối (Người đề xuất và Người tuyên bố cần ký các giao dịch này), đồng bộ các sự kiện blockchain v.v.

Ngoài các Tác nhân đã mô tả bên trên, còn một tác nhân nữa là Máy khách. Máy khách có vai trò như một dịch vụ đáng tin cậy thu thập giao dịch người dùng, thay mặt họ thực hiện Bằng chứng ZK, gửi giao dịch tới Người đề xuất, lắng nghe các sự kiện Blockchain v.v. Tóm lại, Máy khách hoạt động như trình chuyển tiếp đáng tin cậy dành cho một nhóm những người dùng tin tưởng lẫn nhau và muốn giảm tải việc tính toán bằng chứng nặng nề.

Phương án thay thế dành cho Máy khách là sử dụng ví trình duyệt, một dịch vụ không có server mà Polygon cung cấp. Ví này quản lý toàn bộ các hoạt động giao dịch dành cho một người dùng đơn lẻ, đồng thời duy trì quyền riêng tư.
