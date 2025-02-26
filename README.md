# pima-indians-diabetes-prediction-model
---

## About 
Dalam project ini saya melakukan model prediksi pada data Pima Indians Diabetes Dataset. Dataset ini berasal dari Institut Nasional Diabetes dan Penyakit Pencernaan dan Ginjal. Tujuan dari kumpulan data ini adalah untuk memprediksi secara diagnostik apakah pasien menderita diabetes atau tidak, berdasarkan pengukuran diagnostik tertentu yang disertakan dalam kumpulan data. Beberapa batasan ditempatkan pada pemilihan contoh-contoh ini dari basis data yang lebih besar. Secara khusus, semua pasien di sini adalah perempuan berusia minimal 21 tahun yang berasal dari suku **Indian Pima**.

## Models
Dalam project ini ditemukan bahwa dua model yang memiliki performa terbaik yaitu **XGboost** dan **Random Forest**. Keduanya memberikan nilai akurasi yang sama baiknya berkisar pada 74%-75%.

## Evaluation
Evaluasi hasil dapat dilihat dari hasil Confusion Matrix, ROC Curve & Precisiion-Racall Curve, dan Feature Importance. Ketiganya akan memberikan anda pemahaman bagaimana hasil prediksi pada kedua model Xgboost dan Random Forest. Hasil ini masih dapat ditingkakan dengan Hypertuning pada model atau menggunakan algoritma model yang lebih kompleks (contoh Neural Network), karena dalam melakukan diagnosa medis hasil pada model perlu diperhatikan karena efeknya akan berpengaruh pada suatu pasien.
