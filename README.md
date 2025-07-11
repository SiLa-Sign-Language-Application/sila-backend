# Backend FastAPI SiLa

API Backend untuk **SiLa – Sign Language Application**, aplikasi pengenalan Bahasa Isyarat Indonesia secara real-time menggunakan klasifikasi landmark tangan berbasis MLP.

## Teknologi yang Digunakan

- **Backend**: FastAPI (Python)
- **Model ML**: TensorFlow (`.h5` format)
- **Deployment**: Railway / Uvicorn
- **Gaya API**: RESTful
- **Middleware**: CORS (FastAPI)
- **Input Model**: Vektor landmark (42 nilai float)

## Langkah Instalasi

1. Clone repositori ini
   ```bash
   git clone https://github.com/SiLa-Sign-Language-Application/sila-backend.git
   cd sila-backend
   ```
2. Buat dan aktifkan environment virtual:
   ```bash
   python -m venv venv
   source venv/bin/activate  # di Windows: venv\Scripts\activate
   ```
4. Install dependensi:
   ```bash
   pip install -r requirements.txt
   ```
5. Buat folder `model/` dan tambahkan:
   - `gesture_mlp_model.h5` — file model terlatih
   - `label.json` — file mapping label ke karakter

6. Jalankan server lokal:
   ```bash
   uvicorn main:app --reload
   python main.py
   ```

## Variabel Lingkungan (Opsional)

Jika menggunakan layanan seperti Railway, tambahkan variabel berikut:

```
PORT=8000
```

## Endpoint API

### `POST /predict`

**Deskripsi**: Memprediksi karakter bahasa isyarat dari 42 nilai landmark tangan.

#### Contoh Request Body

```json
{
  "landmarks": [0.123, 0.456, ..., 0.789]  // tepat 42 nilai float
}
```

#### Contoh Response

```json
{
  "label": "A",
  "confidence": 0.9876
}
```

#### Kemungkinan Error

- **Jumlah input tidak sesuai**:
```json
{
  "detail": "Expected 42 values for landmarks"
}
```

- **Error internal server**:
```json
{
  "detail": "Internal Server Error: <pesan error>"
}
```

## Catatan Deployment

- Backend ini dapat dideploy ke Railway, Render, Fly.io, atau server lain.
- Pastikan folder `model/` dan file model tersedia di server.
- Uvicorn akan menggunakan `PORT` dari variabel lingkungan.

## Struktur Proyek

```
sila-backend
├── README.md
├── main.py
├── requirements.txt
├── model/
│   ├── gesture_mlp_model.h5
│   └── label.json
```
