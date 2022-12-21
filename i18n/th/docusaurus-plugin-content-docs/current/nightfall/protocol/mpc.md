
# MPC เซเรโมนี {#mpc-ceremony}
การพิสูจน์ความรู้ที่เป็นศูนย์จำเป็นต้องมีการตั้งค่าที่เชื่อถือได้การตั้งค่านี้สร้างสิ่งที่เรียกว่า "ขยะพิษ" ซึ่งอาจทำให้สร้างหลักฐานปลอมได้เพื่อหลีกเลี่ยงปัญหานี้ ต้องมีการจัดพิธีโดยสร้างการตั้งค่านี้ผ่านการคำนวณแบบหลายฝ่าย (Multi-Party Computation หรือ MPC)

Nightfall ดำเนินการการคำนวณแบบหลายฝ่าย (MPC) ตามหลักการเดียวกันของ Perpetual Powers of Tau Ceremonyกระบวนการเริ่มต้นด้วยการบริจาค 72 จาก Perpetual Powers of Tau Ceremony สำหรับ BN254 Curveคุณสามารถหาผลงานนี้ได้[ที่นี่](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response)

เนื่องจาก Nightfall ใช้รูปแบบการพิสูจน์ Groth16 จึงจำเป็นต้องมี MPC ระยะที่สองสำหรับแต่ละวงจร การบริจาคส่วนตัว 4 รายการเป็นส่วนหนึ่งของระยะที่ 2:

1. [Darko Macesic (github ID: dark64)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Jordi Bailyna (github ID: jbaylina)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Paul Brody (EY ผู้นำด้านบล็อกเชนระดับโลก)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Michael Connor (github ID: iAmMichaelConnor)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

หลังจากการบริจาคครั้งสุดท้าย เราใช้บีคอนแบบสุ่มสำหรับ 4 วงจรสำหรับบีคอนนี้ เราได้สร้าง[ธุรกรรม](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1)เมนเน็ต (mainnet) ด้วยข้อมูลเพย์โหลด 0xe095cb (เป็นทศนิยมคือ 14718411)

ธุรกรรมนี้รวมอยู่ในบล็อกหมายเลข [14711908](https://etherscan.io/block/14711908)ซึ่งลงเมื่อวันที่ 5 พฤษภาคม 2022 เวลา 05:00:27 น. +UTC และมีการบล็อกแฮช`0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3`.จากนั้น แฮชนี้จะถูกแฮชซ้ำ 1024 ครั้งผลลัพธ์คือ `0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09`

แฮชสุดท้ายถูกคำนวณด้วยโปรแกรมนี้:

```js
import crypto from 'crypto';

let h = '875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3';
for (let i = 0; i < 1024; i++) {
  h = crypto.createHash('sha256').update(h, 'hex').digest('hex');
}
console.log(h);
```

ข้อมูลที่สมบูรณ์ของเฟส 2 สามารถพบ[ได้ที่นี่](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/phase2.md)

