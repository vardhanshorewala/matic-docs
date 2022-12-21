---
id: nightfall-wallet
title: Ví Nightfall
sidebar: Nightfall Wallet
description: "Hướng dẫn về ví Polygon Nightfall."
keywords:
  - docs
  - matic
  - polygon
  - nightfall
  - wallet
image: https://matic.network/banners/matic-network-16x9.png

---

Ví Polygon Nightfall là một ví trình duyệt có thể tương tác với bản phát hành beta mạng chính Nightfall.

:::info Sử dụng ví Nightfall để nạp, chuyển và rút tiền

### Hạn chế {#restrictions}

Khi Nightfall đạt được trạng thái đầy đủ, các hạn chế sau sẽ được áp dụng:


| Token ERC20 | Nạp tối đa | Rút tối đa |
|-------------|-------------|--------------|
| MATIC | 250 MATIC | 1000 MATIC |
| WETH | 0,25 WETH | 1 WETH |
| DAI | 250 DAI | 1000 DAI |
| USDT | 250 USDT | 1000 USDT |
| USDC | 250 USDC | 1000 USDC |

:::

:::caution Các biện pháp bảo mật

Ví Nightfall được kiểm tra trên trình duyệt Chrome. Với Beta, phí có thể khác nhau trên các trình duyệt khác nhau.

**Bạn nên sử dụng Nightfall trên Chrome**.

:::



## Bắt đầu {#getting-started}

