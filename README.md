# Terminal Professional — Public Update Channel

قناة التحديث العامة (بلا توكن) لمشروع Terminal Professional.

## المحتويات

| العنصر | المسار |
|---|---|
| بيان الإصدار | `update.json` (JSON فقط، بلا مصادقة) |
| حزمة الإصدار | `releases/build-<versionCode>/owner-release.apk` (قابلة للتنزيل بلا مصادقة) |

الجهاز يقرأ البيان من `raw.githubusercontent.com` أو `cdn.jsdelivr.net` لهذا المستودع،
ثم ينزّل الحزمة من رابط الإصدار العام — **بلا أي ترويسة `Authorization` وبلا أي اعتماد**.

## عقد القناة (P138)

1. **البيان** يحمل `versionCode` و`versionName` و`download_url` و`sha256` و`apks`.
2. **`sha256` في البيان = `digest` أصل الإصدار في الـAPI** — تُقارَن آليًا كل يوم
   (بوابة `.github/workflows/channel_health.yml` في مستودع المشروع: مطابقة البصمة +
   مقارنة `versionCode` القناة بآخر بناء ناجح).
3. **`versionCode` تصاعدي فقط** — `2000 + run_number` في مسار البناء، `3000 + run_number`
   في مسار الإصدار — فلا يُقرأ الترقيم الجديد كتراجع فيرفض التطبيق عرض التحديث.
4. **لا يُحذف أي إصدار ناجح** (القاعدة 10): يُستبدل محتوى الأصول فقط
   (`gh release upload --clobber` + `gh release edit`).
5. **تعذّر النشر لا يُسقط البناء**: يحتفظ هذا المستودع بآخر إصدار منشور، فجهاز المستخدم
   لا ينقطع. الإنذار يأتي من بوابة الصحة لا من فشل البناء.
6. **ملكية القناة** تحت حساب المالك `3obadotaify-89` — هي التي ينشر إليها الـCI مباشرة.
   القناة العامة الأصلية (`salahotaify89/Terminal-Professional-Updates`) تبقى مصدر قراءة
   احتياطيًا (لا تُحذف).

## الحالة الحالية

الإصدار المنشور: **build-2001 (1.0.0)** — البيان في `update.json` يشير إلى
`releases/download/build-2001/owner-release.apk` داخل هذا المستودع، لا إلى مستودع آخر.
