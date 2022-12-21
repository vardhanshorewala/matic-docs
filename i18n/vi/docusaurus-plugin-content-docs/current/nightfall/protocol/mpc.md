
# MPC Ceremony {#mpc-ceremony}
Bằng chứng Zero-knowledge cần một thiết lập đáng tin cậy. Thiết lập này tạo ra "rác thải độc hại" có thể dẫn đến khả năng tạo ra bằng chứng giả. Để tránh điều này, cần tổ chức một nghi thức ở nơi tạo ra thiết lập này thông qua tính toán đa bên (MPC).

Nightfall đã thực hiện quá trình Tính toán đa bên (MPC) theo cùng nguyên tắc của Perpetual Powers of Tau Ceremony. Quy trình này bắt đầu với phần đóng góp 72 từ Perpetual Powers of Tau Ceremony cho BN254 Curve. Bạn có thể tìm thấy phần đóng góp này [tại đây](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response).

Do Nightfall sử dụng bộ chứng minh Groth16, cần có giai đoạn thứ hai của MPC cho mỗi mạch. Giai đoạn 2 này có 4 phần đóng góp riêng tư:

1. [Darko Macesic (github ID: dark64)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Jordi Bailyna (github ID: jbaylina)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Paul Brody (Lãnh đạo Blockchain Toàn cầu EY)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Michael Connor (github id ID: iAmMichaelConnor)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

Sau phần đóng góp cuối cùng, chúng tôi áp dụng một mốc hiệu ngẫu nhiên cho 4 mạch. Đối với mốc hiệu này, chúng tôi đã tạo một [giao dịch](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1) mạng chính với tải trọng dữ liệu 0xe095cb (ở dạng thập phân là 14718411).

Giao dịch này đã được đưa vào trong số khối [14711908](https://etherscan.io/block/14711908), được đưa ra vào ngày 5/5/2022 lúc 05:00:27 chiều giờ UTC và có blockhash `0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3`. Hàm băm này sau đó đã bị băm theo cách đệ quy 1024 lần. Kết quả là `0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09`.

Hàm băm cuối cùng được tính toán bằng chương trình này:

```js
import crypto from 'crypto';

let h = '875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3';
for (let i = 0; i < 1024; i++) {
  h = crypto.createHash('sha256').update(h, 'hex').digest('hex');
}
console.log(h);
```

Có thể tìm thấy thông tin hoàn tất về giai đoạn 2 [tại đây](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/phase2.md).

