# Vehicle Direction Detection Dataset

Dataset untuk deteksi arah kendaraan (Vehicle Direction Detection) menggunakan YOLO format. Dataset ini dikumpulkan untuk sistem ANPR (Automatic Number Plate Recognition) dengan tujuan mengidentifikasi apakah kendaraan bergerak dengan arah yang benar atau berlawanan.

**Dataset ini diambil langsung oleh peneliti: [rockmind](https://github.com/salsabilaputri95).**

**Lokasi pengambilan dataset: Indonesia, Provinsi Sulawesi Selatan.**
# Vehicle Direction Detection Dataset

Dataset untuk deteksi arah kendaraan (Vehicle Direction Detection) menggunakan YOLO format. Dataset ini dikumpulkan untuk sistem ANPR (Automatic Number Plate Recognition) dengan tujuan mengidentifikasi apakah kendaraan bergerak dengan arah yang benar atau berlawanan.

## 📋 Deskripsi Dataset

Dataset ini berisi gambar kendaraan yang diambil dalam berbagai kondisi pencahayaan untuk melatih model deteksi arah kendaraan. Setiap gambar telah dianotasi dengan bounding box dan label kelas.

### Kondisi Pencahayaan

Dataset terdiri dari 3 kondisi pencahayaan yang berbeda:

- **🌙 Malam (Low)**: Kondisi pencahayaan rendah/malam hari
- **🌆 Sore (Normal)**: Kondisi pencahayaan normal/sore hari
- **☀️ Siang (Harsh)**: Kondisi pencahayaan tinggi/siang hari

## 📊 Statistik Dataset

| Split | Jumlah Gambar |
|-------|---------------|
| Train | 522 images    |
| Validation | 112 images |
| Test | 99 images |
| **Total** | **733 images** |

## 🏷️ Kelas

Dataset ini memiliki **2 kelas** untuk deteksi:

| ID | Nama Kelas | Deskripsi |
|----|------------|-----------|
| 0 | `correct_vehicle_direction` | Kendaraan bergerak dengan arah yang benar |
| 1 | `opposite_vehicle_direction` | Kendaraan bergerak dengan arah berlawanan |

## 📁 Struktur Dataset

```
arah-kendaraan/
├── data.yaml              # File konfigurasi dataset untuk YOLO
├── train/
│   ├── images/            # Gambar training (522 gambar)
│   └── labels/            # Label YOLO format (.txt)
├── val/
│   ├── images/            # Gambar validasi (112 gambar)
│   └── labels/            # Label YOLO format (.txt)
└── test/
    ├── images/            # Gambar testing (99 gambar)
    └── labels/            # Label YOLO format (.txt)
```

## 📝 Format Anotasi

Dataset menggunakan format YOLO untuk anotasi. Setiap file `.txt` berisi informasi bounding box dengan format:

```
<class_id> <x_center> <y_center> <width> <height>
```

Dimana:
- `class_id`: ID kelas (0 atau 1)
- `x_center`, `y_center`: Koordinat pusat bounding box (normalized 0-1)
- `width`, `height`: Lebar dan tinggi bounding box (normalized 0-1)

## 🚀 Penggunaan

### Training dengan YOLOv8

```python
from ultralytics import YOLO

# Load model
model = YOLO('yolov8n.pt')

# Train model
results = model.train(
    data='data.yaml',
    epochs=100,
    imgsz=640,
    batch=16
)
```

### Inference

```python
from ultralytics import YOLO

# Load trained model
model = YOLO('path/to/best.pt')

# Predict
results = model.predict('path/to/image.jpg')

# Process results
for result in results:
    boxes = result.boxes
    for box in boxes:
        class_id = int(box.cls)
        confidence = float(box.conf)
        print(f"Class: {class_id}, Confidence: {confidence:.2f}")
```

## 🔧 Instalasi Dependencies

```bash
pip install ultralytics opencv-python pillow
```

## 💡 Use Cases

Dataset ini dapat digunakan untuk:

- ✅ Deteksi kendaraan yang melawan arus
- ✅ Sistem monitoring lalu lintas
- ✅ Integrasi dengan sistem ANPR
- ✅ Analisis pelanggaran lalu lintas
- ✅ Smart traffic management system

## 📈 Rekomendasi Training

- **Image Size**: 640x640 atau 1280x1280
- **Batch Size**: 16-32 (tergantung GPU)
- **Epochs**: 100-200
- **Optimizer**: AdamW atau SGD
- **Augmentation**: Mosaic, MixUp, HSV augmentation untuk meningkatkan robustness terhadap variasi pencahayaan

## 📌 Catatan

- Dataset mencakup berbagai kondisi pencahayaan untuk meningkatkan generalisasi model
- Cocok untuk deployment dalam sistem ANPR real-time


## 🤝 Kontribusi

Kontribusi untuk meningkatkan dataset ini sangat diapresiasi. Silakan buat pull request atau buka issue untuk diskusi.


---

**Note**: Dataset ini dibuat untuk tujuan penelitian dan pengembangan sistem ANPR dengan fokus pada deteksi arah kendaraan.
