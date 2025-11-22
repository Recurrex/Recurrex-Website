<!-- .github/copilot-instructions.md: guidance for AI coding agents working on this repo -->

# คำแนะนำสั้น ๆ สำหรับ Copilot / AI agent (ภาษาไทย, เป็นกันเอง)

สรุปสั้น ๆ (แบบเป็นกันเอง)
- โปรเจกต์นี้เป็นตัวอย่าง Next.js (pages-router) ขนาดเล็ก — โค้ดเพจอยู่ที่ `src/pages`, สไตล์ที่ `src/styles` และไฟล์ static อยู่ใน `public/` (เช่น รูปและ copy ใน `public/All-Texts`).

คำสั่งด่วน
- ติดตั้ง: `npm install`
- เริ่มพัฒนา: `npm run dev` (เรียก `next dev`)
- สร้าง production: `npm run build` แล้ว `npm run start`
- ตรวจโค้ด: `npm run lint`

ภาพรวมสถาปัตยกรรม
- Router: ใช้ pages router ของ Next.js — แก้ไขไฟล์เพจที่ `src/pages/*.js` (เช่น `src/pages/index.js`).
- ไฟล์ static: รูปภาพและข้อความสำคัญเก็บใน `public/` และ `public/All-Texts/*.txt` (ไฟล์ข้อความใช้เป็น copy snippets)
- สไตล์: global CSS อยู่ที่ `src/styles/globals.css` และเพจแต่ละหน้าใช้ CSS Modules เช่น `src/styles/Home.module.css` (โค้ดปัจจุบันไม่ได้ใช้ Tailwind)
- API: ใช้ serverless API routes ภายใต้ `src/pages/api/*.js` (ตัวอย่าง `src/pages/api/hello.js` ส่ง JSON กลับ)

บันทึกเฉพาะโปรเจกต์
- README เดิมอ้างถึง Tailwind แต่โค้ดใน repo ใช้ plain CSS + CSS Modules — อย่าแปลงเป็น Tailwind โดยพลการ
- `framer-motion` ถูกเพิ่มใน `package.json` เพื่อรองรับอนิเมชัน ถ้าจะเพิ่มแอนิเมชันให้ import และใช้งานในคอมโพเนนต์ตามต้องการ
- Next.js เวอร์ชันคือ v14 แต่โปรเจกต์ยังใช้ `src/pages` — หลีกเลี่ยงการย้ายไป `app/` router เว้นแต่ได้รับคำสั่ง

งานแก้ไขที่พบบ่อย — ไฟล์เป้าหมาย
- แก้เนื้อหา homepage: `src/pages/index.js` และ `src/styles/Home.module.css` หรือแก้ copy ใน `public/All-Texts/pages.txt`
- เพิ่มเพจใหม่: สร้าง `src/pages/<name>.js` และ CSS module ใน `src/styles` ถ้าจำเป็น
- เพิ่ม API endpoint: สร้าง `src/pages/api/<endpoint>.js` ตาม pattern `handler(req,res)` ใน `src/pages/api/hello.js`
- เพิ่มรูป: วางไฟล์ใน `public/images/` หรือ `website images/` แล้วใช้ `next/image` เพื่ออ้างอิง (`/images/<file>`)

วิธีดีบักและ workflow ของนักพัฒนา
- พัฒนาแบบ local: `npm run dev` — overlay ของ Next จะแสดง error ในเบราว์เซอร์
- ทดสอบ API เล็ก ๆ: เรียก `http://localhost:3000/api/hello` เพื่อตรวจการตอบกลับ
- ทดสอบ production: `npm run build` แล้ว `npm run start` — เฝ้าดูข้อผิดพลาดการ import หรือขนาดรูปภาพที่อาจทำให้ build ล้มเหลว

ข้อปฏิบัติและ convention
- เก็บเพจใน `src/pages` เสมอ — อย่าเปลี่ยนโครงสร้างโฟลเดอร์หลัก
- ใช้ CSS Modules สำหรับสไตล์ของเพจ (`import styles from '@/styles/Name.module.css'`) และเก็บตัวแปรโทนสีใน `src/styles/globals.css`
- ข้อความคงที่บางส่วนเก็บใน `public/All-Texts/*.txt` — ค้นหาและแก้ไฟล์เหล่านี้เมื่อต้องการเปลี่ยน copy ของเว็บไซต์
- ใช้ `next/image` เมื่ออ้างอิงรูปจาก `public/` เพื่อให้ได้ประสิทธิภาพการโหลดที่ดี

dependency และ integration points
- `next`, `react`, `react-dom` — ไลบรารีหลักตามเวอร์ชันใน `package.json`
- `framer-motion` — ใช้เมื่อต้องการแอนิเมชันในคอมโพเนนต์
- ไม่มีการเชื่อมต่อฐานข้อมูลหรือบริการภายนอกอื่น ๆ ใน repo นี้ — มีเพียง API routes แบบ serverless

ตัวอย่าง (คัดลอกใช้ได้)
- ตัวอย่าง API route (`src/pages/api/hello.js`):
```
export default function handler(req, res) {
  res.status(200).json({ name: 'John Doe' })
}
```
- คำสั่งเริ่มพัฒนา:
```
npm install
npm run dev
```

เมื่อติดขัด
- ค้นหาสตริงที่ต้องการเปลี่ยนในโค้ดก่อนแก้ — ข้อความบางส่วนอยู่ใน `public/All-Texts/*.txt`
- หลีกเลี่ยงการเปลี่ยนสถาปัตยกรรมหลัก (เช่น ย้ายไป `app/` router หรือเพิ่ม Tailwind) โดยไม่ได้รับอนุญาต

แก้ไฟล์นี้แล้ว
- คงความสั้นและชัดเจนไว้เมื่อแก้ไฟล์นี้ และเพิ่มคำอธิบายใหม่เมื่อมี convention ใหม่ที่ต้องรู้

ข้อเสนอแนะ
- ถ้าต้องการให้ผมขยายหัวข้อใด (เช่น เพิ่มตัวอย่างการทำ PR, CI, หรือชุดทดสอบ) บอกได้เลยว่าจะเพิ่มอะไร
