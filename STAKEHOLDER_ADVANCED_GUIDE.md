# Stakeholder Management System - Advanced Analytics

## Overview
Sistem Stakeholder Management Advanced adalah modul komprehensif untuk analisis sentimen dan pemetaan network stakeholder dengan klasifikasi otomatis berdasarkan interaksi dan hubungan antar stakeholder.

## Fitur Utama

### 1. Dashboard Statistics
- **Pro-Aktif**: Stakeholder yang mendukung proyek dan aktif terlibat
- **Pro-Pasif**: Stakeholder yang mendukung proyek namun kurang aktif
- **Kontra-Aktif**: Stakeholder yang menolak proyek dan aktif melawan
- **Kontra-Pasif**: Stakeholder yang menolak proyek namun pasif

### 2. Network Visualization
Visualisasi network menampilkan:
- **Node (Stakeholder)** dengan warna berdasarkan sentiment:
  - 🟢 Hijau = Pro-Aktif
  - 🔵 Biru = Pro-Pasif
  - 🟡 Kuning = Kontra-Pasif
  - 🔴 Merah = Kontra-Aktif
  - ⚫ Abu-abu = Netral

- **Connections (Relasi)** dengan ketebalan berdasarkan closeness score:
  - Garis tebal (3px) = Score > 70 (Strong)
  - Garis sedang (2px) = Score 40-70 (Medium)
  - Garis tipis (1px) = Score < 40 (Weak)

### 3. Tab Master Stakeholder
Input data dasar stakeholder:
- Identitas (Nama, NIK, Role)
- Lokasi (Desa, Kecamatan, Kabupaten)
- Kontak (Telepon, Email)
- **Level Pengaruh** (1-5): Seberapa besar pengaruh stakeholder terhadap keputusan masyarakat
- **Level Kepentingan** (1-5): Seberapa besar dampak proyek terhadap stakeholder

### 4. Tab Latar Belakang & Atribut Relasi
Tracking background stakeholder untuk identifikasi shared attributes:
- **Pendidikan**: Jenjang, Universitas, Jurusan, Tahun lulus
- **Pekerjaan**: Pekerjaan utama, Instansi, Jabatan
- **Organisasi**: Keanggotaan organisasi (untuk identifikasi network)
- **Kekerabatan**: Status dan detail hubungan keluarga dengan stakeholder lain
- **Lokasi**: Dusun/RT/RW (untuk identifikasi tetangga)

### 5. Tab Isu/Project per Stakeholder
Tracking persepsi stakeholder terhadap project:
- **Project/Isu**: Nama project yang mempengaruhi stakeholder
- **Jenis Dampak**: Ekonomi, Sosial, Lingkungan, Aset Lahan, Infrastruktur
- **Besaran Dampak**: Skala 1-5
- **Persepsi Umum**: Positif, Netral, atau Negatif
- **Topik Keberatan**: Detail keberatan atau concern stakeholder

### 6. Tab Log Interaksi & Sentimen
Ini adalah tab KUNCI untuk klasifikasi sentimen otomatis:

#### Input Data Interaksi:
- Tanggal interaksi
- Lokasi pertemuan
- Jenis interaksi (Rapat Desa, Kunjungan, Sosialisasi, dll)
- Topik pembahasan
- Perilaku yang diamati
- Pernyataan kunci (kutipan langsung)

#### Scoring System:
**Arah Sikap (-2 s/d +2):**
- **-2**: Sangat Kontra (menolak keras, menentang)
- **-1**: Kontra (tidak setuju, mengkritik)
- **0**: Netral (tidak berpendapat jelas)
- **+1**: Pro (setuju, mendukung)
- **+2**: Sangat Pro (sangat mendukung, antusias)

**Level Aktivitas (1-4):**
- **1**: Pasif (hanya mendengar, tidak bicara)
- **2**: Cukup (sesekali bicara, tidak dominan)
- **3**: Aktif (sering bicara, aktif diskusi)
- **4**: Sangat Aktif (dominan, memimpin diskusi)

