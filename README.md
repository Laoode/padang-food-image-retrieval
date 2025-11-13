# Padang Food Image Retrieval Using Clip Model & Faiss Vector Database
- datasets: [kaggle](https://www.kaggle.com/datasets/faldoae/padangfood)

<img width="950" height="283" alt="image" src="https://github.com/user-attachments/assets/45606583-a665-423e-869a-ab28597e5bcd" />

<img width="950" height="184" alt="image" src="https://github.com/user-attachments/assets/ed9736b9-0da1-4a10-b3d2-eadd74d5da18" />

<img width="950" height="282" alt="image" src="https://github.com/user-attachments/assets/4f398a42-b744-4e8c-ac32-17c237c4856a" />

<img width="950" height="293" alt="image" src="https://github.com/user-attachments/assets/f06b9e5a-1ed3-4ea3-96c2-159cdffa92b7" />

<img width="976" height="405" alt="image" src="https://github.com/user-attachments/assets/e51cd9c4-4182-4a3e-817d-307b6748f4e8" />


# Padang Food Image Similarity Search Engine
## Project Summary

### 🎯 Objective
Built an AI-powered image similarity search system for Padang cuisine that allows users to find similar dishes by uploading food images or text descriptions.

### 🏗️ Technical Architecture
- **Embedding Model**: CLIP (ViT-B-32) - Multi-modal vision-language model
- **Vector Database**: FAISS (Facebook AI Similarity Search) with IndexFlatIP
- **Dataset**: 9 Padang food categories with ~200 images per category
- **Search Method**: Cosine similarity on 512-dimensional embeddings

### 📊 Performance Metrics (Top-5 Retrieval)

| Metric | Score | Interpretation |
|--------|-------|----------------|
| **Precision@5** | 76.9% | 4 out of 5 retrieved images are correct |
| **mAP** | 90.1% | Correct results appear early in rankings |
| **Recall@5** | 3.6% | Expected for large dataset (5 out of ~200 images) |

### 🏆 Category-Level Performance

**Best Performers:**
- Gulai Tunjang: 96.0% precision, 100% mAP
- Telur Balado: 96.0% precision, 99.0% mAP
- Dendeng Batokok: 88.0% precision, 95.0% mAP

**Needs Improvement:**
- Ayam Goreng: 56.0% precision (visually similar to ayam_pop)
- Gulai Tambusu: 60.0% precision (complex texture/appearance)
- Ayam Pop: 68.0% precision (confused with ayam_goreng)

### 💡 Key Insights
1. **CLIP performs well on visually distinct dishes** (eggs, rendang, dendeng)
2. **Similar-looking foods are challenging** (fried chicken variants, gulai varieties)
3. **High mAP scores indicate good ranking quality** - users see relevant results first
4. **Multi-modal capability works** - both text and image queries are supported


## 📈 Success Metrics to Track

| Metric | Current | Target (3 months) |
|--------|---------|-------------------|
| Precision@5 | 76.9% | 85%+ |
| mAP | 90.1% | 95%+ |
| Query Latency | ~500ms | <100ms |


## Example
```bash
Testing category: telur_balado (5 samples) ✓ P@5: 0.960 | R@5: 0.044 | mAP: 0.990
```

1. Konteks Pengujian
- Testing category: telur_balado: Model sedang diuji kemampuannya untuk mengenali, mengklasifikasi, atau mengambil hasil yang relevan dengan topik "telur balado".

- (5 samples): Pengujian ini dilakukan pada 5 kasus uji atau 5 query (permintaan pencarian) yang berbeda terkait "telur balado".

2. P@5 (Precision at 5): 0.960
- Precision (Presisi): Mengukur ketepatan. Yaitu, berapa persen dari hasil yang diprediksi/diambil oleh model yang benar-benar relevan.
- @5: Perhitungan hanya dilakukan pada 5 hasil teratas (ranking 1 hingga 5) yang dikembalikan oleh model.

<b>Interpretasi Hasil:</b>
```bash
P@5: 0.960 -> 96%
````

Ini berarti bahwa, rata-rata dari 5 hasil teratas yang diprediksi model, sebanyak 96% di antaranya adalah benar atau relevan dengan "telur balado".

Kesimpulan P@5: Model memiliki akurasi yang sangat tinggi dalam memberikan prediksi yang benar pada urutan paling atas.

3. R@5 (Recall at 5): 0.044
- Recall (Daya Ingat): Mengukur kelengkapan. Yaitu, berapa persen dari total seluruh item relevan yang tersedia (ground truth) berhasil ditemukan oleh model.
- @5: Perhitungan hanya dilakukan berdasarkan item relevan yang berhasil ditemukan dalam 5 hasil teratas.

```bash
{R@5}: 0.044 -> 4.4%
````

Ini berarti bahwa, 5 hasil teratas yang diberikan model hanya berhasil menangkap 4.4% dari keseluruhan item yang seharusnya relevan dengan "telur balado" di dalam dataset pengujian.

Kesimpulan R@5: Model hanya menemukan sebagian kecil dari total item relevan yang ada. Tingkat recall sangat rendah.

Mengapa P@5 Tinggi, tapi R@5 Rendah?

Ini adalah situasi yang umum terjadi dan menunjukkan adanya trade-off antara Precision dan Recall.

1. Model sangat yakin dan akurat dengan apa yang diprediksi di awal (P@5 tinggi).

2. Namun, Total item relevan yang ada dalam dataset untuk "telur balado" ternyata sangat banyak.

3. karena itu, meskipun 96% dari 5 hasil teratasnya benar, 5 hasil tersebut hanya mewakili sebagian kecil (4.4%) dari keseluruhan item relevan yang tersedia.

- mAP (Mean Average Precision): Metrik ini adalah ukuran performa yang paling komprehensif, karena mengevaluasi kualitas urutan (ranking) hasil dari model di semua 5 samples.

- Ia mengukur seberapa konsisten model berhasil menempatkan semua hasil yang relevan di posisi teratas. Semakin tinggi nilainya (mendekati 1.0), semakin baik rankingnya

<b>Interpretasi Hasil</b>
```bash
{mAP}: 0.990 -> 99%
````
Ini adalah skor mAP yang luar biasa tinggi (hampir sempurna).
Kesimpulan mAP: Secara keseluruhan, kualitas ranking hasil yang diberikan oleh model untuk kategori "telur balado" adalah sangat baik. Ini mengindikasikan bahwa item-item yang relevan ditemukan secara konsisten di urutan paling atas pada 5 kasus uji tersebut.

## 🎯 Conclusion

Your Padang food similarity search achieves **77% precision and 90% mAP** - this is solid performance for a first iteration! The system works well for visually distinct dishes but struggles with similar-looking items (ayam variants, gulai types).
