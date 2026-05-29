# RAPTOR — Sport Performance Web App

เว็บแบรนด์ RAPTOR ดีไซน์ทันสมัย สำหรับสายสปอร์ตพรีเมียม (สเปรย์เย็น Ice Cold Spray + โรลออนสมุนไพร)

## โครงสร้าง

| ไฟล์ | รายละเอียด |
|------|-----------|
| `index.html` | หน้าแบรนด์หลัก — hero, สินค้า, จุดเด่น, Ice Cold Spray, รีวิว, CTA (single page, no build) |
| `roll-on.html` | หน้าขาย RAPTOR Herbal Roll-On เดิม (มี 360° view, แฟลชเซล, รีวิว) |
| `raptor-cool-spray.jpg` | ภาพสินค้า Ice Cold Spray (hero) |
| `Artboard 1_0.jpg` | ภาพ Ice เย็น x2 สูตรใหม่ |
| `E8E82679-…png`, `E7BCE3F2-…png`, `021FCB00-…png` | ภาพ Herbal Roll-On |

## ฟีเจอร์

- ดีไซน์ glassmorphism โทน ice-blue พร้อม ambient gradient background
- Responsive เต็มรูปแบบ + เมนูมือถือ, sticky glass navbar
- Scroll-reveal animation (IntersectionObserver), floating hero, marquee
- Meta Pixel + ปุ่มสั่งซื้อผ่าน LINE
- รองรับ `prefers-reduced-motion`

## รัน / ดีพลอย

เป็น static site ล้วน เปิด `index.html` ได้เลย หรือรันเซิร์ฟเวอร์:

```bash
python3 -m http.server 8000
# เปิด http://localhost:8000
```

ดีพลอยได้ทันทีบน Vercel / Netlify / GitHub Pages (ไม่ต้อง build)
