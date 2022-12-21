---
id: ethereum-polygon
title: Ethereum ↔ Polygon
description: สร้าง แอป บล็อกเชน ถัดไป ของคุณ บน Polygon
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Plasma ได้จัดหา โซลูชัน เพื่อ โอน สินทรัพย์ของคุณ จาก Ethereum ไปยัง Polygon และ ในทางกลับกัน
* ใช้ [matic.js](https://github.com/maticnetwork/matic.js) เพื่อ โต้ตอบ เกี่ยวกับ สัญญา Polygon Plasma

<!-- * [getting-started](https://maticnetwork.github.io/matic.js/): Set-up the environment for maticjs.
1. [(Ethereum → Matic)](/docs/develop/maticjs/deposit): Deposit assets from root chain to Matic.
2. [(Matic ↔ Matic)](/docs/develop/maticjs/transfer): Transfer assets between accounts on Matic.
3. [(Matic → Ethereum)](/docs/develop/maticjs/withdraw): Withdraw assets from Matic to root chain. -->

## Flow {#flow}
นี่ คือ Flow ประกอบดว้ย การย้าย สัญญาของคุณ ใน Polygon และ สนับสนุน Ethereum↔Polygon

1. ผู้ใช้ ย้าย โทเค็น ERC-20 ไปยัง Ethereum - XToken

2. ตอนนี้ โปรดแชร์ ที่อยู่ สัญญา ของคุณ กับ [Polygon](https://t.me/joinchat/HkoSvlDKW0qKs_kK4Ow0hQ) นี่ คือ คำขอ ตัวอย่าง ...

> สวัสดี ทุกท่าน เรา เป็น Aweston DApp ซึ่ง ถูกย้าย ไปยัง Polygon เรา กำลังมองหา โซลูชัน เพื่อ โอน สินทรัพย์ ของ เรา จาก Ethereum ไปยัง Polygon และ ในทางกลับกัน <br/><br/>
> รายละเอียด สรุป เกี่ยวกับ  AwesomeDApp... ของเรา<br/><br/>
> ที่อยู่_โทเค็น ใน Ropsten-> "0x.."<br/>
> ชื่อ_โทเค็น-> "XToken"<br/>
> สัญลักษณ์_โทเค็น-> "X"<br/>
> โทเค็น_เลขทศนิยม-> "18"<br/><br/>
> ขอให้คุณ Map โทเค็น ดังกล่าว ไปยัง Polygon Testnet เวอร์ชััน <br/>

เรา จะ ปรับใช้ สัญญา child สำหรับ คุณ ใน Polygon ซึ่ง จะติด อย่างคล่อง กับ ข้อกำหนด และ ถถูก mapped ไปยัง โทเค็น Ethereum ↔ Polygon ของคุณ(เพื่อดำเนินการย้าย ไปยัง Polygon ต้อง มี โทเค็น ดั้งเดิม ของ Polygon ซึ่ง สามารถ โอน จาก Ethereum ไปยัง Polygon หรือ สามารถ ซื้อ ได้ ใน พื้นที่ ตลาด ระดับสอง)

3. ผู้ใช้ สามารถ สร้าง X-โทเค็น และ โอน เข้า Ethereum ยก ตัวอย่าง สมมุติว่า 100Xโทเค็น ถูก สร้าง และ หลังจากนั้น ถูก โอน ไปยัง บัญชี อื่น

4. เพื่อ avail โทเค็น เหล่า นี้ ใน เชน Polygon คุณ ต้อง call ฟังก์ชัน ฝาก ซึ่ง จะ call ธุรกรรม สอง อย่าง โดยตอนแรก จะอนุมมัติ และ หลังจากนั้น จะฝาก ERC20

5. ตอนนี้ 100Xโทเค็น สามารถใช้ได้ ใน เชน Polygon ตาม ที่อยู่ เดียวกัน

6. คุณ สามารถ โอน 50Xโทเค็น จาก ที่อยู่ของคุณ ไปยัง ที่อยู่ใหม่ อีกทั้ง บรรดาธุรกรรม ใน Polygon คล้าย กับ Ethereum โดย Polygon ใช้ โทเค็น ดั้งเดิม ของตนเอง

7. หาก บรรดาผู้ใช้ ต้องการ รับ Xโทเค็น นั้น คืน เข้า เชน Ethereum ให้ call StartWithdraw ซึ่ง จะ ถอน โทเค็น จาก สัญญา child โทเค็น และ จะ ทำลาย โทเค็น นั้น ใน เชน Polygon เพื่อ หลีกเลี่ยง เข้าร่วม ที่ ไม่ดี ประเภทใด จะ มี การดำเนิน เซท การตรวจสอบความถูกต้อง เมื่อ ถูก ดำเนินการ แล้ว สามารถ ใช้ โทเค็น ใน เชน Ethereum

8. call processExits() เพื่อ รับ โทเค็น นั้น คืน เข้า eoa ของคุณ หรือ ที่อยู่ บัญชี ของคุณ

9. คุณ ต้อง เห็น 50 Xโทเค็น ใน Ethereum Mainnet ตาม ที่อยู่ บัญชี ของคุณ
