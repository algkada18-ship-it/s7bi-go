# 📱 دليل نشر s7bi GO كتطبيق Android

## ✅ الخطوة 1 — رفع الموقع على Firebase Hosting (مجاناً)

```bash
# 1. ثبّت أدوات Firebase (مرة واحدة فقط)
npm install -g firebase-tools

# 2. ابنِ المشروع
npm install
npm run build

# 3. سجّل الدخول بحساب Google
firebase login

# 4. هيّئ Firebase Hosting
firebase init hosting
```

عند السؤال:
- ✅ اختر مشروعك الموجود في Firebase
- ✅ اكتب: `dist` كـ public directory
- ✅ اختر: Yes لـ "Configure as single-page app"
- ✅ اختر: No لـ "Overwrite index.html"

```bash
# 5. انشر الموقع
firebase deploy --only hosting
```

ستحصل على رابط مثل: `https://اسم-مشروعك.web.app` 🎉

---

## ✅ الخطوة 2 — تحويله لـ APK جاهز للنشر

### الطريقة الأسهل: PWABuilder (مجاناً بالكامل)

1. اذهب إلى: **https://www.pwabuilder.com**
2. الصق رابط موقعك: `https://اسم-مشروعك.web.app`
3. اضغط **Start**
4. انتظر التحليل (30 ثانية)
5. اختر **Android** ثم اضغط **Download Package**
6. ستحصل على ملف `.zip` يحتوي على:
   - `app-release-bundle.aab` — للنشر على Google Play
   - `app-release.apk` — للتثبيت المباشر على الهاتف

---

## ✅ الخطوة 3 — النشر على Google Play

### المتطلبات:
- حساب Google Play Developer: **25$ مرة واحدة**
- سجّل على: https://play.google.com/console

### خطوات الرفع:
1. أنشئ تطبيقاً جديداً
2. ارفع ملف `aab.`
3. أضف:
   - اسم التطبيق: **s7bi GO**
   - وصف: منصة التوصيل الجزائرية
   - لقطات شاشة (3 على الأقل)
   - أيقونة 512×512
4. اضغط **نشر** وانتظر مراجعة Google (1-7 أيام)

---

## 📲 للتثبيت المباشر (بدون Google Play)

إذا أردت توزيع التطبيق مباشرة بدون Google Play:
1. حمّل ملف `apk.` من PWABuilder
2. أرسله لأي شخص عبر واتساب أو تيليغرام
3. على الهاتف: الإعدادات ← الأمان ← السماح بمصادر غير معروفة
4. افتح الملف وثبّت

---

## 💡 ملاحظات مهمة

- **الأيقونات**: استبدل ملفات `public/icons/` بأيقونات احترافية بنفس الأحجام
- **لشاشة التحميل**: يمكنك تخصيصها في ملف `manifest.json`
- **التحديثات**: بعد أي تعديل، نفّذ `npm run build && firebase deploy` فقط
