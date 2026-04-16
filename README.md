<p align="center">
  <img src="https://img.shields.io/badge/Laravel-11-FF2D20?style=for-the-badge&logo=laravel&logoColor=white" alt="Laravel 11">
  <img src="https://img.shields.io/badge/Filament-3-FDAE4B?style=for-the-badge&logo=filament&logoColor=white" alt="Filament 3">
  <img src="https://img.shields.io/badge/Livewire-3-FB70A9?style=for-the-badge&logo=livewire&logoColor=white" alt="Livewire 3">
  <img src="https://img.shields.io/badge/PHP-8.2+-777BB4?style=for-the-badge&logo=php&logoColor=white" alt="PHP 8.2+">
  <img src="https://img.shields.io/badge/MySQL-8-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL 8">
</p>

<h1 align="center">🏛️ مسار — MASAR</h1>
<h3 align="center">نظام إدارة الوزارات المتكامل</h3>
<p align="center">Integrated Ministry Management System</p>

---

## 📋 نبذة عن المشروع

**مسار** هو نظام حكومي متكامل مبني بهيكل **Modular Monolith** باستخدام Laravel 11. يوفّر حلولاً شاملة لإدارة الوزارات والهيئات الحكومية من خلال خمس وحدات أساسية تتشارك نفس قاعدة البيانات والمستخدمين:

| الوحدة | الوصف |
|--------|-------|
| 🏢 **Core** | الهيكل التنظيمي: الوزارات، الوحدات، المستخدمون، المدن، الإعدادات |
| 👥 **HR** | الموارد البشرية: الموظفون، الحضور، الإجازات، التقييم، الترقيات، التدريب |
| 💰 **Finance** | المالية: الرواتب، الميزانيات، أوامر الصرف، البدلات، الخصومات |
| 📁 **Archive** | الأرشفة: الوثائق، المراسلات الرسمية، التصنيف الذكي |
| 🔒 **Security** | الأمن: سجل التدقيق، التنبيهات، الجلسات، حظر IP، سياسات كلمات المرور |

---

## 🛠️ التقنيات المستخدمة

### Backend
| التقنية | الإصدار | الغرض |
|---------|---------|-------|
| Laravel | 11 | إطار العمل الرئيسي |
| PHP | 8.2+ | لغة البرمجة |
| MySQL | 8 | قاعدة البيانات |
| Laravel Sanctum | 4.0 | مصادقة API |
| Laravel Scout | 11.0 | بحث فوري |
| nwidart/laravel-modules | 11.0 | هيكل الوحدات المستقلة |
| Spatie Permission | 6.0 | الأدوار والصلاحيات |
| Spatie Activity Log | 4.12 | تسجيل النشاطات |
| Maatwebsite Excel | 3.1 | استيراد/تصدير Excel |

### Frontend
| التقنية | الإصدار | الغرض |
|---------|---------|-------|
| Filament | 3.2 | لوحة الإدارة والنماذج |
| Livewire | 3.5 | واجهات تفاعلية بدون JavaScript |
| Tailwind CSS | 3 | التصميم |
| Alpine.js | — | تفاعلات خفيفة |

---

## 📂 هيكل المشروع

```
masar/
├── app/
│   ├── Filament/
│   │   ├── Pages/              ← صفحات مخصصة (Dashboard, SecurityDashboard)
│   │   ├── Resources/
│   │   │   ├── Archive/        ← DocumentResource, CorrespondenceResource
│   │   │   ├── Finance/        ← PaymentOrderResource + 8 موارد مالية
│   │   │   ├── HR/             ← PersonnelResource + 6 موارد بشرية
│   │   │   └── Security/       ← AuditLogResource + 3 موارد أمنية
│   │   └── Widgets/            ← 4 ودجات إحصائية
│   └── Providers/
│       ├── AppServiceProvider.php
│       └── Filament/
│           └── AdminPanelProvider.php
│
├── Modules/
│   ├── Core/
│   │   ├── Models/             ← Ministry, Unit, User, City, Setting
│   │   ├── Policies/
│   │   └── Database/Migrations/
│   │
│   ├── HR/
│   │   ├── Models/             ← Personnel, Leave, Attendance, RankHistory...
│   │   ├── Enums/
│   │   ├── Policies/
│   │   └── Database/Migrations/
│   │
│   ├── Finance/
│   │   ├── Models/             ← PayrollRun, PayrollItem, Budget, Expense...
│   │   ├── Policies/
│   │   └── Database/Migrations/
│   │
│   ├── Archive/
│   │   ├── Models/             ← Document, Correspondence
│   │   ├── Enums/              ← DocumentCategory, ClassificationLevel, DocumentStatus
│   │   ├── Policies/
│   │   └── Database/Migrations/
│   │
│   └── Security/
│       ├── Models/             ← AuditLog, SecurityAlert, LoginAttempt...
│       ├── Middleware/         ← ForcePasswordChange, CheckIpBlacklist
│       ├── Policies/
│       └── Database/Migrations/
│
├── resources/views/
│   ├── welcome.blade.php       ← الصفحة الترحيبية
│   └── filament/
│       ├── pages/              ← security-dashboard
│       ├── widgets/            ← finance-3d-widget
│       └── components/         ← 3d-background
│
├── database/migrations/        ← الهجرات الأساسية
├── public/css/custom-filament.css
├── bootstrap/app.php
└── composer.json
```

