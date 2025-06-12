# Mini-Challenge DEL: Hyperparameter Tuning und Model Evaluation

Dieses Projekt dokumentiert die vollständige Durchführung der Mini-Challenge im Modul Deep Learning. Ziel ist es, ein Bildklassifikationsmodell auf dem CIFAR-10 Datensatz zu entwickeln, verschiedene Optimierungsstrategien zu untersuchen und dabei ein fundiertes Verständnis für den Einfluss von Architektur, Hyperparametern und Regularisierung zu erlangen.

---

## Inhalte des Notebooks

Das Notebook ist in mehrere strukturierte Abschnitte unterteilt:

### 1. Setup & Datenverständnis
- **Datenquelle**: CIFAR-10 (60.000 RGB-Bilder, 10 Klassen)
- **EDA**: Klassenverteilung, visuelle Kontrolle, Pixelverteilungen
- **Preprocessing**: Normalisierung und stratified Splits in Train/Val/Test

### 2. Baseline-Modell & Trainingspipeline
- Einfaches CNN-Modell mit zwei Conv-Layern
- Implementierung einer sauberen Trainings- und Evaluationsfunktion
- Sanity Check: Overfitting auf ein einzelnes Bild
- Logging mit [Weights & Biases (W&B)](https://wandb.ai)

### 3. Cross-Validation
- 5-Fold Cross-Validation zur Einschätzung der Modellstabilität
- Geringe Streuung zeigt robuste Baseline-Architektur

### 4. Hyperparameter-Tuning
Insgesamt wurden **10 Hypothesen** formuliert und getestet:
- Lernrate (reduziert)
- Gewichtinitialisierung (Xavier)
- Architekturmodifikation (tiefer, breiter, größere Kernel, ohne Pooling)
- Regularisierung (Dropout, BatchNorm)
- Optimierer (SGD vs. Adam)
- Data Augmentation

Alle Modelle wurden systematisch verglichen hinsichtlich:
- Testgenauigkeit
- Precision, Recall, F1-Score
- Anzahl Parameter

### 5. Transfer Learning
- Einsatz von **ResNet18** (vortrainiert auf ImageNet)
- Fine-Tuning der letzten Layer für CIFAR-10
- Vergleich mit eigenem BestModel

---

## Ergebnisse & Erkenntnisse

| Modell         | Accuracy | Parameter |
|----------------|----------|-----------|
| BestModel      | 85.60 %  | 8.3 Mio   |
| ResNet18       | 78.04 %  | 11.2 Mio  |
| Augmentation   | 77.69 %  | 545k      |
| Deeper CNN     | 72.85 %  | 545k      |
| BaselineCNN    | 71.76 %  | 545k      |

**Hauptinsights**:
- Kombination erfolgreicher Maßnahmen (z. B. Dropout + BatchNorm + tiefer/breiter) ist effektiver als einzelne Änderungen
- Data Augmentation brachte große Fortschritte ohne zusätzliche Parameter
- Transfer Learning ist auch bei kleinen Datensätzen wie CIFAR-10 eine starke Alternative

---

## Voraussetzungen

Das Notebook basiert auf folgenden Paketen:

```bash
torch
torchvision
numpy
matplotlib
scikit-learn
Pillow
wandb
```

Alle Abhängigkeiten findest du in der Datei requirements.txt.

## Installation und Setup

1. **Repository klonen**  
```bash
# 1. Repository klonen
git clone <REPO_URL>
```
2. **Virtual Environment erstellen**
```bash
python -m venv venv
source venv/bin/activate      # Linux/macOS
venv\Scripts\activate.bat     # Windows
```

3. **Abhängigkeiten installieren**

```bash
pip install -r requirements.txt
```

4. **Weights & Biases konfigurieren**

```bash
wandb login
```