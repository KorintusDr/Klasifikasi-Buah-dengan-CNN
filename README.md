# Klasifikasi Buah dengan CNN

## Deskripsi
Proyek ini bertujuan untuk mengklasifikasikan gambar buah-buahan berdasarkan dataset **Fruits 360** dari Kaggle. Model ini dilatih dengan teknik augmentasi gambar dan dikonversi ke berbagai format seperti TensorFlow Lite dan TensorFlow.js.

## Dataset
Dataset yang digunakan adalah **Fruits 360**, yang berisi berbagai gambar buah dalam berbagai kategori.
Dataset dapat diunduh secara otomatis melalui perintah berikut:
```bash
kaggle datasets download moltean/fruits -p . --unzip
```
Setelah diunduh, dataset akan disusun ulang agar lebih mudah digunakan dalam proses pelatihan.

## Instalasi dan Dependensi
Pastikan Anda telah menginstal semua dependensi yang diperlukan:
```bash
pip install --upgrade tensorflow tensorflowjs kaggle numpy pandas pillow matplotlib scikit-learn
```

## Struktur Direktori
Setelah menjalankan kode, struktur folder akan menjadi sebagai berikut:
```
submission/
├── fruits/
├── saved_model/
├── tflite/
├── tfjs_model/
```

## Arsitektur Model
Model CNN yang digunakan memiliki beberapa lapisan sebagai berikut:
- **3 Lapisan Convolutional** dengan Batch Normalization dan LeakyReLU
- **Pooling Layers** untuk mengurangi dimensi
- **Dense Layers** dengan Dropout untuk mencegah overfitting
- **Output Layer** dengan aktivasi softmax

## Proses Pelatihan
Model dilatih menggunakan optimizer **Adam** dengan fungsi loss **categorical crossentropy**. Selain itu, callback **Early Stopping** dan **ReduceLROnPlateau** digunakan untuk mengoptimalkan proses pelatihan.

Pelatihan dilakukan dengan:
```python
history = model.fit(train_images,
                    validation_data=test_images,
                    epochs=20,
                    steps_per_epoch=100,
                    validation_steps=25,
                    callbacks=[early_stopping, reduce_lr])
```

### Hasil Pelatihan
| Metrik               | Nilai   |
|----------------------|--------|
| **Training Loss**    | 0.17231 |
| **Training Accuracy** | 95.12% |
| **Test Loss**        | 0.08542 |
| **Test Accuracy**    | 97.23% |

## Konversi Model
Model yang telah dilatih dikonversi ke beberapa format:
- **TensorFlow SavedModel**
- **TensorFlow Lite (TFLite)** untuk perangkat seluler
- **TensorFlow.js (TFJS)** untuk penggunaan di browser


## Visualisasi Kinerja Model
Selama pelatihan, akurasi dan loss divisualisasikan dengan Matplotlib:
```python
plt.plot(history.history['accuracy'], label='Train Accuracy')
plt.plot(history.history['val_accuracy'], label='Validation Accuracy')
plt.legend()
plt.show()
```

## Kesimpulan
Model ini berhasil mencapai akurasi **97.23%** pada dataset pengujian, menunjukkan performa yang sangat baik dalam klasifikasi buah.

## Lisensi
Proyek ini menggunakan dataset dari Kaggle dan dapat digunakan untuk tujuan edukasi dan penelitian.
