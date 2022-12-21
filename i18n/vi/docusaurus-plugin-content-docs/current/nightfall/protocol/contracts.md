---
id: contracts
title: Hợp đồng Thông minh
sidebar_label: Smart Contracts
description: "Phòng vệ, đề xuất, thử thách và Tính toán Merkle Tree."
keywords:
  - docs
  - polygon
  - nightfall
  - smart
  - contracts
  - shield
image: https://matic.network/banners/matic-network-16x9.png
---

Hợp đồng định nghĩa các quy tắc mà mỗi tác nhân Nightfall cần tuân theo để hoạt động trong mạng lưới. Hợp đồng Thông minh bao gồm:

- [Shield.sol](#shield)
- [Proposers.sol](#proposers)
- [Challenges.sol](#challenges)
- [MerkleTree_Computations.sol](#merkletree_computations)

## Phòng vệ {#shield}
Hợp đồng này cho phép người dùng gửi giao dịch để Người đề xuất xử lý. Nếu là Giao dịch nạp tiền, sẽ có khoản thanh toán. Đồng thời, nó cũng cho phép tất cả mọi người yêu cầu cập nhật trạng thái hợp đồng Phòng vệ (gốc cam kết và danh sách nullifier). Khi trạng thái được cập nhật, hoạt động rút tiền bất kỳ trong phần cập nhật sẽ được xử lý.

Không cần phải đăng một chuyển nhượng hoặc giao dịch rút tiền lên blockchain: đây chỉ đơn giản là một diễn đàn dành cho  người đề xuất thu thập giao dịch và kết hợp chúng vào một Khối Lớp 2.

Vì Nightfall tương tác với các hợp đồng ERC thực, các kiểm tra sau sẽ không được thực hiện theo cách riêng tư:

- Trong quá trình **Nạp/Rút tiền**, địa chỉ token ERC phải hợp lệ.
- Trong quá trình **Nạp**, người dùng có số dư hoặc sở hữu token để tạo ra cam kết.

## Người đề xuất {#proposers}
Hợp đồng gồm chức năng đăng ký, hủy đăng ký, thanh toán và xoay chuyển người đề xuất, đề xuất một Khối Lớp 2 mới vào blockchain. Phiên bản Nightfall đầu tiên chỉ chấp nhận một Người đề xuất Boot đơn lẻ do Polygon vận hành. Các phiên bản sắp tới sẽ dỡ bỏ hạn chế này và cho phép nhiều người đề xuất.

## Thử thách {#challenges}
Chức năng cho phép một Khối bị xem là không đúng và bị thử thách.

## MerkleTree_Stateless {#merkletree_stateless}
Một phiên bản không có trạng thái (chức năng thuần túy) của `MerkleTree.sol` gốc, được sử dụng bởi `Challenges.sol` để giúp tính toán các thử thách khối trên chuỗi.

## Các hợp đồng khác {#other-contracts}
- `Utils.sol`- tập hợp chức năng được sử dụng trong nhiều hợp đồng hoặc sẽ ảnh hưởng đến khả năng đọc mã nếu được để trực tiếp.
- `Config.sol`- giữ hằng số, tương tự như một tệp tin cấu hình Node.js.
- `Structures.sol`- định nghĩa các struct, enum, sự kiện, hoán đổi toàn cục và các biến số trạng thái. Nhờ đó, việc tìm kiếm dễ dàng hơn.

## Khả năng nâng cấp {#upgradability}
Tối thiểu vào lúc ban đầu, Polygon giữ lại khả năng nâng cấp hợp đồng Nightfall sau khi triển khai. Chúng tôi sử dụng [Plugin nâng cấp](https://docs.openzeppelin.com/upgrades-plugins/1.x/) Openzeppelin để Truffle làm điều đó.

Polygon sử dụng một môđun [Trình triển khai](https://github.com/EYBlockchain/nightfall_3/tree/master/nightfall-deployer) để nâng cấp hợp đồng. `deployer` có 4 lần di chuyển được lưu trữ trong thư mục di chuyển. Ba lần di chuyển đầu tiên là sự triển khai "bình thường" đối với bộ hợp đồng Polygon Nightfall. Chúng đảm bảo chắc chắn rằng tất cả hợp đồng (nhưng không phải thư viện) được triển khai có proxy để cho phép nâng cấp hợp đồng sau này. Lần di chuyển thứ tư nhằm nâng cấp hợp đồng.
