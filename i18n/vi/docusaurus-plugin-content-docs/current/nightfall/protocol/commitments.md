---
id: commitments
title: Cam kết và Nullifier
sidebar_label: Commitment and Nullifiers
description: "Chuyển nhượng đơn lẻ và chuyển nhượng kép."
keywords:
  - docs
  - polygon
  - nightfall
  - commitment
  - nullifier
image: https://matic.network/banners/matic-network-16x9.png
---


## Cam kết là gì? {#what-are-commitments}
Cam kết là một mật mã cơ sở cho phép người dùng cam kết với một giá trị được chọn mà vẫn giữ bí mật với người khác, với khả năng tiết lộ giá trị đã cam kết trong tương lai. Cách này giữ được tính bảo mật về giá trị và người nhận.

Bất cứ khi nào người dùng thực hiện giao dịch bằng Nightfall, ví trình duyệt sẽ tính toán một Zero Knowledge Proof (ZKP) và tạo (hoặc hủy bỏ) một cam kết. Ví dụ, bạn tạo một cam kết khi nạp tiền hoặc chuyển nhượng và hủy bỏ một cam kết khi chuyển nhượng hoặc rút tiền.

Tính toán ZKP dựa trên [các circuit](../protocol/circuits.md) định nghĩa các quy tắc mà một giao dịch phải tuân theo để được coi là giao dịch đúng.

Cam kết được sử dụng nhằm giấu các thuộc tính sau:
- **Địa chỉ ERC của token**
- **Id token**
- **Giá trị**
- **Chủ sở hữu**

Cam kết được lưu trữ trong cấu trúc *Merkle Tree*. Gốc của *Merkle Tree* này được lưu trữ trên chuỗi.

![](../imgs/commitment.png)

### UTXO {#utxo}
Cam kết được tạo trong quá trình nạp và chuyển nhượng, đồng thời được sử dụng trong quá trình chuyển nhượng và giao dịch rút tiền. **Các cam kết không được tổng hợp lại với nhau**. Khi sử dụng một cam kết, giá trị của cam kết đã dùng bị hạn chế ở mức giá trị của tối đa hai cam kết bất kỳ đang sở hữu.

Circuit rút tiền và chuyển nhượng ZKP hiện tại được sử dụng trong Nightfall bị hạn chế ở mức 2 đầu vào - 2 đầu ra (chuyển nhượng/rút cam kết và thay đổi) trừ các khoản thanh toán. Nếu một tập hợp các cam kết của người giao dịch gồm các cam kết phần lớn là giá trị thấp (dust), có thể sẽ khó khăn khi tiến hành các giao dịch trong tương lai.

Quan sát các bộ giá trị sau đây

- **Bộ A**: [1, 1, 1, 1, 1, 1]
- **Bộ B**: [2, 2, 2]
- **Bộ C**: [2, 4]

Trong khi cả ba bộ có tổng tương đương, chuyển nhượng giá trị tối đa có thể giao dịch theo bộ *A*, *B*, và *C* lần lượt là 2, 4 và 6. Đây là một trong những lý do khiến giá trị cam kết lớn luôn được ưu tiên hơn. Chiến lược lựa chọn cam kết sử dụng giúp giảm bớt rủi ro này bằng cách ưu tiên dùng các cam kết giá trị nhỏ, đồng thời giảm thiểu việc tạo cam kết dust.


## Nullifier là gì? {#what-are-nullifiers}
**Nullifier** là kết quả khi kết hợp một cam kết và khóa nullifier. Một khi nullifier được phát trên chuỗi, cam kết được coi là đã sử dụng. Nullifier được lưu trữ trên chuỗi như một phần của dữ liệu gọi trong thời gian đề xuất khối.

![](../imgs/nullifier.png)



