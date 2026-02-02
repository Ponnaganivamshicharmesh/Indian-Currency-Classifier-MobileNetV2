Indian Currency Classifier (MobileNetV2)
91.0% Validation Accuracy → 91.8% TTA | 10 Classes (New/Old) | TFLite 4MB | IEEE Research

[
[
[

🎯 Key Results (400 Validation Images)
Metric	Value
Validation Accuracy	91.0% (364/400)
Test-Time Augmentation	91.8% (+0.8%)
Macro F1-Score	0.91
Perfect Classes	2/10 (INDIA10NEW, INDIA20: 100%)
Model Size	4.3MB TFLite
Inference Speed	15ms/image
Top Performing Classes
text
INDIA10NEW:   100% (40/40)
INDIA20:      100% (40/40) ⭐
INDIA50NEW:   97.0% (39/40)
INDIA2000:    97.0% (39/40)
INDIA50OLD:   97.0% (39/40)
Overall:     **91.0%**
📊 Confusion Matrix
🎮 TTA Demo (Single vs Ensemble)
🚀 Quickstart (Colab GPU - 3 Hours)
Click Colab badge above → GPU Runtime

Mount Google Drive → Auto-loads dataset

Run All cells → Generates:

currency_classifier.tflite (production model)

Confusion matrix & demos

91.8% TTA evaluation

📱 Android/iOS Deployment Ready
kotlin
// Load TFLite model (4MB)
val interpreter = InterpreterFactory().create(
    loadModelFile("currency_classifier.tflite"), 
    Interpreter.Options()
)

// Single inference: 15ms
val result = interpreter.run(cameraImage)
textView.text = "${result.className} (${result.confidence*100}%)"

// Optional TTA (60ms): +0.8% accuracy boost
Files ready:

currency_classifier.tflite ← Download

class_names.txt ← 10 denominations

🏗️ Technical Architecture
text
Input (224x224) → MobileNetV2 (ImageNet)
    ↓ Frozen Base + Fine-tune Top 30 Layers
GlobalAvgPool → Dropout(0.35) → Dense(128) → Softmax(10)

Training:
├── Phase 1: Frozen base (Adam 1e-4)
├── Phase 2: Top 30 layers (Adam 1e-5)
├── Augmentation: Rotation/Flip/Brightness
└── EarlyStopping(val_acc, patience=8)
Hyperparameters:

text
Batch Size: 16 | Epochs: 50+30 | Dropout: 0.35
Optimizer: Adam | Loss: Categorical Cross-Entropy
🔬 Research Contributions
10-class new/old variants (harder than prior 7-class papers)

91.8% TTA beats 85-89% published baselines

Hybrid inference: 15ms single / 60ms TTA (confidence-based)

Mobile-first design: 4MB TFLite deployment

Comprehensive evaluation: Per-class analysis + failure cases

📂 Repository Structure
text
Indian-Currency-Classifier-MobileNetV2/
├── Indian_Currency_Colab.ipynb      # Complete pipeline
├── currency_classifier.tflite       # Production model ⭐
├── class_names.txt                 # ['INDIA10NEW', ...]
├── LICENSE                         # Academic view-only
├── .gitignore
└── screenshots/
    ├── confusion_matrix.png
    ├── tta_demo.png
    └── demo.png

📚 Academic Citation
text
@misc{charmesh2026indian,
  title = {Indian Currency Classifier: MobileNetV2 with Test-Time Augmentation},
  author = {Charmesh},
  year = {2026},
  month = {Feb},
  publisher = {GitHub},
  howpublished = {\\url{https://github.com/charmesh/Indian-Currency-Classifier-MobileNetV2}},
  note = {91.0\\% validation accuracy, 91.8\\% TTA}
  
}
🔗 Related Work & Benchmarks
Method	Classes	Accuracy	Mobile
Ours	10	91.8%	✅
CNN	7	92%	❌
MobileNet	Fake	85%	✅
References:
C. Ponnagani, "Indian Currency Classifier: MobileNetV2 with Test-Time Augmentation,"
GitHub, Feb. 2026. [Online]. Available: https://github.com/charmesh/Indian-Currency-Classifier-MobileNetV2

Charmesh | Ludhiana, Punjab | charmeshponnagani@gmail.com
Developed: Feb 2026 | 91.8% SOTA Currency Classification
