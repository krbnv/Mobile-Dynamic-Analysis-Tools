# Mobile Dynamic Analysis Tools

## Dynamic tahlil nima?

Dynamic tahlil — mobil ilovani **ishga tushirilgan holatda** tekshirish jarayoni.

Bu usul orqali quyidagilar kuzatiladi:

- ilova yuborayotgan API requestlar;
- serverdan kelayotgan response'lar;
- login va tokenlar;
- ilovaning runtime holati;
- loglar;
- network trafik;
- ilova ishlayotgan paytdagi funksiyalar.

Static tahlilda APK kodi ko‘riladi, dynamic tahlilda esa ilova real ishlayotgan paytda tekshiriladi.

---

## 1. Burp Suite

Burp Suite mobil ilova va backend server orasidagi HTTP/HTTPS trafikni kuzatish uchun ishlatiladi.

### Vazifalari

- Requestlarni ushlash
- Response'larni ko‘rish
- Headerlarni tekshirish
- Tokenlarni ko‘rish
- API endpointlarni aniqlash
- Requestni o‘zgartirib qayta yuborish

### Ishlash sxemasi

```text
Mobile App
    |
    v
Burp Suite Proxy
    |
    v
Backend Server
```

### Misol

```http
POST /api/user/login HTTP/1.1
Host: 192.168.2.112:3000
Content-Type: application/json
```

Burp Suite'da asosan quyidagi bo‘limlar ishlatiladi:

```text
Proxy
HTTP history
Repeater
```

---

## 2. Android Emulator

Android Emulator Android ilovani virtual telefonda ishga tushirish uchun ishlatiladi.

### Vazifalari

- APK o‘rnatish
- Ilovani test qilish
- Proxy sozlash
- ADB bilan ishlash
- Network trafikni Burp orqali yuborish

Misol:

```bash
adb devices
```

Proxy qo‘yish:

```bash
adb shell settings put global http_proxy 10.0.2.2:8080
```

Proxy'ni o‘chirish:

```bash
adb shell settings put global http_proxy :0
```

---

## 3. ADB

ADB — Android qurilma yoki emulator bilan terminal orqali ishlash vositasi.

### Vazifalari

- Qurilmalarni ko‘rish
- APK o‘rnatish
- Shell ochish
- Loglarni ko‘rish
- Proxy sozlash
- Fayllar bilan ishlash

Qurilmalarni tekshirish:

```bash
adb devices
```

Shell ochish:

```bash
adb shell
```

---

## 4. Logcat

Logcat Android ilovalarining loglarini real vaqt rejimida ko‘rsatadi.

### Vazifalari

- Ilova xatolarini ko‘rish
- Debug ma'lumotlarini topish
- Token, URL yoki boshqa ma'lumotlar logga chiqayotganini tekshirish

Misol:

```bash
adb logcat
```

Ma'lum so‘zni qidirish:

```bash
adb logcat | findstr token
```

---

## 5. MobSF Dynamic Analyzer

MobSF Dynamic Analyzer mobil ilovani ishga tushirib avtomatik dynamic tahlil qilish uchun ishlatiladi.

### Tekshirishi mumkin

- Network trafik
- Runtime faoliyat
- API chaqiruvlari
- Fayllar
- Loglar
- Ilova permissionlari
- WebView faoliyati

MobSF static va dynamic tahlilni bir joyda bajarishi mumkin.

---

## 6. Frida

Frida runtime vaqtida mobil ilovaning funksiyalariga ulanib ularni kuzatish yoki o‘zgartirish uchun ishlatiladi.

### Vazifalari

- Methodlarni kuzatish
- Funksiya argumentlarini ko‘rish
- Return qiymatlarini o‘zgartirish
- SSL Pinning bypass laboratoriyalarida ishlatish
- Runtime hook qilish

Oddiy tushuncha:

```text
Ilova ishlayapti
      |
      v
Frida methodga ulanadi
      |
      v
Method ishlashini kuzatadi
```

---

## 7. Objection

Objection Frida asosida ishlaydigan mobil security vositasi.

U Frida bilan bajariladigan ayrim vazifalarni tayyor buyruqlar orqali osonlashtiradi.

### Vazifalari

- Ilova ma'lumotlarini ko‘rish
- Runtime tahlil
- Android komponentlarini tekshirish
- SSL Pinning laboratoriyalarida yordam berish
- Fayl tizimini ko‘rish

---

## Static va Dynamic tahlil farqi

| Static Analysis | Dynamic Analysis |
|---|---|
| Ilova ishga tushirilmaydi | Ilova ishga tushiriladi |
| APK kodi tekshiriladi | Runtime holati tekshiriladi |
| JADX ishlatilishi mumkin | Burp, Frida, Logcat ishlatiladi |
| Manifest va source code ko‘riladi | Request, response va runtime kuzatiladi |

---

## Xulosa

Dynamic analysis mobil ilovani real ishlayotgan paytda tekshirish imkonini beradi.

Eng ko‘p ishlatiladigan vositalar:

```text
Burp Suite
Android Emulator
ADB
Logcat
MobSF Dynamic Analyzer
Frida
Objection
```

Burp Suite network trafikni tahlil qilish uchun, Frida va Objection runtime tahlil uchun, ADB va Logcat esa Android qurilma bilan ishlash va loglarni kuzatish uchun ishlatiladi.

