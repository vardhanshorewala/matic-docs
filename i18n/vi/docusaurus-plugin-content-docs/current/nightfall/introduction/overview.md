---
id: overview
title: Tổng quan
sidebar_label: Overview
description: Tổng quan về Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - privacy
  - rollup
  - zk
image: https://matic.network/banners/matic-network-16x9.png
---

Polygon tin tưởng vào viễn cảnh khi nhiều công ty trong tương lai gần có thể tương tác với nhau qua hợp đồng thông minh để thực hiện logic kinh doanh và quản lý việc trao đổi hàng hóa, dịch vụ.

Cùng với [Ernst & Young](https://blockchain.ey.com/), Polygon cung cấp một giải pháp rollup Lớp 2, tập trung vào quyền riêng tư và công khai với tên gọi Polygon Nightfall, cung cấp khả năng truy cập và quyền riêng tư cho các công ty muốn sử dụng Ethereum.

## Giao thức ZK-Proof A dành cho doanh nghiệp {#a-zk-proof-protocol-for-enterprises}

Polygon Nightfall là một phần trong bộ các giải pháp khả năng mở rộng của Polygon, bao gồm [Polygon Hermez](https://polygon.technology/solutions/polygon-hermez/), [Polygon Miden](https://polygon.technology/solutions/polygon-miden/) và [Polygon Zero](https://polygon.technology/solutions/polygon-zero/). Có một khác biệt quan trọng: Nightfall là một rollup tập trung vào quyền riêng tư, được thiết kế cho các trường hợp sử dụng trong doanh nghiệp bằng cách kết hợp các khái niệm optimistic rollup và mật mã học Zero-Knowledge (ZK) dành cho giao dịch riêng tư và có thể mở rộng.

Nightfall mang đến khả năng mở rộng, đồng thời cũng loại bỏ rào cản to lớn mà các công ty ngày nay đang phải đối mặt khi sử dụng blockchain: thiếu quyền riêng tư khi giao dịch. Nightfall bổ sung một lớp bảo mật để các thông số giao dịch quan trọng (ví dụ: giá trị và đích) không thể truy lại được. Hai tính năng này mang đến lợi ích cho các doanh nghiệp tư nhân coi Nightfall như là cách để thực hiện logic kinh doanh và phối hợp với chuỗi cung ứng của họ trong một mạng lưới phi tập trung với mức giá bền vững, đồng thời duy trì tính bảo mật và quyền riêng tư.

## Các trụ cột của Nightfall {#nightfall-s-pillars}

Mục tiêu giá trị chính của Polygon Nightfall là cho phép chuyển dữ liệu một cách bảo mật, riêng tư với giá rẻ trong một mạng lưới phi tập trung.

![](../imgs/overview.png)

## Quyền riêng tư {#privacy}

Polygon Nightfall sử dụng bằng chứng ZK để gửi đi giao dịch riêng tư. Người dùng có thể tạo bằng chứng ZK của giao dịch mà không cần tiết lộ các thông số giao dịch quan trọng như đích đến hoặc giá trị giao dịch. Xem thêm chi tiết về yếu tố quyền riêng tư của Nightfall tại hướng dẫn [giao thức](../protocol/protocol.md).

## Bảo mật {#security}

> Nightfall đang thực hiện kiểm tra bảo mật và dự kiến sẽ hoàn tất vào khoảng giữa tháng 6 năm 2022. Khi quá trình kiểm tra hoàn tất, kết quả sẽ được đăng tải tại đây.

> Là một mạng lưới mới với giai đoạn bootstrap, Nightfall có các biện pháp bảo mật tạm thời nhằm bảo vệ hệ thống với mục tiêu loại bỏ chúng và để cho mạng lưới hoàn toàn phi tập trung.

Polygon Nightfall là một cấu trúc Lớp 2 vì nó tận dụng Ethereum bằng cách mượn tính bảo mật của Ethereum như một blockchain công khai mạnh mẽ. Nightfall dựa vào các giả định nhất định để đảm bảo sự khôi phục tài sản. Những giả định này dựa trên một số quyết định về kiến trúc và thiết kế xoay quanh ZK-SNARKS, bằng chứng sử dụng một số mật mã cơ sở như hàm băm và chữ ký. Cuối cùng, Nightfall đưa quy định hoạt động vào các hợp đồng thông minh khác để đảm bảo rằng người vận hành không ngăn cản giao dịch của người dùng và người dùng có thể rút tài sản của họ mọi lúc.

Nói chung, Nightfall đưa ra các giả định bảo mật như sau:

1. Giả định bảo mật của Ethereum.
2. Giả định Groth16 (kiến thức về giả định số mũ).
3. Một số giả định mật mã từ các mật mã cơ sở như hàm băm (Poseidon) và chữ ký.
4. Giả định bảo mật phần mềm dựa trên thiết kế và thực hiện đúng.

## Hiệu quả {#efficiency}

Người đề xuất khối thu thập các giao dịch từ nhiều người dùng và kết hợp chúng thành khối L2. Kích thước khối L2 điển hình chứa khoảng 32 giao dịch.

Chi phí gas dự kiến để nạp, chuyển nhượng và rút là 9000, 1200 và 9500. Chi phí này là do lưu trữ 574Byte dữ liệu gọi trên mỗi giao dịch, cộng với một số dữ liệu gọi cố định và tính toán để xử lý khối L2. Chi phí sẽ giảm tối đa 80% sau [EIP 4488](https://eips.ethereum.org/EIPS/eip-4488).

## Chuyển nhượng không thể phủ nhận {#non-deniable-transfers}

Là một phần của bằng chứng ZK giao dịch chuyển nhượng, Nightfall mã hóa các bí mật (địa chỉ token, giá trị, id và salt) cần để xử lý cam kết đã chuyển. Điều này thúc đẩy người dùng mã hóa các bí mật bằng một khóa mà người nhận đã biết. Vì khóa là một phần của bằng chứng ZK, người nhận dựa trên khả năng phủ nhận chính đáng khi người gửi chứng minh được rằng đã sử dụng khóa mã hóa đúng.

## Phi tập trung {#decentralization}

Người xác thực và [Người tuyên bố](docs/nightfall/protocol/actors) là một phần không thể thiếu của Nightfall. Họ đảm bảo rằng giao dịch và khối L2 được tạo ra đúng lúc và chính xác. Cơ chế đồng thuận dựa trên bằng chứng cổ phần (PoS) được dùng để chọn [Người đề xuất](docs/nightfall/protocol/actors) tiếp theo của mạng lưới. Mặt khác, Người tuyên bố sẽ giám sát việc vận hành chính xác mạng lưới bằng cách nâng cao thách thức khi phát hiện một khối không đúng và bằng cách duy trì cổ phần do Người đề xuất đưa ra.


## Bằng chứng tương lai {#future-proof}
Nhờ sự linh hoạt do thực hiện Optimistic rollup của Nightfall, trong tương lai bạn có thể đưa vào các giao dịch mới mà không gây ảnh hưởng đến các giao dịch hiện hữu bằng cách xác định và đăng ký một loại circuit mới đã thực hiện giao dịch ở ZK.

## Tham khảo {#references}

1. [Phương pháp tiếp cận đa chiều để mở rộng ZK](https://messari.io/article/polygon-a-multi-sided-approach-to-zk-scaling)
2. [Quan điểm của Paul Brody về Nightfall](https://www.linkedin.com/pulse/say-hello-nightfall-paul-brody-1f/)
