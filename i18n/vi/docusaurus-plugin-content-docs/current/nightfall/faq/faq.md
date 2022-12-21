---
id: faq
title: HỎI ĐÁP
sidebar_label: FAQ
description: Các câu hỏi thường gặp về Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

:::tip

Nếu không thấy câu hỏi của mình trong danh sách này, bạn hãy gửi câu hỏi về <ins>**[Server discord của Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR)**</ins>.
:::

## Tôi có thể tìm Hợp đồng Thông minh ở đâu? {#where-can-i-find-the-smart-contracts}

Hợp đồng Polygon Nightfall đã được triển khai trên [mạng thử nghiệm Goerli](../deployments/testnet.md) và [mạng chính](../deployments/mainnet.md).

## Trạng thái kiểm tra bảo mật của Polygon Nightfall là gì? {#what-s-the-state-of-polygon-nightfall-s-security-audit}
Polygon Nightfall hiện đang thực hiện đợt kiểm tra bảo mật, theo kế hoạch sẽ hoàn thành vào quý 3. Trong thời gian đó, một số hạn chế đã được bổ sung vào giao thức:

- Người đề xuất đơn lẻ đang hoạt động và do Polygon quản lý
- [Số tiền nạp vào và rút ra bị hạn chế](../tools/nightfall-wallet.md#deposit-and-withdraw-restrictions)

## Cách thức để thiết lập Ví Nightfall của tôi? {#how-do-i-set-up-my-nightfall-wallet}
Toàn bộ hướng dẫn về ví có tại [đây](../tools/nightfall-wallet.md) với đầy đủ chi tiết về cách bắt đầu Polygon Nightfall bằng ví Polygon Nightfall.

## Cách thức để kết nối một Ví cứng Ledger đến Ví Nightfall ? {#how-do-i-connect-a-ledger-hardware-wallet-to-nightfall-wallet}
Trong hướng dẫn về ví sẽ có một phần giải thích về [cách kết nối Ví cứng Ledger với Metamask](../tools/nightfall-wallet.md#how-to-connect-a-ledger-hardware-wallet-to-nightfall).

## Giao dịch chuyển trên Mạng Polygon Nightfall từ khi bắt đầu đến khi kết thúc mất bao lâu? {#how-long-do-transfers-take-on-polygon-nightfall-network-from-start-to-finish}
Người đề xuất hiện tại nhận giao dịch từ người dùng và tạo thành khối chứa tối đa 32 giao dịch. Ngay khi thu thập đủ giao dịch để xây khối, giao dịch sẽ được xử lý.

Ngoài ra, có giới hạn trên trong kỳ tạo khối để cứ mỗi 6 giờ lại có ít nhất một khối được đề xuất (bất kể số lượng giao dịch mà người đề xuất thu thập).

## Tôi có thể giao dịch với ai? {#who-can-i-transact-with}
Để chuyển nhượng trong Polygon Nightfall, bạn chỉ cần `Destination Wallet Address`. Đọc hướng dẫn về ví nhằm hiểu [cách chia sẻ Địa chỉ ví](../tools/nightfall-wallet.md#your-wallet-address) để nhận tiền.

## Các cam kết được sao lưu ở đâu? {#where-are-commitments-backed-up}

Bằng chứng Zero Knowledge được tính toán trong trình duyệt sao cho khóa bí mật vẫn ở lại với bạn và ví tiếp tục theo dõi bất kỳ cam kết nào bạn sở hữu trong IndexedDb. Bất kỳ ai có quyền truy cập dữ liệu này đều có thể tìm ra cam kết của bạn, mặc dù họ không thể trộm chúng vì không có chìa khóa. Khóa chỉ được giải mã khi bạn nhập vào từ gợi nhớ. Vì vậy bạn chỉ nên sử dụng ví trên một chiếc máy mà mình tin tưởng.

Hiện tại, dữ liệu này không được xuất ra ở bất kỳ đâu. Vì vậy, nếu bạn sử dụng trình duyệt trên một máy khác, bạn sẽ không có quyền truy cập vào cam kết của mình trừ khi bạn chuyển nhượng nội dung IndexedDB. Chúng tôi cung cấp cơ chế để xuất và nhập cam kết thông qua ví.

## Quyền tiêng tư của giao dịch {#privacy-of-transactions}
Cần phải hiểu rằng các giao dịch Nạp tiền và Rút tiền không phải riêng tư. Nguyên nhân là do chúng tương tác với Lớp 1 và Lớp 1 không riêng tư. Điều này đồng nghĩa với việc khi bạn tạo cam kết Lớp 2, mọi người đều biết về nó và biết nó chứa bao nhiêu. Tương tự, nếu bạn trả một token về Lớp 1 bằng cách hủy cam kết Lớp 2, mọi người đều biết ai nhận và nhận bao nhiêu.

Tính riêng tư chỉ có từ các giao dịch trong Lớp 2. Từ góc độ của blockchain Ethereum, đây mới là riêng tư hoàn toàn. Dữ liệu duy nhất bị rò rỉ là địa chỉ IP của bạn khi bạn gửi giao dịch chuyển khoản đến Người đề xuất Khối. Với Beta đời đầu, Polygon chỉ vận hành Người đề xuất.


## Cách thức để rút tiền? {#how-to-withdraw-funds}
Có thể rút tiền bằng ví Polygon Nightfall. Việc rút tiền có kỳ hạn **một tuần** kể từ thời điểm khối có chứa giao dịch rút tiền được tạo. Khi kỳ hạn này kết thúc, bạn có thể hoàn tất việc rút tiền để tiền được gửi đến tài khoản Ethereum của bạn.

## Giao dịch trong Nightfall có giá bao nhiêu? {#how-much-will-transactions-cost-on-nightfall}
Có hai loại giao dịch với chi phí khác nhau:

- Giao dịch trên chuỗi: Các giao dịch này được gửi đến hợp đồng thông minh và bạn phải trả phí gas trên Ethereum để có thể khai thác. Bất kỳ người đề xuất nào cũng có thể lấy giao dịch này và đặt nó vào một khối. Hiện tại, `deposit`và `finalize withdrawal`là các giao dịch trên chuỗi.
- Giao dịch ngoài chuỗi : Những giao dịch này được gửi trực tiếp đến người đề xuất. Hiện tại, cả `transfer`và `withdrawals` đều được cấu hình dưới dạng giao dịch ngoài chuỗi.

## Tôi có thể dùng token nào trên Mạng Nightfall? {#which-tokens-can-i-use-on-nightfall-network}
Các token sau đây đang hoạt động trên Nightfall:

- MATIC
- WETH
- DAI
- USDC

## Tôi có cần token MATIC để sử dụng Nightfall không? {#do-i-need-matic-tokens-to-use-nightfall}
Có. Bạn sẽ cần nạp một số token MATIC trên Nightfall để có thể thanh toán cho `transfers` và `withdrawals`.

## Tôi có thể gửi báo cáo lỗi hoặc liên hệ Nightfall để được trợ giúp ở đâu? {#where-can-i-submit-a-bug-report-or-contact-nightfall-for-additional-help}
Cách tốt nhất là tham gia [Server discord của Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR) và gửi câu hỏi của bạn.