---

## 👥 الأدوار والصلاحيات

| الدور | الوصف | النطاق |
|-------|-------|--------|
| `super_admin` | صلاحيات كاملة | كل النظام وكل الوزارات |
| `ministry_admin` | مدير وزارة | وزارته فقط |
| `hr_manager` | مدير الموارد البشرية | وحدة HR |
| `hr_officer` | موظف HR | إدخال وتعديل بيانات |
| `finance_manager` | مدير المالية | وحدة Finance |
| `finance_officer` | موظف مالية | إدخال وتعديل |
| `archive_manager` | مدير الأرشفة | وحدة Archive |
| `archive_officer` | موظف أرشفة | إدخال وتعديل |
| `security_officer` | مسؤول الأمن | وحدة Security + التدقيق |
| `viewer` | عرض فقط | بدون تعديل |

---

## 🗄️ قاعدة البيانات

### الجداول الأساسية (Core)
- `ministries` — الوزارات
- `units` — الوحدات/الإدارات (هيكل هرمي)
- `users` — مستخدمو النظام
- `cities` — المدن
- `settings` — إعدادات النظام

### جداول الموارد البشرية (HR) — 8 جداول
- `personnel` — الملف الأساسي للموظف (40+ حقل)
- `rank_history` — سجل الترقيات
- `service_records` — سجل الخدمة
- `leaves` — الإجازات
- `leave_balances` — رصيد الإجازات
- `attendance` — الحضور والانصراف
- `performance_reviews` — تقييم الأداء
- `training_records` — الدورات التدريبية

### جداول المالية (Finance) — 7 جداول
- `salary_grades` — درجات الرواتب
- `allowance_types` — أنواع البدلات
- `deduction_types` — أنواع الخصومات
- `personnel_salary_config` — تكوين راتب الموظف
- `payroll_runs` — دورات الرواتب الشهرية
- `payroll_items` — تفاصيل راتب كل موظف
- `budgets` — الميزانيات
- `expenses` — المصروفات
- `payment_orders` — أوامر الصرف

### جداول الأرشفة (Archive) — 4 جداول
- `documents` — الوثائق
- `correspondences` — المراسلات الرسمية
- `import_logs` — سجل الاستيرادات
- `export_files` — ملفات التصدير

### جداول الأمن (Security) — 5 جداول
- `audit_logs` — سجل التدقيق (لا يُحذف أبداً)
- `login_attempts` — محاولات الدخول
- `active_sessions` — الجلسات النشطة
- `security_alerts` — تنبيهات الأمن
- `ip_blacklist` — القائمة السوداء
- `password_policies` — سياسات كلمات المرور

---

## ✨ المميزات الرئيسية

### الموارد البشرية
- ✅ ملف موظف شامل (40+ حقل مع وثائق وسجلات)
- ✅ الهيكل التنظيمي الهرمي للوزارات
- ✅ نظام إجازات إلكتروني مع سير عمل موافقة
- ✅ تتبع الحضور اليومي (بصمة، QR، يدوي)
- ✅ تقييم الأداء السنوي/ربع السنوي
- ✅ سجل الترقيات والرتب
- ✅ سجل الدورات التدريبية والشهادات
- ✅ استيراد/تصدير Excel بالجملة

### المالية
- ✅ إعداد مسيرات الرواتب الشهرية تلقائياً
- ✅ بدلات وخصومات مرنة وقابلة للتخصيص
- ✅ ربط الغياب والتأخر بخصم الراتب
- ✅ إدارة ميزانيات الوزارات والوحدات
- ✅ أوامر صرف مع سير عمل موافقة
- ✅ تقارير مالية تفصيلية

### الأرشفة
- ✅ أرشفة الوثائق مع تصنيف ذكي
- ✅ إدارة المراسلات (واردة، صادرة، داخلية)
- ✅ أرقام مراسلات تسلسلية تلقائية
- ✅ مستويات سرية للوثائق
- ✅ تنبيهات انتهاء صلاحية الوثائق

### الأمن
- ✅ سجل تدقيق شامل لكل عملية
- ✅ تنبيهات أمنية فورية (محاولات اختراق، وصول مشبوه)
- ✅ حظر IP تلقائي بعد محاولات فاشلة
- ✅ مراقبة الجلسات النشطة
- ✅ سياسة كلمات مرور قابلة للتخصيص
- ✅ لوحة تحكم أمن مباشرة

---

