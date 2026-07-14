<div dir="rtl" align="right">
[English Version Below ⬇️](#english-version)
</div>

<div dir="rtl" align="right">

<div align="center">
  <!-- [أدخل صورة البانر المتحرك أو الشعار هنا] -->
  <img src="assets/banner.png" alt="شعار مكتبة الأبحاث الحديثية الذكية" width="100%">

  # 🕌 مكتبة الأبحاث الحديثية الذكية (SaaS)
  
  **منصة أكاديمية سحابية متقدمة، تجمع بين المعرفة الشرعية العميقة والهندسة البرمجية المتطورة (Clean Architecture).**

  <!-- التقنيات المستخدمة -->
  <p>
    <img src="https://img.shields.io/badge/Frontend-Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white" alt="Flutter">
    <img src="https://img.shields.io/badge/State_Management-Riverpod-042B59?style=for-the-badge&logo=flutter&logoColor=white" alt="Riverpod">
    <img src="https://img.shields.io/badge/Backend-FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI">
    <img src="https://img.shields.io/badge/Database-SQLite_(Drift)-003B57?style=for-the-badge&logo=sqlite&logoColor=white" alt="SQLite Drift">
    <img src="https://img.shields.io/badge/Cloud-Cloudflare_Workers-F38020?style=for-the-badge&logo=cloudflare&logoColor=white" alt="Cloudflare">
  </p>

  [تجربة النسخة الحية](https://hadithresearchlibrary.pages.dev/)
</div>

---

## 📖 عن المشروع

**مكتبة الأبحاث الحديثية الذكية** هي منصة سحابية متكاملة (SaaS) صُممت بعناية فائقة لتخدم الباحثين الشرعيين، الأكاديميين، والمؤسسات العلمية، وتهدف إلى توفير بيئة بحث متقدمة تدمج بين دقة البحث النصي والمزامنة اللحظية مع المصورات الأصلية (PDF).

عادةً ما يتطلب البحث الحديثي التنقل بين آلاف المخطوطات والكتب المطبوعة، وهي عملية تستغرق وقتاً طويلاً وعرضة للخطأ. يحل هذا المشروع هذه المشكلة الجذرية من خلال رقمنة وهيكلة كميات ضخمة من الأبحاث الحديثية.

يعتمد المشروع على المعمارية النظيفة (Clean Architecture) لضمان قابلية التوسع والصيانة، مع فصل واضح بين واجهات المستخدم، وإدارة الحالة، والاتصال بقواعد البيانات (Local/Cloud).

## ✨ المميزات الرئيسية

*   🚀 **بحث نصي متقدم وفائق السرعة:** محرك بحث محلي وسحابي مصمم للتعامل مع النصوص العربية والوثائق الحديثية بدقة وسرعة.
    *   *![واجهة البحث](assets/search_interface.png)*
*   🔄 **مزامنة لحظية للمخطوطات (pdfrx):** إمكانية الانتقال المباشر من النص المكتوب إلى الصفحة المطابقة في ملف PDF الأصلي، لتوثيق المعلومات فورياً.
    *   *![مزامنة المخطوطات](assets/sync_feature.gif)*
*   📶 **دعم العمل دون اتصال (Offline Support):** بفضل التخزين المحلي الفعال عبر (Drift/SQLite)، يمكن للمستخدم الوصول إلى أجزاء واسعة من المكتبة وإجراء عمليات البحث دون الحاجة الدائمة للإنترنت.
*   📱 **تصميم متجاوب ومتعدد المنصات:** تجربة مستخدم موحدة وسلسة عبر الويب، سطح المكتب، والهواتف المحمولة، اعتماداً على قوة إطار عمل Flutter.
    *   *![واجهات الموبايل والويب](assets/mockups.png)*

## 🏗️ الهيكلية البرمجية (Technical Architecture)

يعتمد المشروع على **المعمارية النظيفة (Clean Architecture)** لضمان أقصى درجات المرونة، وقابلية التوسع والصيانة، مع تطبيق مبادئ (SOLID) واستخدام أنماط التصميم مثل (Repository Pattern). يوضح المخطط التالي دورة تدفق البيانات وتفاعل المكونات:

<div align="center">

```mermaid
graph TD
    direction TB
    
    %% Presentation Layer
    subgraph Presentation["📱 طبقة العرض (Flutter Web Client)"]
        direction TB
        UI["واجهة المستخدم (UI Components)"]
        State["إدارة الحالة (Riverpod / Providers)"]
        UI <--> State
    end

    %% Domain Layer
    subgraph Domain["🧠 طبقة النطاق (Business Logic)"]
        direction TB
        UseCases["محركات البحث والتزامن (Search & Sync Engines)"]
        Entities["الكيانات الأساسية (Core Entities)"]
        UseCases --> Entities
    end

    %% Data & Infrastructure Layer
    subgraph Data["☁️ طبقة البيانات والبنية التحتية (Data & Cloud)"]
        direction TB
        Repos["مستودعات البيانات (Repositories)"]
        LocalDB["قاعدة بيانات محلية (SQLite / Drift)"]
        CF_API["خوادم سحابية (Cloudflare Workers API)"]
        CF_R2["مخزن السحابة للملفات (Cloudflare R2 Bucket)"]
        
        Repos <--> LocalDB
        Repos <--> CF_API
        CF_API <--> CF_R2
    end

    %% Connections between layers
    State <-->|تحديث الحالة| UseCases
    UseCases <-->|طلب بيانات| Repos

    %% Styling
    classDef pres fill:#E3F2FD,stroke:#2196F3,stroke-width:2px,color:#0D47A1;
    classDef dom fill:#F3E5F5,stroke:#9C27B0,stroke-width:2px,color:#4A148C;
    classDef dat fill:#E8F5E9,stroke:#4CAF50,stroke-width:2px,color:#1B5E20;
    
    class UI,State pres;
    class Entities,UseCases dom;
    class Repos,LocalDB,CF_API,CF_R2 dat;
```

</div>

### التقنيات المستخدمة بتفصيل:
*   **تطوير واجهات المستخدم (Flutter & Dart):** لبناء واجهات مستخدم سلسة وعالية الأداء تعمل على مختلف أنظمة التشغيل من كود برمجي واحد.
*   **إدارة الحالة (Riverpod):** لإدارة حالة التطبيق بشكل تفاعلي وآمن.
*   **قواعد البيانات (Drift / SQLite):** لبناء قاعدة بيانات محلية قوية تدعم التخزين المؤقت والبحث السريع (Offline-first).
*   **الخوادم السحابية:** تم استخدام **Python & FastAPI** و **Cloudflare Workers API** لمعالجة البيانات الكثيفة وسرعة الاستجابة، بالإضافة إلى **Cloudflare R2 Bucket** لتخزين الملفات السحابية كبديل لـ AWS S3.
*   **التعامل مع المستندات:** مكتبة **pdfrx** لعرض ومعالجة ملفات PDF بمزامنة دقيقة.

## 🔒 ملاحظة حول الكود المصدري (مستودع عرض فقط)

> **ملاحظة لمدراء التوظيف والمدراء التقنيين (CTOs):**
> هذا المستودع مخصص كـ **واجهة عرض (Showcase)** لتوضيح المعمارية التقنية، تصميم واجهات المستخدم (UI/UX)، والمميزات البرمجية للمشروع.
> 
> نظراً لحقوق الملكية الفكرية (IP) والتراخيص التجارية، فإن الكود المصدري الفعلي محفوظ في **مستودع مغلق (Private)**. يسعدني جداً مناقشة تفاصيل التنفيذ البرمجي، تصميم النظام، وأفضل الممارسات المتبعة في كتابة الكود خلال المقابلات التقنية.
> 
> 🔗 **[اضغط هنا لتجربة النسخة الحية](https://hadithresearchlibrary.pages.dev/)**

## 📫 التواصل

أرحب دائماً بمناقشة الفرص الوظيفية التقنية، التعاون الأكاديمي، أو الفرص الاستثمارية.

*   💼 **لينكد إن:** [أدخل رابط حساب لينكد إن هنا]
*   📧 **البريد الإلكتروني:** [أدخل البريد الإلكتروني هنا]

</div>

---
<br>

<h1 id="english-version" align="left">English Version</h1>

<div align="left">

<div align="center">
  <!-- [Placeholder for Animated Banner or Logo] -->
  <img src="assets/banner.png" alt="Smart Hadith Research Library Banner" width="100%">

  # 🕌 Smart Hadith Research Library (SaaS)
  
  **An Advanced Cloud-Based Academic Platform Bridging Deep Islamic Sciences with State-of-the-Art Software Engineering (Clean Architecture).**

  <!-- Badges -->
  <p>
    <img src="https://img.shields.io/badge/Frontend-Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white" alt="Flutter">
    <img src="https://img.shields.io/badge/State_Management-Riverpod-042B59?style=for-the-badge&logo=flutter&logoColor=white" alt="Riverpod">
    <img src="https://img.shields.io/badge/Backend-FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI">
    <img src="https://img.shields.io/badge/Database-SQLite_(Drift)-003B57?style=for-the-badge&logo=sqlite&logoColor=white" alt="SQLite Drift">
    <img src="https://img.shields.io/badge/Cloud-Cloudflare_Workers-F38020?style=for-the-badge&logo=cloudflare&logoColor=white" alt="Cloudflare">
  </p>

  [Live Demo](https://hadithresearchlibrary.pages.dev/)
</div>

---

## 📖 About The Project

The **Smart Hadith Research Library** is a comprehensive SaaS platform meticulously engineered to serve Islamic scholars, researchers, and academic institutions. 

Traditional Hadith research often involves navigating through thousands of structured manuscripts and text volumes—a time-consuming and error-prone process. This project solves this fundamental problem by digitizing and structuring massive volumes of Hadith research, pairing it with lightning-fast text search capabilities, and instantly synchronizing search results with high-resolution scans of the original manuscripts (PDFs).

The project is built on **Clean Architecture** principles to ensure high scalability and maintainability, with a clear separation of concerns between the UI, state management, and data layers (Local/Cloud).

## ✨ Key Features

*   🚀 **Ultra-Fast Advanced Text Search:** Local and cloud-based search engines optimized for accurate and rapid querying of Arabic text and structured Hadith documents.
    *   *![Search Interface Screenshot](assets/search_interface.png)*
*   🔄 **Real-Time Manuscript Synchronization (pdfrx):** Side-by-side view where navigating the digital text instantly syncs with the exact location in the original scanned PDF manuscript or book.
    *   *![Sync Feature GIF](assets/sync_feature.gif)*
*   📶 **Offline Support (Offline-First):** Thanks to efficient local caching with Drift (SQLite), users can access large parts of the library and perform complex searches without a constant internet connection.
*   📱 **Cross-Platform Accessibility:** A seamless, responsive experience across Web, Desktop, and Mobile, leveraging Flutter's unified codebase.
    *   *![Mobile & Web Mockups](assets/mockups.png)*

## 🏗️ Technical Architecture

This platform utilizes **Clean Architecture** to ensure maximum flexibility, scalability, and maintainability. The codebase heavily relies on SOLID principles and the Repository Pattern. The diagram below illustrates the data flow and component interaction:

<div align="center">

```mermaid
graph TD
    direction TB
    
    %% Presentation Layer
    subgraph Presentation["📱 Presentation Layer (Flutter Web Client)"]
        direction TB
        UI["UI Components"]
        State["State Management (Riverpod)"]
        UI <--> State
    end

    %% Domain Layer
    subgraph Domain["🧠 Domain Layer (Business Logic)"]
        direction TB
        UseCases["Search & Sync Engines"]
        Entities["Core Entities"]
        UseCases --> Entities
    end

    %% Data & Infrastructure Layer
    subgraph Data["☁️ Data & Infrastructure Layer"]
        direction TB
        Repos["Repositories"]
        LocalDB["Local Database (SQLite / Drift)"]
        CF_API["Cloudflare Workers API"]
        CF_R2["Cloudflare R2 Bucket"]
        
        Repos <--> LocalDB
        Repos <--> CF_API
        CF_API <--> CF_R2
    end

    %% Connections between layers
    State <-->|State Update| UseCases
    UseCases <-->|Data Request| Repos

    %% Styling
    classDef pres fill:#E3F2FD,stroke:#2196F3,stroke-width:2px,color:#0D47A1;
    classDef dom fill:#F3E5F5,stroke:#9C27B0,stroke-width:2px,color:#4A148C;
    classDef dat fill:#E8F5E9,stroke:#4CAF50,stroke-width:2px,color:#1B5E20;
    
    class UI,State pres;
    class Entities,UseCases dom;
    class Repos,LocalDB,CF_API,CF_R2 dat;
```

</div>

### Technology Stack Details:
*   **Frontend (Flutter & Dart):** Chosen for its unparalleled ability to deliver native-like performance and highly customized, interactive UI components across all platforms from a single codebase.
*   **State Management (Riverpod):** Used for robust and reactive state management across the application.
*   **Local Database (Drift / SQLite):** Implementing an offline-first approach with robust caching and local search capabilities.
*   **Backend & Cloud:** **Python & FastAPI** alongside **Cloudflare Workers API** for fast, asynchronous data processing, and **Cloudflare R2 Bucket** for efficient object storage.
*   **Document Handling:** The **pdfrx** library is used to seamlessly render and sync PDF files.

## 🔒 Source Code Notice (Showcase Repository)

> **Note to Recruiters and Engineering Managers:**
> This repository serves as a **Showcase / Presentation** of the project's architecture, UI/UX, and technical capabilities. 
> 
> Due to Intellectual Property (IP) protection and commercial licensing, the actual source code resides in a **private repository**. I am more than happy to discuss the technical implementation details, system design, and coding practices during an interview.
> 
> 🔗 **[Click here to try the Live Demo](https://hadithresearchlibrary.pages.dev/)**

## 📫 Contact & Connect

I am actively open to discussions regarding technical roles, collaborations, or investment opportunities.

*   💼 **LinkedIn:** [Insert LinkedIn Profile URL Here]
*   📧 **Email:** [Insert Email Address Here]

</div>
