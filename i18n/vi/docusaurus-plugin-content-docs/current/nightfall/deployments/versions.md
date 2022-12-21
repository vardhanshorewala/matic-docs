---
id: versions
title: Lịch sử
sidebar_label: History of changes
description: "Các phiên bản đã triển khai"
keywords:
  - docs
  - polygon
  - nightfall
  - changelog
image: https://matic.network/banners/matic-network-16x9.png
---


## Beta 1.0 {#beta-1-0}
Beta 1.0 được phát hành vào 17/05/2022. Phiên bản này gồm cơ chế cơ bản để triển khai bằng chứng khái niệm Nightfall. Phiên bản này hỗ trợ việc thực hiện các giao dịch `Proposer` đơn lẻ và  `coarse` đầu tiên. Đồng thời, nó cũng cung cấp phiên bản sơ bộ của ví người dùng. Có thể tìm thấy phiên bản đã triển khai [ở đây](https://github.com/EYBlockchain/nightfall_3/commit/bc3e475de3e2877f14430f9599e5b38ea960765b)

## Beta 2.0 {#beta-2-0}
Có thể tìm thấy phiên bản đã triển khai [ở đây](https://github.com/EYBlockchain/nightfall_3/commit/4c2af01ac95af5ea6f5b40071d73a1624f06ba46) Đã thực hiện một số cải tiến:
- **Thu thập phí**

Khả năng dành cho người đề xuất thu phí khi giao dịch. Tính năng này sẽ khuyến khích nhiều người đề xuất.
- **Triển khai Người tuyên bố**

Mạng hiện gồm một người tuyên bố giám sát các khối của người đề xuất.
- **Giao dịch nối tiếp**

Linh hoạt hơn và hiệu suất tốt hơn khi tạo ZKP của bất kỳ giao dịch nào. Cả `transfer` và `withdrawal`chấp nhận tối đa hai cam kết và trả về thay đổi. Về hiệu suất, hiện giao dịch được tối ưu hóa nên cần ít thời gian để chứng minh hơn.

| Hoạt động | Hạn chế trước | Hạn chế sau |
|-----------|--------------------|------------------|
| Nạp tiền | 84.766 | 1277 |
| Chuyển nhượng | 499.119 | 67.694 |
| Rút tiền | 168.883 | 53.348 |

Có thể tối ưu hóa một phần bằng cách chuyển sang Poseidon

- **Mã hóa bí mật**

Chúng tôi đã chuyển từ El-Gamal sang quy trình mã hóa [KEM-DEM](../protocol/secrets), việc này mang lại một số lợi ích:
- Đơn giản hóa quy trình mã hóa/giải mã
- Giảm các hạn chế và phí gas trên chuỗi.

- **Triển khai Người tuyên bố**