## 🚀 التثبيت والتشغيل

### المتطلبات
- PHP 8.2 أو أعلى
- MySQL 8
- Composer
- Node.js (اختياري — لبناء الأصول عبر Vite)
- XAMPP أو أي خادم محلي

### خطوات التثبيت

```bash
# 1. استنساخ المشروع
git clone <repository-url> masar
cd masar

# 2. تثبيت المكتبات
composer install

# 3. إعداد ملف البيئة
cp .env.example .env
php artisan key:generate

# 4. تكوين قاعدة البيانات في ملف .env
# DB_DATABASE=masar
# DB_USERNAME=root
# DB_PASSWORD=

# 5. تشغيل الهجرات وبذر البيانات
php artisan migrate --seed

# 6. ربط مجلد التخزين
php artisan storage:link

# 7. تحسين الأداء
php artisan optimize

# 8. تشغيل السيرفر
php artisan serve
```

### تفعيل OPcache (مهم للأداء)
أضف إلى `php.ini`:
```ini
zend_extension=opcache

[opcache]
opcache.enable=1
opcache.memory_consumption=256
opcache.max_accelerated_files=20000
opcache.revalidate_freq=60
```
ثم أعد تشغيل PHP.

---

## 🔗 الروابط الأساسية

| الرابط | الوصف |
|--------|-------|
| `http://localhost:8000/` | الصفحة الترحيبية |
| `http://localhost:8000/admin/login` | تسجيل الدخول |
| `http://localhost:8000/admin` | لوحة التحكم الرئيسية |

---

## ⚡ تحسينات الأداء المُطبّقة

| التحسين | التأثير |
|---------|---------|
| وضع SPA (`->spa()`) في Filament | تنقل بدون إعادة تحميل كامل |
| OPcache | تسريع PHP بـ 2-5x |
| تحميل كسول للودجات (`$isLazy = true`) | لوحة التحكم تظهر فوراً |
| تحديث الودجات كل 60 ثانية (`$pollingInterval`) | تقليل استعلامات DB |
| كاش فحص IP (`Cache::remember`) | استعلام واحد كل 60 ثانية |
| `php artisan optimize` | تخزين Routes, Config, Views |
| CSS بدون blur/backdrop-filter/animations | صفر استهلاك GPU |
| استثناء logout من CSRF | تسجيل خروج فوري |

---

## 📊 لوحة التحكم (Dashboard)

تعرض لوحة التحكم الرئيسية أربع مجموعات إحصائية:

- **📊 الموارد البشرية** — إجمالي الموظفين، حاضرون اليوم، إجازات معلقة
- **📁 الأرشفة** — إجمالي الوثائق، المراسلات، وثائق ستنتهي قريباً
- **🔒 الأمن** — تنبيهات غير محلولة، محاولات الدخول، جلسات نشطة
- **💰 المالية** — إجمالي المنصرف، الموظفين ضمن المسير

---

## 🔐 الأمان

- جميع الصلاحيات مُدارة عبر **Spatie Permission** مع سياسات (Policies) مسجلة في `AppServiceProvider`
- **CSRF protection** على جميع المسارات
- **IP Blacklist middleware** مع كاش ذكي
- **Force Password Change middleware** لفرض تغيير كلمة المرور
- **سجل تدقيق** لكل عملية (لا يُحذف)
- **حظر تلقائي** بعد 5 محاولات دخول فاشلة

---

## 📁 هيكل واجهات Filament (30+ واجهة)

### Core (3 واجهات)
`MinistryResource` · `UnitResource` · `UserResource`

### الموارد البشرية (7 واجهات)
`PersonnelResource` · `LeaveBalanceResource` · `PerformanceReviewResource` · `RankHistoryResource` · `ServiceRecordResource` · `TrainingRecordResource` · `AttendanceResource`

### المالية (9 واجهات)
`PayrollRunResource` · `PayrollItemResource` · `SalaryGradeResource` · `AllowanceTypeResource` · `DeductionTypeResource` · `PersonnelSalaryConfigResource` · `BudgetResource` · `ExpenseResource` · `PaymentOrderResource`

### الأرشفة (2 واجهات)
`DocumentResource` · `CorrespondenceResource`

### الأمن (4 واجهات)
`AuditLogResource` · `SecurityAlertResource` · `LoginAttemptResource` · `PasswordPolicyResource`

### الصفحات المخصصة
`MinistryDashboard` · `SecurityDashboard` · `DatabaseImport`

---

## 👨‍💻 المطور

<table>
  <tr>
    <td><strong>الاسم</strong></td>
    <td>محمد أمين الجراش</td>
  </tr>
  <tr>
    <td><strong>المشروع</strong></td>
    <td>نظام مسار — MASAR</td>
  </tr>
</table>

---

## 📄 الرخصة

هذا المشروع محمي بحقوق الملكية الفكرية. جميع الحقوق محفوظة © {{ date('Y') }}.
