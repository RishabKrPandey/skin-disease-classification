# 🩺 Skin Disease Classification using Transfer Learning

This project implements a Deep Learning solution to classify five common skin conditions. The goal was to develop a model capable of distinguishing between diseases that often share similar visual characteristics.

### 📋 Disease Classes:
* **Acne**
* **Eksima** (Eczema)
* **Herpes**
* **Panu** (Tinea Versicolor)
* **Rosacea**

---

## 🚀 The Technical Journey

### 1. Initial Approach & Overfitting Challenges
In the early stages, a standard Convolutional Neural Network (CNN) was trained from scratch. However, the model suffered from significant **overfitting**, plateauing at approximately **52% validation accuracy**. It struggled particularly with "look-alike" conditions, such as confusing the fungal patches of Panu with inflammatory Acne.

### 2. Optimization Strategy 🛠️
To bridge the gap between training and real-world performance, I implemented a three-step optimization strategy:

* **Transfer Learning:** Leveraged the `MobileNetV2` architecture, pre-trained on the ImageNet dataset. This provided a robust foundation of "visual vocabulary" (edges, textures, and shapes).
* **Data Augmentation:** To prevent the model from memorizing specific images, I introduced random rotations, horizontal flips, and zooms during training. This forced the model to learn invariant features.
* **Fine-Tuning:** After initial training, I unfroze the top layers of the base model and re-trained with a very low learning rate ($1 \times 10^{-5}$). This allowed the "expert" weights to adapt specifically to the nuances of dermatological textures.

### 3. Results & Performance 📈
Following fine-tuning, the model achieved a **61.13% validation accuracy**.

#### Error Analysis (Confusion Matrix)
By analyzing the Confusion Matrix, I identified that while accuracy is high, the model still faces challenges with "borderline" cases between **Eksima** and **Panu**. This insight is crucial for understanding where more diverse data is needed.

> **<img width="780" height="701" alt="image" src="https://github.com/user-attachments/assets/4cb8ae70-7078-4398-b0b9-2792dea0a932" />
]**

### 4. Real-World Inference & Uncertainty 🔍
The model utilizes a **Top-K (Top-3) Prediction** system. Instead of a single classification, it provides a ranked leaderboard of probabilities. This transparency allows for a better understanding of the model's "confidence" when conditions appear visually similar.

> **[<img width="337" height="121" alt="image" src="https://github.com/user-attachments/assets/67d0e5b6-4693-4c9e-a8db-10d2275c5b31" />
]**

---

## 🛠️ Tools & Technologies
* **Language:** Python 🐍
* **Framework:** TensorFlow / Keras 🤖
* **Model Architecture:** MobileNetV2
* **Environment:** Google Colab
* **Libraries:** NumPy, Matplotlib, Seaborn, Scikit-learn

---

## 📈 Future Improvements
* Collect more diverse high-resolution data for Eksima to reduce misclassification.
* Implement Class Weights to handle any remaining class imbalances.
* Deploy the model as a web application using Streamlit or Flask.
