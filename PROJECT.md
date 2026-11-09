# WachiTalk — แอป Android (APK)

## คืออะไร
ห่อเว็บ https://wachitalk.pages.dev เป็นแอป Android ด้วย Capacitor 7 แบบ "โหลดสด" (server.url)
→ อัปเว็บขึ้น Cloudflare เมื่อไร แอปได้ของใหม่ทันที ไม่ต้องบิลด์ APK ใหม่
บิลด์ใหม่เฉพาะตอนแก้ของฝั่งแอป (สิทธิ์ ไอคอน ปลั๊กอิน)

## เชื่อมกับอะไร
- เว็บ: Cloudflare Pages โปรเจกต์ wachitalk (โค้ดเว็บอยู่ใน zip เว็บแยก)
- Firebase โปรเจกต์ wachihub (เหมือนเว็บ ไม่มีคีย์ใหม่)
- GitHub repo (ตั้งเป็น Private) + GitHub Actions บิลด์ APK ฟรี — ไม่มี secret ที่ต้องตั้ง
- appId: app.wachitalk.chat

## ไฟล์
- capacitor.config.json — ชื่อแอป, ลิงก์เว็บที่โหลด
- scripts/patch-android.js — ใส่สิทธิ์ ไมค์/กล้อง/ตำแหน่ง/บลูทูธ + เลขเวอร์ชัน (versionCode = เลขรอบบิลด์)
- assets/ — ไอคอน + หน้าเปิดแอป (โทนน้ำตาล)
- www/ — หน้าสำรองตอนไม่มีเน็ต
- .github/workflows/build-apk.yml — สั่งบิลด์

## วิธีบิลด์ (ทำครั้งแรก จากมือถือได้)
1. github.com → New repository → ชื่อ wachitalk-apk → Private → Create
2. Add file → Upload files → เลือกไฟล์ทั้งหมดใน zip นี้ (ยกเว้นโฟลเดอร์ .github ถ้ามือถืออัปโฟลเดอร์ซ่อนไม่ได้) → Commit
3. ถ้า .github ไม่ขึ้น: Add file → Create new file → ช่องชื่อพิมพ์ `.github/workflows/build-apk.yml` → วางเนื้อหาไฟล์นั้น → Commit
4. แท็บ Actions → Build WachiTalk APK → รอ ~5–8 นาที (ติ๊กเขียว)
5. หน้า repo → Releases → apk-N → โหลด WachiTalk-bN.apk → เปิด → อนุญาต "ติดตั้งแอปที่ไม่รู้จัก"
- บิลด์ซ้ำ: Actions → Build WachiTalk APK → Run workflow

## ข้อควรรู้
- ลงทับเวอร์ชันเก่าได้เพราะ cache กุญแจเซ็นไว้ ถ้า cache หาย (ไม่ได้บิลด์เกิน 7 วัน) จะลงทับไม่ได้ → ลบแอปเก่าก่อน (ข้อมูลอยู่บน Firebase ไม่หาย แค่ล็อกอินใหม่)
- บิลด์พัง: เปิดรอบที่แดง → กดขั้นที่แดง → ก๊อป/แคป log ส่งให้ Claude
- รอบนี้ยังเป็นการห่อเว็บล้วน: สลับแอป/ล็อกจอ สายอาจขาด, ยังไม่มีแจ้งเตือนตอนปิดแอป

## ประวัติ
- 9 พ.ย. 2026 23:15 — b8 (คู่กับเว็บแก้ครั้งที่ 8): สร้างโปรเจกต์ครั้งแรก
  ถัดไป: ปลั๊กอินบริการเบื้องหน้า (สายไม่ขาด), แจ้งเตือน push (FCM), แชร์ตำแหน่งตอนปิดจอ, เลือกลำโพง/บลูทูธ
