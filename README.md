# بوت واتساب بالذكاء الاصطناعي

بوت واتساب ذكي يدعم اللغتين العربية والإيطالية، مدعوم بـ OpenAI GPT.

## الميزات

- 🤖 ردود ذكية باستخدام OpenAI GPT
- 🌍 دعم اللغتين العربية والإيطالية
- 📱 تكامل مع واتساب عبر Twilio
- 💾 حفظ المحادثات وتفضيلات المستخدمين
- 🔄 تبديل اللغة التلقائي واليدوي

## المتطلبات

- Python 3.11+
- حساب Twilio مع WhatsApp API
- مفتاح OpenAI API
- Flask

## التثبيت

1. استنساخ المشروع:
```bash
git clone <repository-url>
cd whatsapp-ai-bot
```

2. إنشاء بيئة افتراضية:
```bash
python -m venv venv
source venv/bin/activate  # على Linux/Mac
# أو
venv\Scripts\activate  # على Windows
```

3. تثبيت المتطلبات:
```bash
pip install -r requirements.txt
```

4. إعداد متغيرات البيئة:
```bash
export TWILIO_ACCOUNT_SID="your_account_sid"
export TWILIO_AUTH_TOKEN="your_auth_token"
export TWILIO_PHONE_NUMBER="whatsapp:+14155238886"
```

## الإعداد

### 1. إعداد Twilio

1. إنشاء حساب على [Twilio](https://www.twilio.com/)
2. الحصول على Account SID و Auth Token
3. تفعيل WhatsApp Sandbox أو الحصول على رقم WhatsApp Business
4. إعداد Webhook URL في إعدادات Twilio

### 2. إعداد OpenAI

1. الحصول على مفتاح API من [OpenAI](https://platform.openai.com/)
2. تحديث المفتاح في ملف `src/config.py`

## التشغيل

```bash
cd src
python main.py
```

سيعمل الخادم على `http://0.0.0.0:5000`

## استخدام البوت

### أوامر تغيير اللغة:
- `عربي` أو `arabic` أو `ar` - للتبديل إلى العربية
- `italiano` أو `italian` أو `it` - للتبديل إلى الإيطالية

### الاستخدام العادي:
أرسل أي رسالة للبوت وسيرد عليك بالذكاء الاصطناعي باللغة المحددة.

## API Endpoints

- `POST /bot/webhook` - استقبال رسائل واتساب
- `GET /bot/status` - فحص حالة البوت
- `GET /bot/stats` - إحصائيات البوت

## هيكل المشروع

```
whatsapp-ai-bot/
├── src/
│   ├── config.py              # إعدادات التطبيق
│   ├── main.py               # نقطة الدخول الرئيسية
│   ├── models/
│   │   └── user.py           # نماذج قاعدة البيانات
│   ├── routes/
│   │   ├── bot.py            # مسارات البوت
│   │   └── user.py           # مسارات المستخدمين
│   ├── services/
│   │   ├── openai_service.py # خدمة OpenAI
│   │   └── twilio_service.py # خدمة Twilio
│   └── database/
│       └── app.db            # قاعدة بيانات SQLite
├── requirements.txt          # متطلبات Python
└── README.md                # هذا الملف
```

## النشر

يمكن نشر البوت على منصات مختلفة مثل:
- Heroku
- AWS Lambda
- Google Cloud Functions
- DigitalOcean App Platform

تأكد من إعداد متغيرات البيئة المطلوبة على منصة النشر.

## الدعم

للمساعدة أو الإبلاغ عن مشاكل، يرجى فتح issue في المستودع.