Truy cập [ví mạng chính](https://wallet-beta.polygon.technology) trang web Polygon hoặc [ví mạng thử nghiệm](https://wallet.testnet.polygon-nightfall.technology/), kết nối tài khoản MetaMask của bạn và chọn Ví Polygon bên trái. Nếu bạn cần trợ giúp với MetaMask, hãy tham khảo [tài liệu Polygon trên MetaMask](../../develop/metamask/tutorial-metamask.md)

![](../imgs/tools-wallet/polygon-wallet-click-nf.png)

Tại thời điểm này, ví sẽ nhắc nhở bạn Chuyển sang Mạng Polygon và một popup Metamask sẽ yêu cầu bạn xác nhận việc chuyển này.

![](../imgs/tools-wallet/polygon-network.png)

Tiếp theo, ở phần ví trên cùng, nhấp vào menu Thả xuống và chọn `Polygon Nightfall`, một yêu cầu mới về việc chuyển sang Mạng chính Ethereum sẽ xuất hiện. Bạn hãy chấp nhận chuyển sang mạng chính Ethereum để hoạt động với Polygon Nightfall.

![](../imgs/tools-wallet/polygon-network-dropdown-nf.png)

Nếu bạn đang làm trên mạng thử nghiệm thì URL ví sẽ ngay lập tức đưa bạn đến trang đích của ví Polygon Nightfall.

![](../imgs/tools-wallet/wallet-main-screen.png)

Ngay lần truy cập đầu tiên, ví Nightfall của bạn sẽ được tạo. Một pop-up sẽ xuất hiện để tạo từ gợi nhớ và tạo ví. Nhấp `Generate Mnemonic`, rồi `Create Wallet`. **Lưu ý rằng bạn chỉ có thể sử dụng ví này trên thiết bị hiện tại**.

![](../imgs/tools-wallet/generate-mnemonic-create-wallet.png)

:::caution Sao lưu các cam kết và từ gợi nhớ của bạn

Các khóa ví và giao dịch của bạn được lưu trữ trong trình duyệt (IndexedDb). Giống như từ gợi nhớ bạn thiết lập khi truy cập Ví Nightfall lần đầu tiên.

Đừng quên lưu trữ từ gợi nhớ này ở nơi an toàn. Đây là cách duy nhất để có thể tạo ra bằng chứng tương thích với số tiền của bạn trên L2. Tương tự như vậy với cam kết của bạn: đảm bảo lưu trữ cam kết một cách an toàn bằng cách bấm `export commitments` bất kỳ khi nào bạn sử dụng trình duyệt hoặc máy khác.

:::

**Nếu làm mất cam kết, số tiền của bạn cũng sẽ mất**


Vào lúc này, bạn có thể thấy cả Metamask và địa chỉ ví Nightfall (trên cùng bên phải).

**Hãy chờ thêm vài phút để hoàn tất thiết lập ví trước khi bắt đầu giao dịch**.

Ở góc dưới cùng bên trái của ví, trạng thái ví sẽ hiển thị `Syncing Nightfall`. Ở trạng thái này, ví đang truy xuất các circuit ZK và trạng thái mạng lưới cần có để thực hiện giao dịch.

![](../imgs/tools-wallet/wallet-state-syncing.png)

Vui lòng chờ cho đến khi trạng thái ví chuyển thành `Nightfall Synced`

![](../imgs/tools-wallet/wallet-state-synced.png)


## Cách thức để kết nối Ví cứng Ledger tới Nightfall {#how-to-connect-a-ledger-hardware-wallet-to-nightfall}
Bạn có thể xem hướng dẫn kết nối Ví cứng Ledger với Metamask trên trang Metamask chính thức [tại đây](https://support.ledger.com/hc/en-us/articles/4404366864657-How-to-access-your-Ledger-Ethereum-ETH-account-via-Metamask?docs=true).

Đừng quên kết nối Ứng dụng Ethereum trong ví của bạn và cho phép "ký mù" trong phần thiết lập Ứng dụng Ethereum.


### Địa chỉ ví của bạn {#your-wallet-address}
Lấy địa chỉ ví Nightfall từ trang Tài sản Nightfall bằng cách nhấp `Receive`.

![](../imgs/tools-wallet/nightfall-wallet-address.png)

## Cách thức thực hiện nạp tiền {#how-to-make-deposits}
Trên trang Tài sản Nightfall, nhấp vào nút `Deposit` bên phải của tài sản được chọn hoặc chuyển sang trang Cầu nối L2.

1. Kiểm tra xem chế độ Chuyển nhượng được đặt thành `Deposit`hay chưa
2. Kiểm tra xem token mong muốn đã được chọn (WETH, MATIC,...) hay chưa
3. Nhập giá trị cần nạp vào ví Nightfall của bạn, nhấp `Transfer`
4. Xem lại giao dịch trên pop-up
5. Nhấp `Create Transaction`

![](../imgs/tools-wallet/deposit-click-transfer.png)

Một quy trình sẽ bắt đầu để tính toán ZKP và chuẩn bị giao dịch - cấp cho Metamask quyền truy cập vào số dư tài khoản của bạn. Khi kết thúc, hãy nhấp  `Send Transaction`- cấp cho Metamask các quyền hạn bổ sung để tương tác hợp đồng.

![](../imgs/tools-wallet/deposit-tx-created-and-ready-to-be-sent.png)

Đến trang Giao dịch để [xem khoản nạp của bạn](#view-transactions).

### Thông tin quan trọng về các khoản nạp {#important-information-about-deposits}
- [Số tiền nạp bị hạn chế](#note-the-following-deposit-and-withdrawal-restrictions) khi ở chế độ Beta

## Cách thức thực hiện chuyển nhượng {#how-to-make-transfers}
Trên trang Tài sản Nightfall, nhấp vào nút `Send` bên phải của tài sản được chọn.

1. Nhập vào một địa chỉ hợp lệ hiện hữu trên Polygon Nightfall L2
2. Kiểm tra xem token mong muốn đã được chọn (WETH, MATIC,...) hay chưa
3. Nhập giá trị cần chuyển từ ví Nightfall của bạn, nhấp `Continue`

![](../imgs/tools-wallet/send-nf.png)

Một quy trình sẽ bắt đầu để tính toán ZKP và chuẩn bị giao dịch. Khi kết thúc, nhấp `Send Transaction`.

Đến trang Giao dịch để [xem chuyển nhượng của bạn](#view-transactions).

### Thông tin quan trọng về chuyển nhượng {#important-information-about-transfers}
Các circuit chuyển nhượng ZKP hiện tại được sử dụng trong Nightfall hạn chế lượng chuyển nhượng đến mức khớp chính xác với giá trị của một trong những cam kết hiện hữu hoặc với bất kỳ kết hợp tuyến tính nào giữa hai cam kết hiện hữu.

Để minh họa hạn chế chuyển nhượng bằng ví dụ, hãy quan sát các bộ cam kết sau:

- Bộ A: [1, 1, 1, 1, 1, 1]
- Bộ B: [2, 2, 2]
- Bộ C: [2, 4]

Mặc dù cả ba bộ đều có tổng tương đương 6 nhưng chỉ các chuyển nhượng sau khả dụng:

- Bộ A: các chuyển nhượng từ 0 đến 2 (đều nằm ngoài)
- Bộ B: các chuyển nhượng từ 0 đến 4 (đều nằm ngoài)
- Bộ C: các chuyển nhượng từ 0 đến 6 (đều nằm ngoài)

Tiếp tục ví dụ này, nếu Alex sở hữu Bộ cam kết C, các chuyển nhượng khả dụng sẽ bao gồm số lượng bất kỳ từ 0 đến 6, không bao gồm hai giá trị giới hạn. Nếu Alex quyết định chuyển nhượng 3,5 cho Bob, Alex sẽ kết thúc với một cam kết đơn lẻ 2,5 và Bob sẽ nhận cam kết 3,5 khi khối được đề xuất.

Mặt khác, nếu Alex quyết định chuyển nhượng 6 cho Bob, bằng chứng ZK sẽ không thành công vì không thể kết hợp các cam kết một cách hợp lệ.

**Cần lưu ý rằng các giá trị này đại diện cho cam kết sở hữu**, không phải khoản tiền nạp. Xem thêm thông tin tại phần [cam kết](../protocol/commitments.md) của các tài liệu này.

## Cách thức thực hiện rút tiền {#how-to-make-withdrawals}
Trên trang Tài sản Nightfall, nhấp vào nút `Withdraw` bên phải của tài sản được chọn hoặc chuyển sang trang Cầu nối L2.

1. Kiểm tra xem chế độ Chuyển nhượng được đặt thành `Withdraw`hay chưa
2. Kiểm tra xem token mong muốn đã được chọn (WETH, MATIC,...) hay chưa
3. Nhập giá trị cần rút ra từ ví Nightfall của bạn, nhấp vào `Transfer`
4. Xem lại giao dịch trên pop-up
5. Nhấp `Create Transaction`

Một quy trình sẽ bắt đầu để tính toán ZKP và chuẩn bị giao dịch. Khi kết thúc, nhấp `Send Transaction`.

Đến trang Giao dịch để [xem việc rút tiền của bạn](#view-transactions). Sau khi kết thúc khoảng thời gian quyết toán một tuần, người dùng có thể hoàn thành và nhận số tiền rút.

### Thông tin quan trọng về việc rút {#important-information-about-withdrawals}
- Giá trị rút phải hoàn toàn khớp với số lượng tại một trong những cam kết sở hữu (nhiều hơn [về cam kết](#learn-about-commitments))
- Hoạt động rút tiền có kỳ hạn hoàn thành là **một tuần** kể từ lúc khối có chứa giao dịch rút được tạo. Khi kỳ hạn này kết thúc, bạn có thể hoàn tất việc rút tiền để tiền được gửi đến tài khoản Ethereum của bạn.
- [Số lượng rút bị hạn chế](#note-the-following-deposit-and-withdrawal-restrictions) khi ở chế độ Beta
- Rút tiền là một giao dịch trên chuỗi và phải thanh toán phí gas trong quá trình yêu cầu giao dịch cũng như khi đã rút xong.

![](../imgs/tools-wallet/cooling-off-vs-ready.png)

## Xem giao dịch {#view-transactions}
Kiểm tra trạng thái nạp tiền, chuyển nhượng và rút tiền của bạn trên trang Giao dịch. Lưu ý rằng giao dịch sẽ được xử lý ngay khi có đủ giao dịch để tạo khối hoặc sau 6 tiếng.

![](../imgs/tools-wallet/transactions.png)
