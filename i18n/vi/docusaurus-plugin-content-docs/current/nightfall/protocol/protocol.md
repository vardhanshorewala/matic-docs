---
id: protocol
title: Giao thức Nightfall
sidebar_label: Nightfall Protocol
description: "Quy trình Nightfall."
keywords:
  - docs
  - polygon
  - nightfall
  - protocol
  - chain
  - block
  - structure
  - layer
image: https://matic.network/banners/matic-network-16x9.png
---

Chúng tôi giả sử rằng có ít nhất 1 Người đề xuất đã đăng ký với hệ thống, đăng lên một Cổ phần tối thiểu.

## Đăng giao dịch {#transaction-posting}
Có hai cơ chế để đăng giao dịch mới:

- [Trên chuỗi](#on-chain)
- [Ngoài chuỗi](#off-chain)

### Trên chuỗi {#on-chain}
Quy trình bắt đầu khi một Người giao dịch tạo giao dịch bằng cách gọi `submitTransaction` trên `Shield.sol`. Người giao dịch phải trả phí Hợp đồng Phòng vệ cho Giao dịch đó, có thể là bất cứ gì mà Người giao dịch quyết định. Khoản này sẽ được thanh toán cho Người đề xuất, là người kết hợp giao dịch vào Khối. Hiện nay, người đề xuất và loại Optimist cơ bản có nhiều khả năng sẽ chọn phí cao hơn để kết hợp vào Khối, tương tự như thợ đào sẽ làm. Việc gọi Giao dịch sẽ khiến cho sự kiện blockchain với các thông tin chi tiết được đăng lên. Nếu là hoạt động Nạp tiền, Hợp đồng Phòng vệ sẽ thanh toán token ERC Lớp 1 được đề cập.

### Ngoài chuỗi {#off-chain}
Các giao dịch Chuyển nhượng và Rút tiền có thể được gửi trực tiếp cho người đề xuất đang lắng nghe thay vì gửi trên chuỗi theo quy trình bên trên. Các giao dịch ngoài chuỗi này sẽ giúp Người giao dịch tiết kiệm chi phí gửi trên chuỗi cho khoản nạp (~45k gas) nhưng đòi hỏi mức độ tin cậy cao hơn giữa người giao dịch và người đề xuất được chọn để kết nối. Người đề xuất có hành động xấu sẽ dễ dàng kiểm duyệt các giao dịch được nhận ngoài chuỗi hơn là giao dịch trên chuỗi, do các giao dịch này không được phát cho tất cả những người đề xuất đang lắng nghe. Trong trường hợp này, người giao dịch chỉ nên coi một giao dịch là đáng tin cậy sau khi kết thúc kỳ hạn xét duyệt (1 tuần).

## Chấp nhận giao dịch {#transaction-acceptance}
Khi Người đề xuất nhận bất kỳ giao dịch nào, họ thực hiện một loạt kiểm tra để xác thực rằng giao dịch được hình thành tốt và bằng chứng xác nhận theo hàm băm đầu vào công khai. Nếu thông qua tất cả các kiểm tra, giao dịch sẽ được bổ sung vào mempool của Người đề xuất để được xem xét trong Khối.

## Tập hợp khối và gửi đi {#block-assembly-and-submission}
Người đề xuất chờ đến khi Hợp đồng Phòng vệ chỉ định họ là người đề xuất hiện hành. Người đề xuất hiện hành nhận từ Optimist nội bộ của chính mình một khối mới chứa các giao dịch từ mempool của mình. Đối với mỗi giao dịch, Người đề xuất tính toán cam kết Merkle Tree mới sẽ được đưa vào nếu các giao dịch này được bổ sung vào Hợp đồng Phòng vệ.

Khối chứa các hàm băm của Giao dịch, được đưa vào trong Khối và cam kết gốc Merkle Tree như sẽ tồn tại sau khi xử lý tất cả các giao dịch trong Khối (Gốc cam kết). Sau đó Người đề xuất gửi khối này đến hợp đồng thông minh Trạng thái.

Khi một khối được đề xuất, thông tin sau sẽ được ghi lại trên chuỗi:

- Cấu trúc dữ liệu khối
```
  struct Block {
    uint48 leafCount; // note this is defined to be the number of leaves BEFORE the commitments in this block are added
    address proposer;
    bytes32 root; // the 'output' commitment root after adding all commitments
    uint256 blockNumberL2;
    bytes32 previousBlockHash;
    bytes32 transactionHashesRoot;
  }
```
- Các giao dịch trong khối
```
    struct Transaction {
        uint112 value;
        uint112 fee;
        TransactionTypes transactionType;
        TokenType tokenType;
        uint64[2] historicRootBlockNumberL2; // number of L2 block containing historic root
        uint64[2] historicRootBlockNumberL2Fee; //number of L2 block containing historic root fee
        bytes32 tokenId;
        bytes32 ercAddress;
        bytes32 recipientAddress;
        bytes32[2] commitments;
        bytes32[2] nullifiers;
        bytes32[1] commitmentFee;
        bytes32[2] nullifiersFee;
        bytes32[2] compressedSecrets;
        uint256[4] proof;
    }
```

## Thử thách {#challenges}
Các khối sẽ được thử thách trong một tuần chờ đợi. Trong thời gian đó tính, khối sẽ được kiểm tra chính xác bằng cách gọi ra một trong những chức năng thử thách. Các thử thách có thể thực hiện là:

- **INVALID_ PROOF** - bằng chứng được đưa trong giao dịch không được xác minh là đúng;
- **INVALID_ PUBLIC_INPUT_HASH** - hàm băm đầu vào công khai của giao dịch không phải là hàm băm đúng của đầu vào công khai;
- **HISTORIC_ ROOT_EXISTS** - gốc của cam kết Merkle Tree được sử dụng để tạo bằng chứng giao dịch chưa bao giờ tồn tại;
- **DUPLICATE_NULLIFIER** - một nullifier, được cho như một phần của Giao dịch, hiện diện trong danh sách các nullifier đã sử dụng;
- **HISTORIC_ ROOT_ INVALID** - gốc cam kết cập nhật có nguồn gốc từ việc xử lý các giao dịch trong Khối là gốc không đúng;
- **DUPLICATE_TRANSLATIONS** - một giao dịch giống y hệt được đưa vào khối này đã có trong một khối trước đây;
- **TRANSACTION_TYPE_INVALID** - giao dịch không được hình thành tốt dựa trên loại giao dịch (ví dụ: nạp tiền, chuyển nhượng, rút tiền).

Nếu vượt qua thử thách thành công, ví dụ tính toán trên chuỗi cho thấy đó là một thử thách hợp lệ, tiếp đó sẽ tiến hành các thao tác sau:

- Hàm băm của Khối được đề cập và tất cả các Khối sau đó sẽ được gỡ khỏi hàng đợi.
- Cổ phần Khối do Người đề xuất gửi đi sẽ được trả cho Người tuyên bố.
- Người giao dịch có Giao dịch trong Khối được hoàn lại khoản phí mà họ lẽ ra phải trả cho Người đề xuất cũng như bất kỳ khoản tiền giao kèo nào theo Hợp đồng Phòng vệ trong trường hợp giao dịch nạp tiền.

