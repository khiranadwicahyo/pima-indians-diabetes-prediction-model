# pima-indians-diabetes-prediction-model
---

## Project

### About Project
Dalam project ini saya melakukan model prediksi pada data Pima Indians Diabetes Dataset. Dataset ini berasal dari Institut Nasional Diabetes dan Penyakit Pencernaan dan Ginjal. Tujuan dari kumpulan data ini adalah untuk memprediksi secara diagnostik apakah pasien menderita diabetes atau tidak, berdasarkan pengukuran diagnostik tertentu yang disertakan dalam kumpulan data. Beberapa batasan ditempatkan pada pemilihan contoh-contoh ini dari basis data yang lebih besar. Secara khusus, semua pasien di sini adalah perempuan berusia minimal 21 tahun yang berasal dari suku **Indian Pima**.

[Source : https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database]

### Library
* pandas
* numpy
* scikit-learn
* imblearn
* scipy
* matplotlib
* seaborn

### Datasets
Data termasuk dalam data catatan medis yang terdapat banyak data bertipe numberik dan satu-satunya data numberik hanyalah data pada variabel target **Outcome**. Keseluruhan data berdimensi 768 baris dengan 9 fitur.

### Feature Engineering 
1. **Outomme**

        # melakukan klasifikasi diabetes dari outcome

        def classify_outcome(outcome):
            if outcome == 0:
                return "Tidak Diabetes"
            else:
                return "Diabetes"
            
        # Memasukkan hasil decoding
        df['Category_outcome'] = df['Outcome'].apply(classify_outcome)
        df

2. **Glucose**

        # melakukan klasifikasi glukosa dalam tubuh

        def classify_glucose(glucose):
            if glucose < 140:
                return "Normal"
            elif  140 <= glucose <= 199:
                return "Prediabetes"
            else :
                return "Diabetes"
        # Memasukkan hasil decoding
        df['Category_glucose'] = df['Glucose'].apply(classify_glucose)
        df['Category_glucose'].value_counts()

3. **BMI**

        # melakukan klasifikasi BMI 

        def classify_bmi(bmi):
            if bmi < 18.5:
                return "Underweight"
            elif  18.5 <= bmi <= 24.9:
                return "Ideal"
            elif 25 <= bmi <= 29.9:
                return "Overweight"
            else:
                return "Obese"
        # Memasukkan hasil decoding
        df['Category_bmi'] = df['BMI'].apply(classify_bmi)
        df['Category_bmi'].value_counts()

4. **DPF**

        # melakukan klasifikasi glukosa dalam tubuh

        def classify_dpf(dpf):
            if dpf < 0.3:
                return "Rendah"
            elif  0.3 <= dpf <= 0.7:
                return "Sedang"
            elif  0.8 <= dpf <= 1.0:
                return "Tinggi"
            else :
                return "Sangat Tinggi"
            
        # Memasukkan hasil decoding
        df['Category_dpf'] = df['DiabetesPedigreeFunction'].apply(classify_dpf)
        df['Category_dpf'].value_counts()

5. **Insulin**

        # melakukan klasifikasi pada nilai insulin
        def classify_insulin(insulin):
            if insulin < 25:
                return 'Rendah'
            elif  25 <= insulin <= 200:
                return 'Normal'
            else:
                return 'Hiperinsulinemia'

        # apply pada fitur insulin dalam kolom baru
        df['Category_insulin'] = df['Insulin'].apply(classify_insulin)
        df['Category_insulin'].value_counts()


### Data Pre-Processing
**Handling Missing Values & Outlier**

!['Hasil Handling Missing Values](outputs/hasil%20handling%20missing%20values.png)
 Fitur Seperti **Glucose, BloodPressure, BMI, SkinThickness** terdapat data **missing values** dari ketiga fitur tersebut memiliki nilai 0 yang mana nilai ini tidak mungkin terjadi pada pemerikasaan darah pada manusia yang masih hidup. Sehingga data dengan missing values tersebut akan diisi nilai dengan rentan yang dapat diterima dengan menggunakan KNN. Namun untuk **Insulin** menggunakan nilai median untuk mengganti nilai missing values.

Perubahan lain juga dilakuan pada **data outlier (data insulin > 400)**. Perubahan ini dilakukan karena banyaknya data ekstrem yang sangat jauh dari jangkauan batas atas (upper whisker) yang mengindikasikan bahwa data tersebut **mungkin memiliki kesalahan input atau memang memiliki kondisi tubuh yang berbeda** sehingga perlu ditinjau secara terpisah. Maka dari itu saya memutuskan untuk merubah nilai insulin > 400 dengan batas nilai indikasi resistensi insulin yaitu > 200 dengan batas atas quartil yaitu 350. Karena pada kasus ini volume pasien cukup banyak ditemukan pada rentan nilai tersebut, sehingga hal ini dapat mengurangi kesalahan dalam menghapus nilai real dari suatu individu.






## Models
    Model Decision Tree Scores:
    Accuracy : 0.6663
    Precision : 0.6690
    F1_score : 0.6648
    Recall : 0.6663
    Model Random Forest Scores:
    Accuracy : 0.7513
    Precision : 0.7536
    F1_score : 0.7505
    Recall : 0.7513
    Model XGBoost Scores:
    Accuracy : 0.7412
    Precision : 0.7432
    F1_score : 0.7407
    Recall : 0.7412
    Model AdaBoost Scores:
    Accuracy : 0.7100
    Precision : 0.7110
    F1_score : 0.7096
    Recall : 0.7100

Dalam project ini ditemukan bahwa dua model yang memiliki performa terbaik yaitu **XGboost** dan **Random Forest**. Keduanya memberikan nilai akurasi yang sama baiknya berkisar pada 74%-75%.

## Evaluation
*Confusion Matrix XGBoost & Random Forest*
![Confusion Matrix](outputs/Hasil%20Confusion%20Matrix%20XGB%20&%20RF.png)
*ROC Precision-Recall*
![ROC-Precision Recall](outputs/Hasil%20ROC%20&%20Precision-Recall.png)
*Feature Importance*
![Feature Importance](outputs/Hasil%20feature%20Importance.png)

Evaluasi hasil dapat dilihat dari hasil Confusion Matrix, ROC Curve & Precisiion-Racall Curve, serta Feature Importance. Ketiganya akan memberikan anda pemahaman bagaimana hasil prediksi pada kedua model Xgboost dan Random Forest. Hasil ini masih dapat ditingkakan dengan Hypertuning pada model atau menggunakan algoritma model yang lebih kompleks (contoh Neural Network), karena dalam melakukan diagnosa medis hasil pada model perlu diperhatikan karena efeknya akan berpengaruh pada suatu pasien.