#### Klasifikasi Otomatis:
Sistem akan otomatis mengklasifikasikan berdasarkan kombinasi:
- **Pro-Aktif**: Arah Sikap > 0 DAN Level Aktivitas ≥ 3
- **Pro-Pasif**: Arah Sikap > 0 DAN Level Aktivitas < 3
- **Kontra-Aktif**: Arah Sikap < 0 DAN Level Aktivitas ≥ 3
- **Kontra-Pasif**: Arah Sikap < 0 DAN Level Aktivitas < 3
- **Netral**: Arah Sikap = 0

### 7. Tab Relasi & Network
Mapping hubungan antar stakeholder:

#### Jenis Relasi:
- Keluarga inti
- Keluarga besar
- Tetangga
- Rekan kerja
- Rekan organisasi
- Teman

#### Frekuensi Kontak:
- Harian
- Mingguan
- Bulanan
- Jarang

#### Score Closeness (0-100):
Calculated based on:
- Frekuensi interaksi (25%)
- Shared attributes:
  - Satu universitas (+15)
  - Satu jurusan (+10)
  - Satu organisasi (+20)
  - Hubungan kekerabatan (+30)

#### Arah Pengaruh:
- A → B (A mempengaruhi B)
- B → A (B mempengaruhi A)
- Bidirectional (Saling mempengaruhi)

### 8. Tab Dokumen & Bukti
Management evidence dokumentasi:
- **Jenis Bukti**: Notulen, Foto, Rekaman Audio, Video, Surat, Dokumen
- **Deskripsi**: Detail dokumen
- **Tanggal Dokumen**: Kapan dibuat/didapat
- **Penanggung Jawab**: Siapa yang mengumpulkan/menyimpan
- **Link ke Stakeholder**: Dokumen terkait stakeholder mana
- **File Upload**: Upload file evidence

## Cara Penggunaan

### Workflow Standar:

#### 1. Input Master Stakeholder
- Identifikasi semua stakeholder (individu maupun kelompok)
- Input data dasar dan kontak
- Tentukan level pengaruh dan kepentingan

#### 2. Input Background
- Lengkapi data pendidikan, pekerjaan, organisasi
- Identifikasi hubungan kekerabatan antar stakeholder
- Data ini akan digunakan untuk network analysis

#### 3. Input Isu/Project
- Mapping dampak project terhadap masing-masing stakeholder
- Catat persepsi awal dan keberatan

#### 4. Log Interaksi (PALING PENTING!)
- Setiap kali ada pertemuan/interaksi, WAJIB log di sini
- Catat pernyataan kunci (kutipan langsung)
- Tentukan arah sikap dan level aktivitas
- Sistem akan otomatis klasifikasi sentimen

#### 5. Mapping Relasi
- Identifikasi hubungan antar stakeholder
- Hitung closeness score berdasarkan shared attributes
- Tentukan arah pengaruh untuk strategy engagement

#### 6. Upload Evidence
- Upload semua dokumen pendukung (notulen, foto, rekaman)
- Link ke stakeholder dan interaksi terkait
- Untuk dokumentasi dan legal purposes

## Analisis & Strategy

### Prioritas Engagement:
1. **High Priority**: 
   - Kontra-Aktif dengan Level Pengaruh 4-5
   - Pro-Aktif dengan Level Pengaruh 4-5 (perlu dipertahankan)

2. **Medium Priority**:
   - Kontra-Pasif dengan Level Pengaruh 3-5
   - Pro-Pasif yang bisa diaktifkan

3. **Low Priority**:
   - Stakeholder dengan Level Pengaruh 1-2
   - Sudah Pro-Aktif dengan Level Pengaruh rendah

### Strategy Berdasarkan Klasifikasi:

