---
id: circuits
title: Circuit và Giao dịch
sidebar_label: Circuits and Transactions
description: "Các loại Circuit trong Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - circuits
  - deposit
  - transfer
image: https://matic.network/banners/matic-network-16x9.png
---

Circuit được sử dụng để xác định các quy tắc mà giao dịch phải tuân theo để được coi là giao dịch đúng. Thường có ba loại circuit, mỗi circuit ứng với một loại giao dịch:

- [Nạp tiền](#deposit)
- [Chuyển nhượng](#transfer)
- [Rút tiền](#withdraw)

Mọi giao dịch đều có Bằng chứng ZK tuân theo các hạn chế được chỉ định trong các circuit này. Người dùng xây dựng bằng chứng này bằng Ví, hoặc thông qua máy chủ Máy khách. Bằng chứng chỉ được tạo nếu thỏa mãn tất cả các trường hợp sau:

- [Cam kết](./commitments#what-are-commitments) mới hợp lệ
- [Cam kết](./commitments#what-are-commitments) cũ hợp lệ và do người gửi sở hữu
- [Nullifier] (./commitments#what-are-nullifiers) hợp lệ
- Đường dẫn/gốc Merkle Tree hợp lệ
- Bản mã có chứa cam kết hợp lệ


## Nạp tiền {#deposit}
Việc nạp chuyển đổi các token ERC hiển thị công khai thành cam kết token có cùng giá trị hoặc id token như id của token ban đầu, và khóa công khai Nightfall của chủ sở hữu cam kết dự định.

Một Bằng chứng ZK về khoản nạp cho thấy người thử đã tạo một cam kết hợp lệ$Z_A$ with a public key $pk_A$.

Sau đó circuit sẽ kiểm tra xem $Z_A$ == H(@ | ɑ | $pk_A$| σ Thông tin bị rò rỉ về giao dịch nạp bao gồm địa chỉ đã khai thác cam kết mới và địa chỉ, giá trị của token ERC đang được sử dụng.

![](../imgs/deposit.png)

## Chuyển nhượng {#transfer}
Chuyển nhượng cho phép chuyển giao tối đa hai cam kết của cùng tài sản giữa hai bên bằng cách gỡ bỏ các cam kết trước và tạo thành tối đa hai cam kết mới:
- Một được gửi đến người nhận, bao gồm giá trị của số tiền đã chuyển
- Một được tạo với giá trị của thay đổi (chênh lệch giữa tổng giá trị của cam kết đã sử dụng trừ đi giá trị đã chuyển nhượng) và do người truyền đi sở hữu.

Bằng chứng ZK chuyển nhượng chứng minh rằng người dùng đã gỡ bỏ tối đa hai cam kết cũ tồn tại trong Merkle Tree, tạo một cam kết mới và mã hóa thông tin cho người nhận.

Trong hai trường hợp, thông tin bị rò rỉ sẽ là một địa chỉ Ethereum có cam kết đã bị bỏ trong số những cam kết thuộc sở hữu của người truyền đi và có cam kết mới được tạo ra. Thông tin về chủ sở hữu mới, những cam kết nào đã được sử dụng hoặc số lượng được chuyển vẫn được giữ riêng tư.

Sơ đồ đầu tiên minh họa các bước hủy bỏ một cam kết (hoặc các cam kết) hiện hữu và thêm thông tin vào cấu trúc dữ liệu `transaction`.

![](../imgs/transfer_a.png)

Sơ đồ thứ hai minh họa các bước cần thiết để tạo và mã hóa các cam kết mới tạo.

![](../imgs/transfer_b.png)

## Rút tiền {#withdraw}
Rút tiền là hoạt động hủy bỏ một cam kết Nightfall hiện hữu và chuyển đổi nó thành các token ERC hiển thị công khai với cùng giá trị và id token như cam kết đã đốt. Rút tiền là hoạt động đối lập với Nạp tiền. Tương tự như chuyển nhượng, rút tiền chấp nhận đầu vào tối đa là hai cam kết.

Bằng chứng ZK về rút tiền chứng minh rằng người dùng đã hủy tối đa hai cam kết cũ từng tồn tại trong Merkle Tree.

Thông tin bị rò rỉ trong hoạt động rút tiền bao gồm địa chỉ của địa chỉ đã rút cam kết và giá trị/id token cũng như địa chỉ của token đã rút.

![](../imgs/withdraw.png)

### Thời kỳ xét duyệt {#cooling-off-period}

Việc rút tiền cần có thời kỳ xét duyệt `COOLING OFF` kéo dài một tuần để hoàn thành. Nguyên nhân là do bản chất optimistic của Nightfall, vì một khối mới sẽ được giả định là đúng cho đến khi một số người tuyên bố gửi một bằng chứng gian lận. Số tiền được giữ cho đến hết một tuần mới có thể rút về L1.

# Phí {#fees}

Người đề xuất nhận giao dịch đến và đưa vào khối L2 với một khoản phí. Có hai loại phí khác nhau phải trả cho đề xuất, phụ thuộc vào giao dịch:
- Hoạt động nạp thanh toán phí ETH trực tiếp trong L1.
- Hoạt động chuyển nhượng và rút tiền thanh toán phí trong MATIC trong L2.
