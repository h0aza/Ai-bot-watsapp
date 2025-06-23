# دليل نشر وإعداد بوت واتساب بالذكاء الاصطناعي

## نظرة عامة

تم تطوير بوت واتساب ذكي يدعم اللغتين العربية والإيطالية باستخدام:
- **OpenAI GPT** للردود الذكية
- **Twilio API** للتكامل مع واتساب
- **Flask** كإطار عمل الخادم
- **SQLite** لحفظ البيانات

## الملفات المطلوبة

تم إنشاء المشروع في المجلد `/home/ubuntu/whatsapp-ai-bot` ويحتوي على:

### الملفات الأساسية:
- `src/main.py` - نقطة الدخول الرئيسية
- `src/config.py` - إعدادات التطبيق (يحتوي على مفتاح OpenAI)
- `src/routes/bot.py` - معالج رسائل واتساب
- `src/services/openai_service.py` - خدمة التكامل مع OpenAI
- `src/services/twilio_service.py` - خدمة التكامل مع Twilio
- `src/models/user.py` - نماذج قاعدة البيانات
- `requirements.txt` - متطلبات Python
- `README.md` - دليل الاستخدام

## خطوات الإعداد والنشر

### 1. إعداد حساب Twilio

1. **إنشاء حساب Twilio:**
   - اذهب إلى [console.twilio.com](https://console.twilio.com)
   - أنشئ حساب جديد أو سجل دخول

2. **الحصول على بيانات الاعتماد:**
   - Account SID
   - Auth Token
   - رقم واتساب (يمكن البدء بـ Sandbox)

3. **إعداد WhatsApp Sandbox:**
   - اذهب إلى Console > Messaging > Try it out > Send a WhatsApp message
   - اتبع التعليمات لتفعيل Sandbox
   - احفظ رقم Sandbox (مثل: `whatsapp:+14155238886`)

### 2. تحديث إعدادات التطبيق

في ملف `src/config.py`، قم بتحديث:

```python
# Twilio Configuration
TWILIO_ACCOUNT_SID = "your_actual_account_sid"
TWILIO_AUTH_TOKEN = "your_actual_auth_token"
TWILIO_PHONE_NUMBER = "whatsapp:+14155238886"  # رقم Sandbox أو رقمك المعتمد
```

### 3. خيارات النشر

#### أ) النشر على Heroku

1. **تثبيت Heroku CLI:**
```bash
# على Ubuntu/Debian
curl https://cli-assets.heroku.com/install.sh | sh
```

2. **إعداد المشروع:**
```bash
cd whatsapp-ai-bot
git init
git add .
git commit -m "Initial commit"
```

3. **إنشاء تطبيق Heroku:**
```bash
heroku create your-whatsapp-bot-name
```

4. **إعداد متغيرات البيئة:**
```bash
heroku config:set TWILIO_ACCOUNT_SID=your_account_sid
heroku config:set TWILIO_AUTH_TOKEN=your_auth_token
heroku config:set TWILIO_PHONE_NUMBER=whatsapp:+14155238886
```

5. **النشر:**
```bash
git push heroku main
```

#### ب) النشر على Railway

1. اذهب إلى [railway.app](https://railway.app)
2. اربط حساب GitHub
3. ارفع المشروع إلى GitHub
4. أنشئ مشروع جديد في Railway
5. اربطه بمستودع GitHub
6. أضف متغيرات البيئة في إعدادات Railway

#### ج) النشر على DigitalOcean App Platform

1. اذهب إلى [cloud.digitalocean.com](https://cloud.digitalocean.com)
2. أنشئ App جديد
3. اربطه بمستودع GitHub
4. اختر Python كبيئة التشغيل
5. أضف متغيرات البيئة

### 4. إعداد Webhook في Twilio

بعد النشر، ستحصل على URL للتطبيق (مثل: `https://your-app.herokuapp.com`)

1. اذهب إلى Twilio Console
2. Messaging > Settings > WhatsApp sandbox settings
3. في حقل "When a message comes in"، أدخل:
   ```
   https://your-app-url.com/bot/webhook
   ```
4. اختر HTTP POST
5. احفظ الإعدادات

### 5. اختبار البوت

1. **أرسل رسالة إلى رقم Twilio Sandbox:**
   - أرسل الكود المطلوب أولاً (مثل: `join <code>`)
   - ثم أرسل أي رسالة للاختبار

2. **أوامر تغيير اللغة:**
   - `عربي` أو `arabic` أو `ar` - للعربية
   - `italiano` أو `italian` أو `it` - للإيطالية

3. **اختبار الردود:**
   - أرسل أسئلة باللغة العربية أو الإيطالية
   - تأكد من أن البوت يرد بنفس اللغة

## استكشاف الأخطاء

### مشاكل شائعة:

1. **خطأ في OpenAI API:**
   - تأكد من صحة مفتاح API
   - تأكد من وجود رصيد في حساب OpenAI

2. **خطأ في Twilio:**
   - تأكد من صحة Account SID و Auth Token
   - تأكد من إعداد Webhook بشكل صحيح

3. **خطأ في النشر:**
   - تأكد من وجود جميع الملفات المطلوبة
   - تأكد من صحة requirements.txt

### فحص السجلات:

```bash
# على Heroku
heroku logs --tail

# على Railway
# استخدم واجهة الويب لعرض السجلات
```

## الأمان

1. **لا تشارك مفاتيح API:**
   - استخدم متغيرات البيئة دائماً
   - لا تضع المفاتيح في الكود مباشرة

2. **تحديث المفاتيح بانتظام:**
   - غير مفاتيح API بشكل دوري
   - راقب الاستخدام في لوحات التحكم

## الدعم والصيانة

- راقب استخدام OpenAI API لتجنب تجاوز الحدود
- راقب رسائل Twilio لتجنب الرسوم الزائدة
- احتفظ بنسخ احتياطية من قاعدة البيانات
- حدث المكتبات بانتظام للأمان

## ملاحظات مهمة

1. **مفتاح OpenAI المقدم:**
   - تم تضمين مفتاح OpenAI في الكود
   - يُنصح بتغييره لمفتاح خاص بك لضمان الأمان

2. **حدود الاستخدام:**
   - OpenAI له حدود استخدام وتكلفة
   - Twilio له تكلفة لكل رسالة

3. **التطوير المستقبلي:**
   - يمكن إضافة المزيد من اللغات
   - يمكن تحسين خوارزمية تحديد اللغة
   - يمكن إضافة ميزات إضافية مثل الصور والملفات