#### Pro-Aktif:
- **Strategy**: Maintain & Leverage
- **Action**: Jadikan champion/advocate, libatkan dalam sosialisasi
- **Risk**: Jangan sampai berubah menjadi pasif atau kontra

#### Pro-Pasif:
- **Strategy**: Activate & Engage
- **Action**: Ajak lebih aktif, berikan role/tanggung jawab
- **Risk**: Bisa jadi kontra jika ada isu negatif

#### Kontra-Aktif:
- **Strategy**: Mitigate & Negotiate
- **Action**: Intensive engagement, address concerns, cari kompromi
- **Risk**: TINGGI - bisa mempengaruhi stakeholder lain

#### Kontra-Pasif:
- **Strategy**: Monitor & Address
- **Action**: Pahami concern, cari solusi win-win
- **Risk**: Bisa menjadi aktif jika ada trigger

### Network Analysis:
- **Identify Key Influencers**: Stakeholder dengan banyak connections dan closeness score tinggi
- **Identify Clusters**: Kelompok stakeholder yang saling terhubung
- **Strategy Indirect Influence**: Pengaruhi key influencers untuk mempengaruhi cluster
- **Risk Assessment**: Cluster kontra-aktif perlu special attention

## Technical Notes

### Network Visualization Engine:
- Menggunakan HTML5 Canvas untuk rendering
- Layout: Circular layout untuk visualisasi sederhana
- Node size: Fixed 30px radius
- Line thickness: Berdasarkan closeness score
- Color coding: Berdasarkan sentiment classification

### Data Structure:
```typescript
Stakeholder {
  id, nama, role, desa, level_pengaruh, level_kepentingan, 
  klasifikasi_sikap (calculated)
}

Background {
  stakeholder_id, pendidikan, pekerjaan, organisasi, 
  kekerabatan, lokasi
}

Interaction {
  stakeholder_id, tanggal, jenis_interaksi, pernyataan_kunci,
  arah_sikap (-2 to +2), level_aktivitas (1-4),
  klasifikasi_sentimen (auto-calculated)
}

Relation {
  stakeholder_a_id, stakeholder_b_id, jenis_relasi,
  frekuensi_kontak, skor_kedekatan_total (0-100),
  arah_pengaruh
}
```

### Sentiment Classification Algorithm:
```javascript
if (arah_sikap > 0 && level_aktivitas >= 3) return 'Pro-Aktif'
if (arah_sikap > 0 && level_aktivitas < 3) return 'Pro-Pasif'
if (arah_sikap < 0 && level_aktivitas >= 3) return 'Kontra-Aktif'
if (arah_sikap < 0 && level_aktivitas < 3) return 'Kontra-Pasif'
return 'Netral'
```

### Closeness Score Calculation:
```javascript
score = base_frequency_score (25 points) +
        same_university (15 points) +
        same_major (10 points) +
        same_organization (20 points) +
        family_relation (30 points)
Max score = 100
```

## Integration dengan Modul Lain

- **LARAP Module**: Stakeholder sentiment untuk land acquisition planning
- **Pembebasan Lahan**: Identify key stakeholders per parcel
- **Litigasi**: Track stakeholder involvement in disputes
- **Community Relations**: Overall sentiment monitoring

## Future Enhancements

1. **Sentiment Trend Analysis**: Track sentiment changes over time
2. **Influence Propagation Model**: Predict influence spread in network
3. **AI-Powered Sentiment Analysis**: Auto-classify from text input
4. **Integration with WhatsApp/SMS**: Auto-log interactions
5. **Export to PDF**: Generate stakeholder analysis report
6. **Interactive Network Graph**: Zoom, filter, search in network view
7. **Predictive Analytics**: Predict stakeholder behavior based on historical data

## Akses

**URL**: `/stakeholder-advanced`

**Navigation**: Sidebar → Stakeholder Management → Advanced Analytics

**Server Development**: 
```bash
npm run dev
# Access at http://localhost:5174
```

## Support

Untuk pertanyaan atau issues, silakan kontak tim development.
