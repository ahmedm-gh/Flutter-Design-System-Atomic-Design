# 🎨 Flutter Design System & Atomic Design - Complete Guide 2026

دليل شامل ومزدوج اللغة (عربي / إنجليزي) لبناء Design System احترافي في Flutter باستخدام منهجية Atomic Design.

## Table of Contents / جدول المحتويات

1. [Why a Design System? / لماذا نحتاج Design System؟](#1-why-a-design-system--لماذا-نحتاج-design-system)
2. [Tokens / الرموز الأساسية](#2-tokens--الرموز-الأساسية)
3. [Atomic Design Layers / طبقات Atomic Design](#3-atomic-design-layers--طبقات-atomic-design)
4. [Theme System / نظام الثيم](#4-theme-system--نظام-الثيم)
5. [Typography / الطباعة](#5-typography--الطباعة)
6. [Components Deep Dive / تعمق في المكونات](#6-components-deep-dive--تعمق-في-المكونات)
7. [Assets Management / إدارة الأصول](#7-assets-management--إدارة-الأصول)
8. [Project Structure / هيكل المشروع](#8-project-structure--هيكل-المشروع)
9. [Testing & Widgetbook / الاختبار والكتالوج](#9-testing--widgetbook--الاختبار-والكتالوج)
10. [Best Practices & Anti-Patterns / أفضل الممارسات والأخطاء الشائعة](#10-best-practices--anti-patterns--أفضل-الممارسات-والأخطاء-الشائعة)

### 🚥 Difficulty Levels / مستويات الصعوبة

🟢 **Foundational / أساسي**\
🟡 **Intermediate / متوسط**\
🔴 **Advanced / متقدم**

---

## 1. Why a Design System? / لماذا نحتاج Design System؟

### 🟢 Step 1: Understand the Design System and the Problems it Solves

*الخطوة 1: فهم الـ Design System والمشكلة التي يحلها*

**What it solves:**

* Eliminates visual inconsistency across screens and platforms.
* Removes redundant code - one component, used everywhere.
* Enables a single package shared across mobile, web, and desktop.
* Bridges the gap between designers and developers with shared language.

**المشكلات التي يحلها:**

* يُنهي حالة التضارب البصري بين الشاشات والمنصات المختلفة.
* يُلغي تكرار الكود - مكوّن واحد يُستخدم في كل مكان.
* يتيح مشاركة باكدج واحد بين Mobile وWeb وDesktop.
* يُجسّر الهوّة بين المصمم والمطور بلغة مشتركة وموحدة.

> [!IMPORTANT]
> A Design System is a **product inside your product** - it needs ownership, versioning, and maintenance like any other package.
>
> الـ Design System هو **منتج داخل منتجك** - يحتاج مالكاً وإصداراً وصيانة مستمرة مثل أي باكدج آخر.

---

### 🟢 Step 2: Explore Atomic Design Fundamentals and its Origins

*الخطوة 2: استكشاف أساسيات Atomic Design ومن ابتكره*

**Atomic Design Fundamentals:**

* Coined by **Brad Frost** - inspired by chemistry's atomic structure.
* Breaks UI into 5 hierarchical layers: Tokens → Atoms → Molecules → Organisms → Templates → Pages.
* Forces developers to think in components, not screens.
* Works universally - React, Vue, SwiftUI, and Flutter alike.

**أساسيات Atomic Design:**

* ابتكره **Brad Frost** - مستوحى من البنية الذرية في الكيمياء.
* يُقسّم الواجهة إلى 5 طبقات هرمية: Tokens ← Atoms ← Molecules ← Organisms ← Templates ← Pages.
* يُجبر المطور على التفكير بالمكونات لا بالشاشات كاملة.
* يعمل عالمياً - React وVue وSwiftUI وFlutter على حدٍّ سواء.

---

### 🟡 Step 3: Identify the Measurable Benefits of Adopting a Design System

*الخطوة 3: تحديد الفوائد القابلة للقياس من تبني Design System*

**Measurable Benefits:**

* **80% reduction** in time-to-market for new screens.
* **Zero** color or spacing inconsistencies across the app.
* New developer onboarding reduced from days to hours.
* Dark mode support requires changes in **one place only**.
* QA effort drops - pre-tested atoms mean fewer regressions.

**الفوائد القابلة للقياس:**

* **تخفيض 80%** في وقت تسليم الشاشات الجديدة.
* **صفر** تضارب في الألوان أو المسافات عبر التطبيق.
* تأهيل المطور الجديد يتقلص من أيام إلى ساعات.
* دعم الـ Dark Mode يتطلب تعديلاً في **مكان واحد فقط**.
* جهد الـ QA ينخفض - atoms مُختبرة مسبقاً = رجعات أقل.

---

## 2. Tokens / الرموز الأساسية

### 🟢 Step 4: Define Design Tokens and their Naming Rules

*الخطوة 4: تعريف الـ Design Tokens وقواعد تسميتها*

**Design Tokens Rules:**

* Raw primitive values - colors, sizes, radii, shadows, durations.
* Named semantically, not by usage: `brand.500` NOT `buttonColor`.
* Only the design team defines token values - developers consolidate them.
* Changing one token propagates the change to every consumer automatically.

**قواعد الـ Design Tokens:**

* قيم خام أولية - ألوان وأحجام وزوايا وظلال ومدد زمنية.
* تُسمى دلالياً لا باستخدامها: `brand.500` وليس `buttonColor`.
* فريق التصميم فقط يحدد قيم الـ tokens - المطور يُجمّعها فقط.
* تغيير token واحد ينتشر تلقائياً لكل مكان يستخدمه.

---

### 🟡 Step 5: Implement AppColors with Full Palette Support

*الخطوة 5: تنفيذ AppColors مع دعم كامل للـ palette*

**AppColors Implementation:**

```dart
/// {@template app_colors}
/// Colors class for themes - provides direct access via static fields.
/// {@endtemplate}
abstract final class AppColors {

  static const white       = Colors.white;
  static const black       = Colors.black;
  static const transparent = Colors.transparent;

  /// Brand color palette - primary identity color.
  /// لوحة ألوان العلامة التجارية - اللون التعريفي الأساسي.
  static const brand = MaterialColor(
    0xFF347AF6,
    {
      50:  Color(0xFFF0F5FF), // Lightest / الأفتح
      100: Color(0xFFE0ECFF),
      200: Color(0xFFBDD3F9),
      300: Color(0xFF81ACF9),
      400: Color(0xFF5A93F9),
      500: Color(0xFF347AF6), // Primary / الأساسي
      600: Color(0xFF1559D1),
      700: Color(0xFF174EAF),
      800: Color(0xFF1D4387),
      900: Color(0xFF163367), // Darkest / الأغمق
    },
  );

  static const grayLight = MaterialColor(0xFF667085, { ... });
  static const error     = MaterialColor(0xFFF04438, { ... });
  static const success   = MaterialColor(0xFF12B76A, { ... });
  static const warning   = MaterialColor(0xFFF79009, { ... });
}
```

> [!NOTE]
> Use `MaterialColor` for brand palettes - it gives you shade access like `AppColors.brand.shade500` and works seamlessly with Flutter's theming.
>
> استخدم `MaterialColor` للـ palettes - يتيح الوصول كـ `AppColors.brand.shade500` ويتكامل مع نظام الثيم في Flutter.

---

### 🟡 Step 6: Define Spacing, Radius, and Shadow Tokens

*الخطوة 6: تعريف tokens الـ Spacing والـ Radius والـ Shadow*

**Spacing Tokens:**

```dart
/// {@template app_spacing}
/// All spacing values used across the app - horizontal and vertical alike.
/// جميع قيم التباعد المستخدمة - أفقية وعمودية على حدٍّ سواء.
/// {@endtemplate}
abstract final class AppSpacing {

  static const none = 0.0;
  static const xxs  = 2.0;
  static const xs   = 4.0;
  static const sm   = 6.0;
  static const md   = 8.0;
  static const lg   = 12.0;
  static const xl   = 16.0;
  static const xxl  = 24.0;
  static const xxxl = 32.0;
  static const huge = 48.0;
}
```

**Radius Tokens:**

```dart
/// {@template app_radius}
/// Border radius constants - use these instead of raw Radius.circular().
/// ثوابت نصف القطر - استخدمها بدلاً من Radius.circular() المباشرة.
/// {@endtemplate}
abstract final class AppRadius {

  static const none = Radius.zero;
  static const xxs  = Radius.circular(2);
  static const xs   = Radius.circular(4);
  static const sm   = Radius.circular(6);
  static const md   = Radius.circular(8);
  static const lg   = Radius.circular(12);
  static const xl   = Radius.circular(16);
  static const full = Radius.circular(999); // Pill shape / شكل حبة دواء
}
```

**Shadow Tokens:**

```dart
/// {@template app_shadow}
/// Elevation shadows - defined as List<BoxShadow> for direct use.
/// ظلال الارتفاع - مُعرّفة كـ List<BoxShadow> للاستخدام المباشر.
/// {@endtemplate}
abstract final class AppShadow {

  static const none = <BoxShadow>[];

  static const xs = [
    BoxShadow(
      blurRadius: 2,
      offset: Offset(0, 1),
      color: Color.fromRGBO(16, 24, 40, 0.05),
    ),
  ];

  static const sm = [
    BoxShadow(color: Color(0x0F101828), blurRadius: 2, offset: Offset(0, 1)),
    BoxShadow(color: Color(0x19101828), blurRadius: 3, offset: Offset(0, 1)),
  ];

  static const md = [
    BoxShadow(color: Color(0x0F101828), blurRadius: 4,  offset: Offset(0, 2)),
    BoxShadow(color: Color(0x19101828), blurRadius: 8,  offset: Offset(0, 4)),
  ];

  static const lg = [
    BoxShadow(color: Color(0x0F101828), blurRadius: 8,  offset: Offset(0, 4)),
    BoxShadow(color: Color(0x19101828), blurRadius: 16, offset: Offset(0, 8)),
  ];
}
```

> [!TIP]
> Define shadows as `static const List<BoxShadow>` so they can be used directly in `BoxDecoration.boxShadow` without any conversion.
>
> عرّف الظلال كـ `static const List<BoxShadow>` لاستخدامها مباشرة في `BoxDecoration.boxShadow` بدون أي تحويل.

---

## 3. Atomic Design Layers / طبقات Atomic Design

### 🟢 Step 7: Break Down the 5 Atomic Design Layers

*الخطوة 7: تفصيل طبقات Atomic Design الخمس ومحتوياتها*

**Layer Breakdown:**

| Layer / الطبقة | Contains / تحتوي | Flutter Equivalent / المقابل في Flutter |
|---|---|---|
| **Tokens** | Raw values / قيم خام | `class AppColors`, `AppSpacing` |
| **Atoms** | Indivisible widgets | `AppButton`, `AppTextField`, `AppIcon` |
| **Molecules** | 2+ atoms with one purpose | `SearchField`, `UserCard`, `FormRow` |
| **Organisms** | Complex, multi-responsibility | `LoginForm`, `AppHeader`, `ProductList` |
| **Templates** | Layout skeleton, no real data | `AuthTemplate`, `DashboardTemplate` |
| **Pages** | Template + real data + routing | `LoginPage`, `HomeScreen` |

**تفصيل الطبقات:**

```
Pages         ← شاشات كاملة مع بيانات حقيقية
  ↑
Templates     ← هيكل الشاشة بدون بيانات
  ↑
Organisms     ← مكونات معقدة متعددة المسؤوليات
  ↑
Molecules     ← مجموعة Atoms لغرض واحد
  ↑
Atoms         ← أصغر وحدة لا تنقسم
  ↑
Tokens        ← قيم خام (ألوان، مسافات، ظلال)
```

---

### 🟡 Step 8: Build a Base Atom (Abstract Button Pattern)

*الخطوة 8: بناء Atom أساسي (نمط الزر المجرد)*

**Abstract Button Atom:**

```dart
/// Typedef for icon builder - receives state color, returns Widget.
/// Typedef لبناء الأيقونة - يستقبل لون الحالة، يُعيد Widget.
typedef IconBuilder = Widget Function(Color iconColor);

/// {@template app_text_button}
/// Abstract base for all text buttons - subclass to define colors.
/// قاعدة مجردة لكل أزرار النص - ورّث منها لتحديد الألوان.
/// {@endtemplate}
abstract base class AppTextButton extends StatelessWidget {
  const AppTextButton({
    super.key,
    required this.label,
    this.onTap,
    this.leading,
    this.trailing,
    this.appButtonSize = AppButtonSize.medium,
  });

  final String         label;
  final VoidCallback?  onTap;
  final IconBuilder?   leading;
  final IconBuilder?   trailing;
  final AppButtonSize  appButtonSize;

  // Subclasses define these / الأبناء يعرّفون هذه
  Color backgroundColor(BuildContext context);
  Color hoverColor(BuildContext context);
  Color focusColor(BuildContext context);
  Color disabledColor(BuildContext context);
  Color textColor(BuildContext context);
  Color disabledTextColor(BuildContext context) =>
      context.buttonTheme.primaryTextDisabled;

  // Border overrides - default to none / افتراضياً بدون حدود
  BorderSide defaultBorder(BuildContext context)   => BorderSide.none;
  BorderSide focusedBorder(BuildContext context)   => BorderSide.none;
  BorderSide hoverBorder(BuildContext context)     => BorderSide.none;
  BorderSide disabledBorder(BuildContext context)  => BorderSide.none;

  @override
  Widget build(BuildContext context) { ... }
}

// Concrete implementations / التطبيقات الملموسة
class PrimaryTextButton extends AppTextButton {
  const PrimaryTextButton({super.key, required super.label, super.onTap, super.appButtonSize});

  @override Color backgroundColor(BuildContext ctx) => ctx.buttonTheme.primaryDefault;
  @override Color hoverColor(BuildContext ctx)      => ctx.buttonTheme.primaryHover;
  @override Color focusColor(BuildContext ctx)      => ctx.buttonTheme.primaryFocused;
  @override Color disabledColor(BuildContext ctx)   => ctx.buttonTheme.primaryDisabled;
  @override Color textColor(BuildContext ctx)       => ctx.buttonTheme.primaryText;
}

class SecondaryTextButton extends AppTextButton { ... }
class OutlineTextButton   extends AppTextButton { ... }
class GhostTextButton     extends AppTextButton { ... }
```

**Button Size Enum:**

```dart
/// Enum for button sizes - maps to fixed heights.
/// Enum لأحجام الأزرار - يُعيّن ارتفاعات ثابتة.
enum AppButtonSize {
  xSmall,  // height: 36 - padding: H:12
  small,   // height: 36 - padding: H:12
  medium,  // height: 40 - padding: H:16
  large,   // height: 44 - padding: H:16
  xlarge,  // height: 48 - padding: H:20
  xxLarge, // height: 56 - padding: H:24
}
```

> [!IMPORTANT]
> Never hardcode colors inside a widget - always delegate to the abstract method which reads from `context.buttonTheme`. This is what makes theming and dark mode trivial.
>
> لا تضع ألواناً صلبة داخل أي widget - فوّض دائماً للـ abstract method التي تقرأ من `context.buttonTheme`. هذا ما يجعل الـ theming والـ dark mode أمراً تافهاً.

---

### 🟡 Step 9: Build a Molecule (SearchField Example)

*الخطوة 9: بناء Molecule (مثال SearchField)*

**SearchField Molecule:**

```dart
/// {@template search_field}
/// A search input molecule - combines [AppTextField] + search [AppIcon].
/// مولكيول حقل البحث - يجمع [AppTextField] مع أيقونة البحث [AppIcon].
/// {@endtemplate}
class SearchField extends StatelessWidget {
  const SearchField({
    super.key,
    this.onChanged,
    this.onSubmit,
    this.hintText = 'Search...',
  });

  final ValueChanged<String>? onChanged;
  final VoidCallback?         onSubmit;
  final String                hintText;

  @override
  Widget build(BuildContext context) {
    return AppTextField(          // Atom / ذرة
      labelText: hintText,
      onChanged: onChanged,
      keyboardType: TextInputType.text,
      onEditingComplete: onSubmit,
      suffixIcon: GestureDetector(  // Atom / ذرة
        onTap: onSubmit,
        child: SvgPicture(loader: AppAssets.searchIcon),
      ),
    );
  }
}
```

> [!NOTE]
> A Molecule has **one responsibility**. If your molecule is doing two unrelated things, it should be an Organism.
>
> المولكيول لها **مسؤولية واحدة**. إذا كانت تفعل شيئين غير مترابطين، فهي Organism.

---

### 🔴 Step 10: Build an Organism (LoginForm Example)

*الخطوة 10: بناء Organism (مثال LoginForm)*

**LoginForm Organism:**

```dart
/// {@template login_form}
/// Login form organism - orchestrates multiple atoms and molecules.
/// كائن نموذج تسجيل الدخول - ينسّق atoms و molecules متعددة.
/// {@endtemplate}
class LoginForm extends StatefulWidget {
  const LoginForm({super.key, required this.onSubmit});

  final void Function(String email, String password) onSubmit;

  @override
  State<LoginForm> createState() => _LoginFormState();
}

class _LoginFormState extends State<LoginForm> {
  final _formKey  = GlobalKey<FormState>();
  final _email    = TextEditingController();
  final _password = TextEditingController();
  bool  _obscure  = true;

  @override
  Widget build(BuildContext context) {
    return Form(
      key: _formKey,
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.stretch,
        children: [
          // Atom / ذرة
          AppTextField(
            controller: _email,
            labelText: 'Email',
            keyboardType: TextInputType.emailAddress,
            validator: (v) => v!.contains('@') ? null : 'Invalid email',
          ),
          const SizedBox(height: AppSpacing.xl),

          // Atom / ذرة
          AppTextField(
            controller: _password,
            labelText: 'Password',
            obscureText: _obscure,
            suffixIcon: IconButton(
              icon: Icon(_obscure ? Icons.visibility : Icons.visibility_off),
              onPressed: () => setState(() => _obscure = !_obscure),
            ),
            validator: (v) => v!.length >= 8 ? null : 'Min 8 characters',
          ),
          const SizedBox(height: AppSpacing.xxl),

          // Atom / ذرة
          PrimaryTextButton(
            label: 'Log In',
            appButtonSize: AppButtonSize.large,
            onTap: () {
              if (_formKey.currentState!.validate()) {
                widget.onSubmit(_email.text, _password.text);
              }
            },
          ),
        ],
      ),
    );
  }

  @override
  void dispose() {
    _email.dispose();
    _password.dispose();
    super.dispose();
  }
}
```

---

### 🟡 Step 11: Differentiate Templates and Pages in Practice

*الخطوة 11: التفريق بين Template و Page في التطبيق الفعلي*

**Template - Layout only, no data:**

```dart
/// {@template auth_template}
/// Auth layout template - provides consistent padding and background.
/// قالب تخطيط المصادقة - يوفر padding وخلفية متسقة.
/// {@endtemplate}
class AuthTemplate extends StatelessWidget {
  const AuthTemplate({super.key, required this.body, this.header});

  final Widget  body;
  final Widget? header;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: context.layoutTheme.authBackground,
      body: SafeArea(
        child: Padding(
          padding: const EdgeInsets.symmetric(
            horizontal: AppSpacing.xxl,
            vertical: AppSpacing.xl,
          ),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: [
              if (header != null) ...[header!, const SizedBox(height: AppSpacing.xxl)],
              Expanded(child: body),
            ],
          ),
        ),
      ),
    );
  }
}
```

**Page - Template + real data + routing:**

```dart
/// {@template login_page}
/// Login page - wires template, organism, and state management.
/// صفحة تسجيل الدخول - تربط القالب والكائن وإدارة الحالة.
/// {@endtemplate}
class LoginPage extends StatelessWidget {
  const LoginPage({super.key});

  @override
  Widget build(BuildContext context) {
    return AuthTemplate(               // Template / قالب
      header: AppAssetImage(           // Atom / ذرة
        path: AppAssets.logoFull,
      ),
      body: LoginForm(                 // Organism / كائن
        onSubmit: (email, password) {
          context.read<AuthCubit>()    // State management
              .login(email, password);
        },
      ),
    );
  }
}
```

> [!TIP]
> Pages are the **only layer** that knows about state management (BLoC, Riverpod, etc.) and routing. Templates and below are completely framework-agnostic.
>
> الـ Pages هي **الطبقة الوحيدة** التي تعرف عن إدارة الحالة والـ routing. كل ما دونها مستقل تماماً عن أي framework.

---

## 4. Theme System / نظام الثيم

### 🔴 Step 12: Build a Component-Level ThemeExtension

*الخطوة 12: بناء ThemeExtension على مستوى المكوّن*

**AppButtonTheme with ThemeExtension:**

```dart
/// {@template app_button_theme}
/// Theming contract for all button variants.
/// عقد الـ theming لكل متغيرات الأزرار.
/// {@endtemplate}
class AppButtonTheme extends ThemeExtension<AppButtonTheme> {
  const AppButtonTheme({
    required this.primaryText,
    required this.primaryDefault,
    required this.primaryHover,
    required this.primaryFocused,
    required this.primaryDisabled,
    required this.primaryTextDisabled,
    required this.secondaryDefault,
    required this.secondaryHover,
    required this.outlinedDefault,
    required this.outlinedBorderDisabled,
    required this.buttonLineDefault,
  });

  /// Light mode factory / مصنع الوضع الفاتح
  factory AppButtonTheme.light() => AppButtonTheme(
    primaryText:          AppColors.white,
    primaryDefault:       AppColors.brand.shade500,
    primaryHover:         AppColors.brand.shade600,
    primaryFocused:       AppColors.brand.shade700,
    primaryDisabled:      AppColors.grayLight.shade200,
    primaryTextDisabled:  AppColors.grayLight.shade300,
    secondaryDefault:     AppColors.grayLight.shade100,
    secondaryHover:       AppColors.grayLight.shade150,
    outlinedDefault:      AppColors.white,
    outlinedBorderDisabled: AppColors.grayLight.shade200,
    buttonLineDefault:    AppColors.grayLight.shade300,
  );

  /// Dark mode factory / مصنع الوضع المظلم
  factory AppButtonTheme.dark() => AppButtonTheme(
    primaryText:          AppColors.white,
    primaryDefault:       AppColors.brand.shade400,
    primaryHover:         AppColors.brand.shade300,
    primaryFocused:       AppColors.brand.shade200,
    primaryDisabled:      AppColors.grayDark.shade700,
    primaryTextDisabled:  AppColors.grayDark.shade500,
    secondaryDefault:     AppColors.grayDark.shade800,
    secondaryHover:       AppColors.grayDark.shade700,
    outlinedDefault:      AppColors.transparent,
    outlinedBorderDisabled: AppColors.grayDark.shade700,
    buttonLineDefault:    AppColors.grayDark.shade500,
  );

  final Color primaryText;
  final Color primaryDefault;
  final Color primaryHover;
  final Color primaryFocused;
  final Color primaryDisabled;
  final Color primaryTextDisabled;
  final Color secondaryDefault;
  final Color secondaryHover;
  final Color outlinedDefault;
  final Color outlinedBorderDisabled;
  final Color buttonLineDefault;

  @override
  AppButtonTheme copyWith({ Color? primaryDefault, ... }) => AppButtonTheme(
    primaryDefault: primaryDefault ?? this.primaryDefault,
    // ...
  );

  @override
  AppButtonTheme lerp(covariant AppButtonTheme? other, double t) {
    if (other is! AppButtonTheme) return this;
    return AppButtonTheme(
      primaryDefault: Color.lerp(primaryDefault, other.primaryDefault, t)!,
      // lerp all fields / حوّل كل الحقول
    );
  }
}
```

---

### 🔴 Step 13: Aggregate All Themes into a Single AppTheme

*الخطوة 13: تجميع كل الـ themes في AppTheme واحد*

**AppTheme Aggregator:**

```dart
/// {@template app_theme}
/// Single entry point for all design system themes.
/// نقطة دخول واحدة لكل themes نظام التصميم.
/// {@endtemplate}
class AppTheme extends ThemeExtension<AppTheme> {
  const AppTheme({
    required this.appButtonTheme,
    required this.appInputTheme,
    required this.appTypography,
    required this.appCheckboxTheme,
    required this.appToggleTheme,
    required this.appBadgeTheme,
    required this.appAvatarTheme,
    required this.appNavigationTheme,
    required this.appLayoutTheme,
  });

  factory AppTheme.light() => AppTheme(
    appButtonTheme:     AppButtonTheme.light(),
    appInputTheme:      AppInputTheme.light(),
    appTypography:      AppRegularTypography(),
    appCheckboxTheme:   AppCheckboxTheme.light(),
    appToggleTheme:     AppToggleTheme.light(),
    appBadgeTheme:      AppBadgeTheme.light(),
    appAvatarTheme:     AppAvatarTheme.light(),
    appNavigationTheme: AppNavigationTheme.light(),
    appLayoutTheme:     AppLayoutTheme.light(),
  );

  factory AppTheme.dark() => AppTheme(
    appButtonTheme:     AppButtonTheme.dark(),
    appInputTheme:      AppInputTheme.dark(),
    appTypography:      AppRegularTypography(),
    // ...
  );

  final ThemeExtension<AppButtonTheme>     appButtonTheme;
  final ThemeExtension<AppInputTheme>      appInputTheme;
  final AppTypography                      appTypography;
  // ...

  @override AppTheme copyWith({ ... }) => ...;
  @override AppTheme lerp(covariant AppTheme? other, double t) => ...;
}
```

---

### 🟡 Step 14: Expose the Theme via BuildContext Extensions

*الخطوة 14: عرض الـ theme عبر extensions على BuildContext*

**BuildContext Theme Extensions:**

```dart
/// Extensions on [BuildContext] - clean theme access everywhere.
/// Extensions على [BuildContext] - وصول نظيف للـ theme في كل مكان.
extension ThemeExt on BuildContext {
  ThemeData      get theme          => Theme.of(this);
  AppTheme       get _appTheme      => theme.extension<AppTheme>()!;

  AppButtonTheme     get buttonTheme     => _appTheme.appButtonTheme     as AppButtonTheme;
  AppInputTheme      get inputTheme      => _appTheme.appInputTheme      as AppInputTheme;
  AppTypography      get typography      => _appTheme.appTypography      as AppTypography;
  AppCheckboxTheme   get checkboxTheme   => _appTheme.appCheckboxTheme   as AppCheckboxTheme;
  AppToggleTheme     get toggleTheme     => _appTheme.appToggleTheme     as AppToggleTheme;
  AppBadgeTheme      get badgeTheme      => _appTheme.appBadgeTheme      as AppBadgeTheme;
  AppAvatarTheme     get avatarTheme     => _appTheme.appAvatarTheme     as AppAvatarTheme;
  AppNavigationTheme get navigationTheme => _appTheme.appNavigationTheme as AppNavigationTheme;
  AppLayoutTheme     get layoutTheme     => _appTheme.appLayoutTheme     as AppLayoutTheme;
}

// Usage / الاستخدام:
context.buttonTheme.primaryDefault
context.typography.titleSmall
context.inputTheme.borderFocused
context.badgeTheme.successBackground
```

---

### 🔴 Step 15: Provide and Switch Themes using ThemeScope

*الخطوة 15: توفير الثيم وتبديله باستخدام ThemeScope*

**ThemeScope InheritedWidget:**

```dart
/// {@template theme_scope}
/// InheritedWidget - provides [AppTheme] to the entire widget tree.
/// InheritedWidget - يُوفّر [AppTheme] لكل شجرة الـ widgets.
/// {@endtemplate}
class ThemeScope extends InheritedWidget {
  const ThemeScope({
    super.key,
    required super.child,
    required this.themeMode,
    required this.appTheme,
  });

  final ThemeMode themeMode;
  final AppTheme  appTheme;

  static ThemeScope of(BuildContext context) {
    final result = context.dependOnInheritedWidgetOfExactType<ThemeScope>();
    assert(result != null, 'ThemeScope not found - wrap your app with ThemeScopeWidget');
    return result!;
  }

  @override
  bool updateShouldNotify(ThemeScope old) =>
      old.themeMode != themeMode || old.appTheme != appTheme;
}
```

**ThemeScopeWidget with persistence:**

```dart
const _kThemeMode = 'themeMode';

class ThemeScopeWidget extends StatefulWidget {
  const ThemeScopeWidget({super.key, required this.child, required this.preferences});

  final Widget            child;
  final SharedPreferences preferences;

  /// One-liner initializer for main() / مُهيّئ سطر واحد لـ main()
  static Future<ThemeScopeWidget> initialize(Widget child) async {
    final prefs = await SharedPreferences.getInstance();
    return ThemeScopeWidget(preferences: prefs, child: child);
  }

  static ThemeScopeWidgetState? of(BuildContext context) =>
      context.findRootAncestorStateOfType<ThemeScopeWidgetState>();

  @override
  State<ThemeScopeWidget> createState() => ThemeScopeWidgetState();
}

class ThemeScopeWidgetState extends State<ThemeScopeWidget> {
  ThemeMode _themeMode = ThemeMode.system;

  /// Toggle theme from anywhere / بدّل الثيم من أي مكان
  Future<void> changeTo(ThemeMode mode) async {
    if (_themeMode == mode) return;
    await widget.preferences.setInt(_kThemeMode, ThemeMode.values.indexOf(mode));
    setState(() => _themeMode = mode);
  }

  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    final idx = widget.preferences.getInt(_kThemeMode) ?? 0;
    _themeMode = ThemeMode.values[idx];
  }

  @override
  Widget build(BuildContext context) {
    final brightness = MediaQuery.platformBrightnessOf(context);
    final appTheme = switch (_themeMode) {
      ThemeMode.light  => AppTheme.light(),
      ThemeMode.dark   => AppTheme.dark(),
      ThemeMode.system => brightness == Brightness.dark
          ? AppTheme.dark()
          : AppTheme.light(),
    };

    return ThemeScope(
      themeMode: _themeMode,
      appTheme:  appTheme,
      child: widget.child,
    );
  }
}
```

**main.dart setup / إعداد main.dart:**

```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  final app = await ThemeScopeWidget.initialize(const MyApp());
  runApp(app);
}

// In MaterialApp / في MaterialApp:
final scope = ThemeScope.of(context);
return MaterialApp(
  themeMode: scope.themeMode,
  theme:     ThemeData(extensions: [scope.appTheme]),
  darkTheme: ThemeData(extensions: [scope.appTheme]),
);

// Change theme from any widget / غيّر الثيم من أي widget:
ThemeScopeWidget.of(context)?.changeTo(ThemeMode.dark);
```

> [!IMPORTANT]
> The `lerp` method in `ThemeExtension` is what enables smooth animated transitions between light and dark mode - never skip it.
>
> دالة `lerp` في `ThemeExtension` هي ما يُتيح الانتقال المتحرك السلس بين الوضع الفاتح والمظلم - لا تتخطاها أبداً.

---

## 5. Typography / الطباعة

### 🟡 Step 16: Define a Scalable AppTypography System

*الخطوة 16: تعريف نظام AppTypography قابل للتوسع*

**AppTypography as ThemeExtension:**

```dart
/// {@template app_typography}
/// Typography contract - defines all TextStyles as named properties.
/// عقد الطباعة - يُعرّف كل TextStyles كخصائص مسماة.
/// {@endtemplate}
interface class AppTypography extends ThemeExtension<AppTypography> {
  AppTypography({
    // Display / عرض
    required this.display2XLarge,
    required this.displayXLarge,
    required this.displayLarge,
    // Title / عناوين
    required this.titleLarge,
    required this.titleMedium,
    required this.titleSmall,
    // Body / نص أساسي
    required this.bodyLarge,
    required this.bodyMedium,
    required this.bodySmall,
    // Label / تسميات
    required this.labelLarge,
    required this.labelMedium,
    required this.labelSmall,
    // Button / أزرار
    required this.button2XLarge,
    required this.buttonXLarge,
    required this.buttonLarge,
    required this.buttonMedium,
    required this.buttonSmall,
    // Input / مدخلات
    required this.inputLabel,
    required this.inputPlaceHolder,
    required this.inputHint,
  });

  final TextStyle display2XLarge;
  final TextStyle displayXLarge;
  final TextStyle displayLarge;
  final TextStyle titleLarge;
  final TextStyle titleMedium;
  final TextStyle titleSmall;
  final TextStyle bodyLarge;
  final TextStyle bodyMedium;
  final TextStyle bodySmall;
  final TextStyle labelLarge;
  final TextStyle labelMedium;
  final TextStyle labelSmall;
  final TextStyle button2XLarge;
  final TextStyle buttonXLarge;
  final TextStyle buttonLarge;
  final TextStyle buttonMedium;
  final TextStyle buttonSmall;
  final TextStyle inputLabel;
  final TextStyle inputPlaceHolder;
  final TextStyle inputHint;

  @override AppTypography copyWith({ ... }) => ...;
  @override AppTypography lerp(covariant AppTypography? other, double t) => ...;
}

/// Concrete regular typography implementation.
/// التطبيق الملموس لطباعة النص العادي.
class AppRegularTypography extends AppTypography {
  AppRegularTypography({
    super.titleLarge = const TextStyle(
      fontSize: 20, height: 30 / 20, fontWeight: FontWeight.w600,
    ),
    super.titleMedium = const TextStyle(
      fontSize: 18, height: 28 / 18, fontWeight: FontWeight.w600,
    ),
    super.titleSmall = const TextStyle(
      fontSize: 16, height: 24 / 16, fontWeight: FontWeight.w600,
    ),
    super.bodyLarge = const TextStyle(
      fontSize: 16, height: 24 / 16, fontWeight: FontWeight.w400,
    ),
    super.bodyMedium = const TextStyle(
      fontSize: 14, height: 20 / 14, fontWeight: FontWeight.w400,
    ),
    super.buttonLarge = const TextStyle(
      fontSize: 16, height: 24 / 16, fontWeight: FontWeight.w500,
    ),
    super.buttonMedium = const TextStyle(
      fontSize: 14, height: 20 / 14, fontWeight: FontWeight.w500,
    ),
    // ... all other styles
  });
}
```

> [!TIP]
> Set `height` as `lineHeight / fontSize` (e.g. `24 / 16 = 1.5`) - this matches Figma's line height exactly and avoids clipping descenders on dense layouts.
>
> اضبط `height` كـ `lineHeight / fontSize` (مثل `24 / 16 = 1.5`) - يتطابق مع line height في Figma تماماً ويمنع قطع الأحرف السفلية في التخطيطات المكتظة.

---

## 6. Components Deep Dive / تعمق في المكونات

### 🔴 Step 17: Implement AppTextField with Full State-Driven Styling

*الخطوة 17: تنفيذ AppTextField بتصميم مدفوع بالحالة بالكامل*

**AppTextField with WidgetStateTextStyle:**

```dart
/// {@template app_text_field}
/// A fully theme-driven text field - all colors from [AppInputTheme].
/// حقل نص مدفوع بالثيم كلياً - كل الألوان من [AppInputTheme].
/// {@endtemplate}
class AppTextField extends StatelessWidget {
  const AppTextField({
    super.key,
    this.controller,
    this.labelText,
    this.helperText,
    this.errorText,
    this.enabled      = true,
    this.obscureText  = false,
    this.maxLines     = 1,
    this.onChanged,
    this.validator,
    this.suffixIcon,
    this.prefixIcon,
    this.suffixIconConstraints = const BoxConstraints(minHeight: 24, minWidth: 40),
    this.prefixIconConstraints = const BoxConstraints(minHeight: 24, minWidth: 40),
    this.keyboardType,
    this.inputFormatters,
    this.autofillHints,
    this.onEditingComplete,
    this.autovalidateMode = AutovalidateMode.onUserInteraction,
  });

  final TextEditingController?   controller;
  final String?                  labelText;
  final String?                  helperText;
  final String?                  errorText;
  final bool                     enabled;
  final bool                     obscureText;
  final int                      maxLines;
  final ValueChanged<String>?    onChanged;
  final FormFieldValidator<String>? validator;
  final Widget?                  suffixIcon;
  final Widget?                  prefixIcon;
  final BoxConstraints?          suffixIconConstraints;
  final BoxConstraints?          prefixIconConstraints;
  final TextInputType?           keyboardType;
  final List<TextInputFormatter>? inputFormatters;
  final Iterable<String>?        autofillHints;
  final VoidCallback?            onEditingComplete;
  final AutovalidateMode         autovalidateMode;

  @override
  Widget build(BuildContext context) {
    return TextFormField(
      controller:        controller,
      enabled:           enabled,
      obscureText:       obscureText,
      maxLines:          maxLines,
      onChanged:         onChanged,
      validator:         validator,
      keyboardType:      keyboardType,
      inputFormatters:   inputFormatters,
      autofillHints:     autofillHints,
      onEditingComplete: onEditingComplete,
      autovalidateMode:  autovalidateMode,
      cursorColor:       context.inputTheme.focusedTextDefault,
      cursorHeight:      16,

      // Text style changes with state / نمط النص يتغير مع الحالة
      style: WidgetStateTextStyle.resolveWith((states) {
        final color = states.contains(WidgetState.disabled)
            ? context.inputTheme.disabledText
            : context.inputTheme.defaultText;
        return context.typography.inputPlaceHolder.copyWith(color: color);
      }),

      decoration: InputDecoration(
        labelText:  labelText,
        helperText: helperText,
        errorText:  errorText,
        filled:     true,
        fillColor:  enabled
            ? context.inputTheme.defaultColor
            : context.inputTheme.disabledColor,
        hoverColor: Colors.transparent,
        focusColor: Colors.transparent,

        // Label style / نمط التسمية
        labelStyle: WidgetStateTextStyle.resolveWith((states) {
          Color color;
          if (states.contains(WidgetState.error))    color = context.inputTheme.errorTextDefault;
          else if (states.contains(WidgetState.focused)) color = context.inputTheme.focusedOnBrand;
          else if (states.contains(WidgetState.disabled)) color = context.inputTheme.disabledText;
          else color = context.inputTheme.defaultText;
          return context.typography.inputPlaceHolder.copyWith(color: color);
        }),

        // Border changes with state / الحدود تتغير مع الحالة
        border: WidgetStateOutlineInputBorder.resolveWith((states) {
          Color borderColor;
          if (states.contains(WidgetState.error))      borderColor = context.inputTheme.borderError;
          else if (states.contains(WidgetState.focused)) borderColor = context.inputTheme.borderFocused;
          else if (states.contains(WidgetState.disabled)) borderColor = context.inputTheme.borderDisabled;
          else if (states.contains(WidgetState.hovered))  borderColor = context.inputTheme.borderHover;
          else borderColor = context.inputTheme.borderDefault;

          return OutlineInputBorder(
            borderRadius: const BorderRadius.all(AppRadius.md),
            borderSide: BorderSide(color: borderColor),
          );
        }),

        suffixIcon: suffixIcon,
        prefixIcon: prefixIcon,
        suffixIconConstraints: suffixIconConstraints,
        prefixIconConstraints: prefixIconConstraints,

        errorStyle: context.typography.inputHint.copyWith(
          color: context.inputTheme.errorTextDefault,
        ),
      ),
    );
  }
}
```

---

## 7. Assets Management / إدارة الأصول

### 🟡 Step 18: Structure Assets as a Separate Package with SSOT

*الخطوة 18: هيكلة الـ assets كباكدج منفصل مع مصدر حقيقة واحد*

**Assets Package Structure:**

```
assets/                    # Separate Flutter package / باكدج Flutter منفصل
├── lib/
│   └── app_assets.dart    # SSOT - Single Source of Truth
├── fonts/
│   └── inter/             # Export fonts via lib/ folder
├── vectors/               # SVGs - compiled at build time
│   ├── icons/
│   │   ├── search.svg
│   │   └── person.svg
│   └── illustrations/
│       └── empty_state.svg
└── rasters/               # PNGs, JPEGs, WebPs
    ├── logo_full.png
    └── placeholder.webp
```

**AppAssets SSOT class:**

```dart
/// {@template app_assets}
/// Single Source of Truth for all app assets.
/// المصدر الوحيد للحقيقة لكل أصول التطبيق.
/// {@endtemplate}
abstract class AppAssets {
  // SVG Vectors - compiled via flutter_svg / مُجمَّعة بـ flutter_svg
  static const searchIcon = AssetBytesLoader(
    'vectors/icons/search.svg', packageName: 'assets',
  );
  static const personIcon = AssetBytesLoader(
    'vectors/icons/person.svg', packageName: 'assets',
  );
  static const emptyStateIllustration = AssetBytesLoader(
    'vectors/illustrations/empty_state.svg', packageName: 'assets',
  );

  // Rasters / صور نقطية
  static const logoFull    = 'rasters/logo_full.png';
  static const placeholder = 'rasters/placeholder.webp';
}

// Usage / الاستخدام:
SvgPicture(loader: AppAssets.searchIcon)
Image.asset(AppAssets.logoFull, package: 'assets')
```

> [!IMPORTANT]
> Always pass `packageName: 'assets'` to `AssetBytesLoader` and `package: 'assets'` to `Image.asset` when loading assets from a separate package - Flutter won't find them without it.
>
> مرّر دائماً `packageName: 'assets'` لـ `AssetBytesLoader` و `package: 'assets'` لـ `Image.asset` عند تحميل assets من باكدج منفصل - Flutter لن يجدها بدونه.

---

## 8. Project Structure / هيكل المشروع

### 🔴 Step 19: Adopt the Recommended Project Structure for Production

*الخطوة 19: تبني هيكل المشروع الموصى به في الإنتاج*

**Production-Ready Structure:**

```
my_design_system/               # Standalone Flutter package
│
├── lib/
│   ├── src/
│   │   │
│   │   ├── tokens/             # Layer 0: Raw values / القيم الخام
│   │   │   ├── app_colors.dart
│   │   │   ├── app_spacing.dart
│   │   │   ├── app_radius.dart
│   │   │   └── app_shadow.dart
│   │   │
│   │   ├── foundations/        # Layer 1: Themes + Typography
│   │   │   ├── app_typography.dart
│   │   │   ├── app_button_theme.dart
│   │   │   ├── app_input_theme.dart
│   │   │   ├── app_checkbox_theme.dart
│   │   │   ├── app_toggle_theme.dart
│   │   │   ├── app_badge_theme.dart
│   │   │   ├── app_avatar_theme.dart
│   │   │   ├── app_navigation_theme.dart
│   │   │   ├── app_layout_theme.dart
│   │   │   └── app_theme.dart      # Aggregator / المجمّع
│   │   │
│   │   ├── atoms/              # Layer 2: Indivisible widgets
│   │   │   ├── buttons/
│   │   │   │   ├── app_text_button.dart    # Abstract base
│   │   │   │   ├── primary_text_button.dart
│   │   │   │   ├── secondary_text_button.dart
│   │   │   │   ├── outline_text_button.dart
│   │   │   │   └── ghost_text_button.dart
│   │   │   ├── app_text_field.dart
│   │   │   ├── app_icon.dart
│   │   │   ├── app_avatar.dart
│   │   │   ├── app_badge.dart
│   │   │   ├── app_toggle.dart
│   │   │   ├── app_checkbox.dart
│   │   │   └── app_radio.dart
│   │   │
│   │   ├── molecules/          # Layer 3: Atomic combinations
│   │   │   ├── search_field.dart
│   │   │   ├── user_card.dart
│   │   │   ├── form_row.dart
│   │   │   └── nav_item.dart
│   │   │
│   │   ├── organisms/          # Layer 4: Complex sections
│   │   │   ├── login_form.dart
│   │   │   ├── app_header.dart
│   │   │   ├── bottom_nav_bar.dart
│   │   │   └── product_list.dart
│   │   │
│   │   ├── templates/          # Layer 5: Layout skeletons
│   │   │   ├── auth_template.dart
│   │   │   ├── main_template.dart
│   │   │   └── dashboard_template.dart
│   │   │
│   │   ├── scope/              # Theme provisioning
│   │   │   ├── theme_scope.dart          # InheritedWidget
│   │   │   └── theme_scope_widget.dart   # StatefulWidget + persistence
│   │   │
│   │   └── extensions/         # BuildContext sugar
│   │       └── theme_ext.dart
│   │
│   └── my_design_system.dart   # Public API - exports everything
│
├── test/
│   ├── atoms/
│   ├── molecules/
│   └── organisms/
│
assets/                         # Separate assets package
├── lib/app_assets.dart
├── fonts/
├── vectors/
└── rasters/
```

**Public API barrel file:**

```dart
// my_design_system.dart - export everything consumers need
library my_design_system;

// Tokens
export 'src/tokens/app_colors.dart';
export 'src/tokens/app_spacing.dart';
export 'src/tokens/app_radius.dart';
export 'src/tokens/app_shadow.dart';

// Foundations
export 'src/foundations/app_typography.dart';
export 'src/foundations/app_theme.dart';
export 'src/foundations/app_button_theme.dart';
// ... all foundations

// Atoms
export 'src/atoms/buttons/primary_text_button.dart';
export 'src/atoms/app_text_field.dart';
// ... all atoms

// Molecules + Organisms + Templates
// ...

// Scope
export 'src/scope/theme_scope.dart';
export 'src/scope/theme_scope_widget.dart';
export 'src/extensions/theme_ext.dart';
```

---

## 9. Testing & Widgetbook / الاختبار والكتالوج

### 🟡 Step 20: Test Design System Components

*الخطوة 20: اختبار مكونات الـ Design System*

**Testing Strategy:**

```dart
// Widget test for an Atom / اختبار widget لذرّة
void main() {
  group('PrimaryTextButton', () {
    testWidgets('renders label correctly', (tester) async {
      await tester.pumpWidget(
        MaterialApp(
          theme: ThemeData(extensions: [AppTheme.light()]),
          home: Scaffold(
            body: PrimaryTextButton(
              label: 'Test Button',
              onTap: () {},
            ),
          ),
        ),
      );

      expect(find.text('Test Button'), findsOneWidget);
    });

    testWidgets('shows disabled state when onTap is null', (tester) async {
      await tester.pumpWidget(
        MaterialApp(
          theme: ThemeData(extensions: [AppTheme.light()]),
          home: const Scaffold(
            body: PrimaryTextButton(label: 'Disabled'),
          ),
        ),
      );

      final button = tester.widget<ElevatedButton>(find.byType(ElevatedButton));
      expect(button.onPressed, isNull);
    });
  });
}
```

---

### 🟡 Step 21: Use Widgetbook as a Component Catalog

*الخطوة 21: استخدام Widgetbook كتالوج للمكونات*

**Widgetbook Setup:**

```dart
// widgetbook/main.dart
@App()
class WidgetbookApp extends StatelessWidget {
  const WidgetbookApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Widgetbook.material(
      addons: [
        MaterialThemeAddon(
          themes: [
            WidgetbookTheme(name: 'Light', data: ThemeData(extensions: [AppTheme.light()])),
            WidgetbookTheme(name: 'Dark',  data: ThemeData(extensions: [AppTheme.dark()])),
          ],
        ),
        DeviceFrameAddon(devices: [Devices.ios.iPhone13, Devices.android.samsungGalaxyS20]),
        TextScaleAddon(),
      ],
      directories: [
        WidgetbookCategory(
          name: 'Atoms',
          children: [
            WidgetbookComponent(
              name: 'PrimaryTextButton',
              useCases: [
                WidgetbookUseCase(
                  name: 'Default',
                  builder: (context) => PrimaryTextButton(
                    label: context.knobs.string(label: 'Label', initialValue: 'Click me'),
                    onTap: () {},
                    appButtonSize: context.knobs.list(
                      label: 'Size',
                      options: AppButtonSize.values,
                    ),
                  ),
                ),
                WidgetbookUseCase(
                  name: 'Disabled',
                  builder: (context) => const PrimaryTextButton(label: 'Disabled'),
                ),
              ],
            ),
          ],
        ),
      ],
    );
  }
}
```

> [!TIP]
> Run Widgetbook as a separate Flutter app (not inside your main app) - `flutter run -d chrome -t widgetbook/main.dart`. This gives you a live component catalog in the browser.
>
> شغّل Widgetbook كتطبيق Flutter منفصل - `flutter run -d chrome -t widgetbook/main.dart`. هذا يعطيك كتالوجاً حياً للمكونات في المتصفح.

---

## 10. Best Practices & Anti-Patterns / أفضل الممارسات والأخطاء الشائعة

### 🟡 Step 22: Avoid Common Design System Mistakes in Flutter

*الخطوة 22: تجنب الأخطاء الشائعة للـ Design System في Flutter*

**❌ Anti-Patterns / الأنماط السلبية:**

| Anti-Pattern / الخطأ | Problem / المشكلة | Fix / الحل |
|---|---|---|
| Hardcoded `Color(0xFF347AF6)` in widget | Can't theme or swap colors | Use `context.buttonTheme.primaryDefault` |
| Named token `buttonColor` | Couples token to component | Use `brand.500` - semantic naming |
| `StatefulWidget` for every atom | Unnecessary overhead | Use `StatelessWidget` when no internal state |
| Huge organism doing 5 things | Untestable, unmaintainable | Split into smaller organisms |
| No barrel file exports | Messy consumer imports | One `design_system.dart` that exports all |
| Copy-pasting component styles | Drift over time | Abstract base class pattern |
| Assets in main app package | No SSOT, hard to share | Dedicated `assets` package |

**✅ Best Practices / أفضل الممارسات:**

```
✅ Tokens have no component names
✅ Every atom is const-constructible
✅ Themes use ThemeExtension + lerp
✅ BuildContext has extension methods
✅ One barrel file as public API
✅ Assets in a separate dedicated package
✅ Widgetbook for visual regression testing
✅ Abstract base for component families (buttons)
✅ Dark mode factory for every ThemeExtension
✅ Pages are the only layer that knows about state management
```

---

### 🔴 Step 23: Version and Maintain the Design System as a Shared Package

*الخطوة 23: إصدار والحفاظ على الـ Design System كباكدج مشترك*

**Versioning Strategy:**

* Use semantic versioning: `MAJOR.MINOR.PATCH`.
* **MAJOR** - breaking API changes (rename token, remove component).
* **MINOR** - new components or tokens added (backward compatible).
* **PATCH** - bug fixes, style tweaks (fully backward compatible).
* Use `melos` for monorepo management when design system and apps share one repo.
* Publish to a private pub server (e.g. `pub.dev` private or self-hosted) for cross-team sharing.

**استراتيجية الإصدار:**

* استخدم semantic versioning: `MAJOR.MINOR.PATCH`.
* **MAJOR** - تغييرات كسر متوافقة (إعادة تسمية token، حذف مكوّن).
* **MINOR** - إضافة مكونات أو tokens جديدة (متوافقة للخلف).
* **PATCH** - إصلاح أخطاء، تعديلات نمط (متوافقة كلياً).
* استخدم `melos` لإدارة الـ monorepo عندما يتشارك الـ design system والتطبيقات مستودعاً واحداً.
* انشر على pub server خاص لمشاركة عبر الفرق.

---

### 🟢 Quick Reference - Full Hierarchy Cheat Sheet

*مرجع سريع - ورقة غش الهرمية الكاملة*

```
Tokens        → AppColors, AppSpacing, AppRadius, AppShadow
  ↓
Foundations   → AppTypography, AppButtonTheme, AppInputTheme → AppTheme
  ↓
Atoms         → PrimaryButton, AppTextField, AppIcon, AppAvatar
  ↓
Molecules     → SearchField, UserCard, FormRow, NavItem
  ↓
Organisms     → LoginForm, AppHeader, BottomNavBar, ProductList
  ↓
Templates     → AuthTemplate, MainTemplate, DashboardTemplate
  ↓
Pages         → LoginPage, HomeScreen, ProfilePage
```

```
Consumers use:
  context.buttonTheme.primaryDefault   ← Button color
  context.typography.titleSmall        ← Text style
  context.inputTheme.borderFocused     ← Input border
  AppSpacing.xl                        ← 16.0
  AppRadius.md                         ← Radius.circular(8)
  AppColors.brand.shade500             ← Primary brand color
  AppShadow.sm                         ← List<BoxShadow>
  AppAssets.searchIcon                 ← SVG loader
```

---

*تم إعداد هذا الدليل كمرجع شامل لبناء **Design Systems** احترافية في Flutter*\
*Prepared as a complete reference for building professional **Design Systems** in Flutter*

---

## ⭐ Support This Guide / ادعم هذا المرجع

If this guide helped you build a better Flutter Design System, consider giving it a **star** ⭐ - it takes 2 seconds and helps others find it!

إذا ساعدك هذا الدليل في بناء Design System أفضل في Flutter، امنحه **Star** ⭐ - لن يأخذ منك سوى ثانيتين وسيساعد الآخرين في إيجاده!

> **Share it** with your Flutter team - a shared reference means fewer architecture debates.
>
> **شاركه** مع فريق Flutter الخاص بك - مرجع مشترك يعني نقاشات معمارية أقل.
