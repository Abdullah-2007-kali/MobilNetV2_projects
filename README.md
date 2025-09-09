🩺 Skin Disease Classification using Transfer Learning
📌 مقدمة

هذا المشروع يهدف إلى تصنيف صور أمراض الجلد إلى عدة فئات طبية باستخدام تقنيات التعلم العميق (Deep Learning).
تم استخدام شبكة MobileNetV2 (مدربة مسبقًا على ImageNet) كأساس، مع تطبيق Transfer Learning و Fine-Tuning لتحسين الدقة.

⚙️ المكونات التقنية

لغة البرمجة: Python 3.12

المكتبات المستخدمة:

TensorFlow / Keras (لبناء وتدريب النموذج)

NumPy & Pandas (للتعامل مع البيانات)

Matplotlib & Seaborn (لتحليل النتائج والرسم البياني)

scikit-learn (لحساب metrics مثل classification report)

📂 هيكل البيانات

المشروع يعتمد على تقسيم البيانات إلى ثلاث مجلدات:

dataset/
│── train/   # بيانات التدريب
│── val/     # بيانات التحقق
│── test/    # بيانات الاختبار

🧠 خطوات العمل
1️⃣ استيراد البيانات

تم استخدام ImageDataGenerator لتوليد بيانات التدريب مع Augmentation (مثل التدوير، القلب، تغيير الإضاءة) لتحسين قدرة النموذج على التعميم.

2️⃣ بناء النموذج

استخدام MobileNetV2 كـ Base Model.

إضافة طبقات Dense + Dropout مخصصة.

تجميد جميع طبقات MobileNetV2 أولًا (Transfer Learning).

3️⃣ التدريب الأساسي (Transfer Learning)

تدريب الطبقات الجديدة فقط.

استخدام Optimizer Adam مع learning rate = 0.001.

حفظ أفضل نموذج باستخدام ModelCheckpoint.

4️⃣ Fine-Tuning

فك تجميد آخر 30 طبقة من MobileNetV2.

إعادة التدريب بمعدل تعلم أصغر 1e-5.

الهدف: تحسين دقة النموذج على البيانات الطبية.

5️⃣ حفظ النموذج

تم حفظ النموذج النهائي في ملف:

skin_disease_mobilnetv2_final.keras

📊 النتائج

بعد التقييم على بيانات test:

Test Accuracy: حوالي 34% (النموذج يحتاج تحسين إضافي بسبب صعوبة البيانات وعدم توازن الفئات).

Classification Report: يوضح الـ precision, recall, f1-score لكل فئة مرضية.

📌 مثال على بعض النتائج:

Nail Fungus → دقة عالية نسبيًا (0.75 f1-score).

بعض الفئات مثل Lupus, Systemic Disease → أداء ضعيف بسبب قلة العينات.

🔧 تحسينات مستقبلية

جمع بيانات أكثر وتوزيعها بشكل متوازن بين الفئات.

تجربة نماذج أكبر مثل EfficientNet أو ResNet.

استخدام Data Augmentation أكثر تعقيدًا.

تطبيق Class Weights أو Oversampling لمعالجة مشكلة عدم التوازن.

🚀 كيفية التشغيل

استنساخ المستودع:

git clone https://github.com/USERNAME/skin-disease-classification.git
cd skin-disease-classification


تثبيت المتطلبات:

pip install -r requirements.txt


تشغيل التدريب:

python train.py


تقييم النموذج:

python evaluate.py --model best_skin_model.keras --data dataset/test

👨‍⚕️ الهدف

المشروع يوضح إمكانية استخدام الذكاء الاصطناعي في المجال الطبي لدعم التشخيص المبكر لأمراض الجلد، لكنه ليس بديلًا عن الطبيب.
