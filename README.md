Festus Mikhael / 122140087  
Kenneth Austin / 122140043

# Plain-34 vs ResNet-34  vs Modified ResNet-34

## Konfigurasi Hyperparameter

Eksperimen ini menggunakan konfigurasi hyperparameter yang identik untuk memastikan perbandingan performa yang adil.

| Parameter | Nilai |
| :--- | :--- |
| **Dataset** | Dataset Makanan Indonesia (5 Kelas) |
| **Model** | Plain-34 dan ResNet-34 |
| **Epochs** | 10 |
| **Batch Size** | 16 |
| **Learning Rate (LR)** | 0.01 |
| **Optimizer** | SGD dengan Momentum (0.9) |
| **Scheduler** | StepLR (step=7, gamma=0.1) |

---

## Metrik Performa

# Plain-34
<img width="507" height="223" alt="image" src="https://github.com/user-attachments/assets/2912267b-b6cf-4afe-8c0c-d16365b83de8" />

# ResNet-34
<img width="504" height="228" alt="image" src="https://github.com/user-attachments/assets/3cf93b83-9fbb-4b70-ae2d-0e32a236cd91" />

# Modified ResNet-34
<img width="502" height="228" alt="Screenshot 2025-10-02 173201" src="https://github.com/user-attachments/assets/353efbb0-2401-42b8-85ce-c3379fbd21db" />

---

## Grafik Perbandingan

# Grafik Training Loss
<img width="500" height="300" alt="training_loss_comparison" src="https://github.com/user-attachments/assets/01f09a18-3582-4fe2-ae27-f2c51d38c3f4" />

# Grafik Training Accuracy
<img width="500" height="300" alt="training_accuracy_comparison" src="https://github.com/user-attachments/assets/e5a79959-2f5e-4221-82ac-979dde8d970d" />

# Grafik Validation Loss
<img width="500" height="300" alt="validation_loss_comparison" src="https://github.com/user-attachments/assets/add17b33-f462-41c1-98a6-8b9df7f94f7b" />

# Grafik Validation Accuracy
<img width="500" height="300" alt="validation_accuracy_comparison" src="https://github.com/user-attachments/assets/5db351d5-74d3-43fc-bf80-f6c7fac953c3" />

---

## Arsitektur Model Modifikasi (Tahap 3)

Model hibrida Tahap 3 mengintegrasikan empat modifikasi utama:

1.  **Multi-Path Block (Stage 2):** Menggunakan jalur paralel $3 \times 3$ dan $5 \times 5$ untuk menangkap fitur multi-skala.
2.  **ResNeXt-like Block (Stage 3 & 4):** Menerapkan konsep Cardinality ($C=4$) untuk meningkatkan kapasitas representasional.
3.  **Leaky ReLU:** Menggantikan ReLU standar untuk meningkatkan stabilitas aliran gradien.
4.  **Dropout ($p=0.5$):** Ditempatkan sebelum lapisan *classifier* untuk \*\*regularization\*\* yang ketat.

## Analisis

Analisis kinerja dari ketiga model (Plain-34, ResNet-34, dan Modified ResNet-34) membuktikan manfaat fundamental koneksi residual dan mengkonfirmasi trade-off kritis dari regularization. Model Plain-34 dikonfirmasi mengalami degradasi total, gagal dalam training maupun generalization. ResNet-34 standar berhasil mengatasi masalah tersebut, mencapai akurasi validasi tertinggi (≈67%), menjadikannya baseline yang kuat.

Namun, Model Modifikasi Hibrida (dengan Multi-Path, ResNeXt, dan Leaky ReLU) mengalami konflik kinerja yang signifikan: akurasi validasinya anjlok ke ≈59% di epoch 10. Penurunan drastis ini disebabkan oleh regularization **Dropout p=0.5** yang terlalu agresif. Loss training tertinggi dan konvergensi paling lambat pada Model Modifikasi menunjukkan bahwa **Dropout secara aktif mencegah model mencapai potensi arsitekturalnya** dalam durasi pelatihan yang singkat, menyebabkan underfitting parah alih-alih generalization yang stabil. Model ini berpotensi superior di jangka panjang, namun kinerja awal dibatasi oleh pemilihan hyperparameter.


