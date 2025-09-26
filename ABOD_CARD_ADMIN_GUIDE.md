# دليل الإدارة الشامل - Abod Card System
## دليل تعديل وإدارة النظام بالكامل

---

## 📋 جدول المحتويات
1. [تعديل المفاجآت اليومية](#daily-surprises)
2. [إدارة العروض والكوبونات](#offers)
3. [إدارة المنتجات](#products)
4. [إدارة الفئات](#categories)
5. [إدارة الأكواد](#codes)
6. [التعامل مع قاعدة البيانات](#database)
7. [تعديل النصوص والرسائل](#texts)
8. [إعادة تشغيل النظام](#restart)

---

## 🎁 تعديل المفاجآت اليومية {#daily-surprises}

### 📂 المكان: `/app/backend/offers_config.py`

```python
# المفاجآت اليومية (يمكن تخصيصها حسب اليوم)
DAILY_SURPRISES = [
    "🎮 خصم 20% على جميع بطاقات الألعاب",
    "💳 شحن مجاني للطلبات فوق $30",
    "🎁 بطاقة هدايا مجانية مع كل شحن $100",
    "⚡ تسليم مضاعف السرعة اليوم فقط",
    "🌟 نقاط مضاعفة لكل عملية شراء"
]
```

### 🔧 طريقة التعديل:
1. افتح ملف `/app/backend/offers_config.py`
2. عدل قائمة `DAILY_SURPRISES`
3. أضف أو احذف العروض حسب الحاجة
4. احفظ الملف
5. أعد تشغيل الخادم: `sudo supervisorctl restart backend`

### 💡 مثال تعديل:
```python
DAILY_SURPRISES = [
    "🎮 خصم 25% على PlayStation Cards",
    "💎 عرض خاص: اشتري 2 واحصل على 1 مجاناً",
    "🚀 تسليم فوري لجميع الطلبات اليوم",
    "💰 كاش باك 15% على كل عملية شراء"
]
```

---

## 🔥 إدارة العروض والكوبونات {#offers}

### 📂 المكان: `/app/backend/offers_config.py`

### العروض الأساسية:
```python
CURRENT_OFFERS = [
    "🎮 خصم 15% على بطاقات الألعاب",
    "💳 خصم 10% على بطاقات Google Play",  
    "🎵 عروض خاصة على اشتراكات البرامج",
    "🛍️ شحن مجاني للطلبات فوق $50"
]
```

### أكواد الكوبونات:
```python
COUPON_CODES = {
    "WELCOME10": "خصم 10% للعملاء الجدد",
    "VIP15": "خصم 15% للعضوية الذهبية", 
    "DAILY20": "خصم يومي 20%",
    "FREE50": "شحن مجاني للطلبات فوق $50"
}
```

### رسالة العروض الإضافية:
```python
OFFERS_FOOTER = """
📞 للاستفادة من العروض تواصل مع الدعم الفني أو اطلب منتجك الآن!

⏰ العروض سارية حتى نفاد الكمية أو انتهاء المدة المحددة

🎁 للحصول على أكواد الخصم، تواصل مع الدعم الفني
💬 @AbodStoreVIP"""
```

---

## 📦 إدارة المنتجات {#products}

### عبر بوت الإدارة:
1. بوت الإدارة → إدارة المنتجات
2. ➕ إضافة منتج / ✏️ تعديل منتج / 🗑 حذف منتج

### عبر قاعدة البيانات مباشرة:

#### إضافة منتج جديد:
```javascript
// في MongoDB
db.products.insertOne({
    "id": "product_uuid_here",
    "name": "اسم المنتج",
    "description": "وصف المنتج",
    "terms": "شروط وأحكام المنتج",
    "is_active": true,
    "created_at": new Date()
})
```

#### تعديل منتج:
```javascript
db.products.updateOne(
    {"name": "اسم المنتج القديم"},
    {
        "$set": {
            "name": "الاسم الجديد",
            "description": "الوصف الجديد",
            "terms": "الشروط الجديدة"
        }
    }
)
```

#### حذف منتج:
```javascript
db.products.deleteOne({"name": "اسم المنتج"})
```

#### عرض جميع المنتجات:
```javascript
db.products.find().pretty()
```

---

## 🏷️ إدارة الفئات {#categories}

### عبر بوت الإدارة:
1. بوت الإدارة → إدارة المنتجات → إضافة فئة

### عبر قاعدة البيانات:

#### إضافة فئة جديدة:
```javascript
db.categories.insertOne({
    "id": "category_uuid_here",
    "name": "اسم الفئة",
    "description": "وصف الفئة",
    "category_type": "نوع الفئة",
    "price": 10.00,
    "delivery_type": "code", // أو "phone", "email", "id", "manual"
    "redemption_method": "طريقة الاسترداد",
    "terms": "الشروط والأحكام",
    "image_url": "رابط الصورة (اختياري)",
    "product_id": "معرف المنتج المرتبط",
    "created_at": new Date()
})
```

#### تعديل فئة:
```javascript
db.categories.updateOne(
    {"name": "اسم الفئة"},
    {
        "$set": {
            "price": 15.00,
            "description": "وصف جديد",
            "delivery_type": "manual"
        }
    }
)
```

#### حذف فئة:
```javascript
db.categories.deleteOne({"name": "اسم الفئة"})
```

#### عرض الفئات حسب نوع التسليم:
```javascript
db.categories.find({"delivery_type": "code"}).pretty()
```

---

## 🎫 إدارة الأكواد {#codes}

### عبر بوت الإدارة:
1. بوت الإدارة → إدارة الأكواد → إضافة أكواد

### عبر قاعدة البيانات:

#### إضافة كود واحد:
```javascript
db.codes.insertOne({
    "id": "code_uuid_here",
    "code": "ABC123DEF456",
    "description": "وصف الكود",
    "terms": "شروط الاستخدام",
    "category_id": "معرف الفئة",
    "code_type": "text", // أو "number", "dual"
    "serial_number": "1234567890", // للنوع dual فقط
    "is_used": false,
    "used_by": null,
    "used_at": null,
    "created_at": new Date()
})
```

#### إضافة أكواد متعددة (مجموعة):
```javascript
// مثال لإضافة 10 أكواد
var codes = [];
for(var i = 1; i <= 10; i++) {
    codes.push({
        "id": "code_" + i + "_uuid",
        "code": "GAME" + (1000 + i),
        "description": "كود لعبة",
        "terms": "صالح لمدة سنة",
        "category_id": "معرف_فئة_الألعاب",
        "code_type": "text",
        "is_used": false,
        "created_at": new Date()
    });
}
db.codes.insertMany(codes);
```

#### البحث عن الأكواد المتاحة:
```javascript
db.codes.find({
    "category_id": "معرف_الفئة",
    "is_used": false
}).pretty()
```

#### عدد الأكواد المتاحة لكل فئة:
```javascript
db.codes.aggregate([
    {$match: {"is_used": false}},
    {$group: {_id: "$category_id", count: {$sum: 1}}}
])
```

---

## 🗄️ التعامل مع قاعدة البيانات {#database}

### الاتصال بقاعدة البيانات:
```bash
# من داخل الكونتينر
mongo mongodb://localhost:27017/abod_card_db
```

### العمليات الأساسية:

#### عرض جميع المجموعات:
```javascript
show collections
```

#### عرض المستخدمين:
```javascript
db.users.find().pretty()
```

#### عرض الطلبات:
```javascript
db.orders.find().pretty()
```

#### البحث عن مستخدم معين:
```javascript
db.users.find({"telegram_id": 123456789})
```

#### عرض الطلبات المعلقة فقط:
```javascript
db.orders.find({"status": "pending"}).pretty()
```

#### حذف الطلبات القديمة (أكثر من شهر):
```javascript
var oneMonthAgo = new Date();
oneMonthAgo.setMonth(oneMonthAgo.getMonth() - 1);
db.orders.deleteMany({
    "order_date": {"$lt": oneMonthAgo},
    "status": "completed"
})
```

#### عمل نسخة احتياطية من البيانات:
```bash
mongodump --db abod_card_db --out /backup/
```

#### استعادة النسخة الاحتياطية:
```bash
mongorestore /backup/abod_card_db/
```

---

## 📝 تعديل النصوص والرسائل {#texts}

### 📂 المكان: `/app/backend/server.py`

### رسائل الترحيب:
ابحث عن: `مرحباً بك`
```python
welcome_text = f"""مرحباً {name}! 

💰 رصيدك: ${user_balance:.2f}
🆔 معرف حسابك: `{telegram_id}`"""
```

### رسائل النجاح:
ابحث عن: `تم الشراء بنجاح`
```python
success_text = f"""✅ *تم الشراء بنجاح!*

📦 المنتج: *{product['name']}*"""
```

### رسائل الأخطاء:
ابحث عن: `حدث خطأ`
```python
error_text = "❌ حدث خطأ أثناء معالجة طلبك"
```

### رسائل الدعم الفني:
ابحث عن: `الدعم الفني`
```python
support_text = """💬 *الدعم الفني*

للحصول على المساعدة: @AbodStoreVIP"""
```

---

## 🔄 إعادة تشغيل النظام {#restart}

### إعادة تشغيل الخادم الخلفي فقط:
```bash
sudo supervisorctl restart backend
```

### إعادة تشغيل النظام كاملاً:
```bash
sudo supervisorctl restart all
```

### التحقق من حالة الخدمات:
```bash
sudo supervisorctl status
```

### عرض سجلات الأخطاء:
```bash
tail -f /var/log/supervisor/backend.err.log
```

---

## 🚨 نصائح مهمة للأمان

### 1. عمل نسخة احتياطية قبل أي تعديل:
```bash
# نسخة احتياطية من قاعدة البيانات
mongodump --db abod_card_db --out /backup/$(date +%Y%m%d)/

# نسخة احتياطية من الكود
cp -r /app/backend /backup/code_$(date +%Y%m%d)/
```

### 2. اختبار التعديلات:
- اختبر أي تعديل على بيئة تطوير أولاً
- تأكد من عمل جميع الوظائف بعد التعديل
- راجع سجلات الأخطاء بانتظام

### 3. مراقبة النظام:
```bash
# مراقبة استخدام الذاكرة
free -h

# مراقبة استخدام القرص
df -h

# مراقبة العمليات
top
```

---

## 📞 الدعم والمساعدة

إذا واجهت أي مشاكل:
1. تحقق من سجلات الأخطاء أولاً
2. تأكد من إعادة تشغيل الخدمات بعد التعديل
3. راجع هذا الدليل للتأكد من الخطوات
4. تواصل مع فريق التطوير عند الحاجة

---

**📝 آخر تحديث:** سبتمبر 2025
**📧 للدعم:** استخدم نظام الدعم في Emergent