<template>
  <div>
    <div class="app-content-header">
      <div class="container-fluid">
        <div class="row">
          <div class="col-sm-6">
            <h3 class="mb-0">Tambah Aset Inventori</h3>
          </div>
          <div class="col-sm-6">
            <ol class="breadcrumb float-sm-end">
              <li class="breadcrumb-item"><router-link to="/">Home</router-link></li>
              <li class="breadcrumb-item"><router-link to="/aset-inventori">Aset Inventori</router-link></li>
              <li class="breadcrumb-item active" aria-current="page">Tambah</li>
            </ol>
          </div>
        </div>
      </div>
    </div>

    <div class="app-content">
      <div class="container-fluid">
        <div class="card mb-4">
          <div class="card-header">
            <h5 class="card-title">Form Identitas Kepala Keluarga</h5>
          </div>
          <div class="card-body">
            <form @submit.prevent="handleSubmit">
              <div class="row g-3">
                <div class="col-md-4">
                  <label for="namaDepan" class="form-label">Nama Depan</label>
                  <input type="text" class="form-control" id="namaDepan" required />
                </div>
                <div class="col-md-4">
                  <label for="namaTengah" class="form-label">Nama Tengah</label>
                  <input type="text" class="form-control" id="namaTengah" />
                </div>
                <div class="col-md-4">
                  <label for="namaBelakang" class="form-label">Nama Belakang</label>
                  <input type="text" class="form-control" id="namaBelakang" required />
                </div>

                <div class="col-md-4">
                  <label for="namaAyah" class="form-label">Nama Ayah</label>
                  <input type="text" class="form-control" id="namaAyah" />
                </div>
                <div class="col-md-4">
                  <label for="namaKakek" class="form-label">Nama Kakek</label>
                  <input type="text" class="form-control" id="namaKakek" />
                </div>
                <div class="col-md-4">
                  <label for="namaPasangan" class="form-label">Nama Pasangan</label>
                  <input type="text" class="form-control" id="namaPasangan" />
                </div>

                <div class="col-md-4">
                  <label for="nomorTelepon" class="form-label">Nomor Telepon</label>
                  <input type="tel" class="form-control" id="nomorTelepon" placeholder="0812xxxxxxx" />
                </div>
                <div class="col-md-4">
                  <label for="nik" class="form-label">NIK</label>
                  <input type="text" class="form-control" id="nik" maxlength="16" placeholder="16 digit NIK" />
                </div>

                <div class="col-md-4">
                  <label for="desa" class="form-label">Desa</label>
                  <input type="text" class="form-control" id="desa" />
                </div>
                <div class="col-md-4">
                  <label for="kecamatan" class="form-label">Kecamatan</label>
                  <input type="text" class="form-control" id="kecamatan" />
                </div>
                <div class="col-md-4">
                  <label for="kabupaten" class="form-label">Kabupaten</label>
                  <input type="text" class="form-control" id="kabupaten" />
                </div>
                <div class="col-md-4">
                  <label for="provinsi" class="form-label">Provinsi</label>
                  <input type="text" class="form-control" id="provinsi" />
                </div>

                <div class="col-md-6">
                  <label for="namaResponden" class="form-label">Nama Responden (jika berbeda dengan Kepala Keluarga)</label>
                  <input type="text" class="form-control" id="namaResponden" />
                </div>
                <div class="col-md-6">
                  <label for="hubunganResponden" class="form-label">Hubungan Responden dengan Kepala Keluarga</label>
                  <select class="form-select" id="hubunganResponden">
                    <option value="" selected>Pilih hubungan</option>
                    <option>Pasangan</option>
                    <option>Anak Laki-laki</option>
                    <option>Anak Perempuan</option>
                    <option>Menantu Laki-laki</option>
                    <option>Menantu Perempuan</option>
                    <option>Cucu Laki-laki</option>
                    <option>Cucu Perempuan</option>
                    <option>Ayah</option>
                    <option>Ibu</option>
                    <option>Mertua</option>
                    <option>Saudara Laki-laki</option>
                    <option>Saudara Perempuan</option>
                    <option>Ipar Laki-laki</option>
                    <option>Ipar Perempuan</option>
                    <option>Kerabat lain</option>
                    <option>Sepupu</option>
                    <option>Bukan kerabat</option>
                  </select>
                </div>

                <div class="col-12">
                  <button type="submit" class="btn btn-primary">Simpan</button>
                  <router-link to="/aset-inventori" class="btn btn-secondary ms-2">Batal</router-link>
                </div>
              </div>
            </form>
          </div>
        </div>

        <div class="card mb-4">
          <div class="card-header">
            <h5 class="card-title">A. Identifikasi Rumah Tangga dan PAP</h5>
          </div>
          <div class="card-body">
            <form @submit.prevent="handleSubmit2">
              <div class="row g-3">
                <div class="col-md-4">
                  <label for="kodeEnumerator" class="form-label">1. Kode Enumerator</label>
                  <input type="text" class="form-control" id="kodeEnumerator" required />
                </div>

                <div class="col-md-4">
                  <label for="tanggal" class="form-label">3. Tanggal (DD/MM/YYYY)</label>
                  <input type="date" class="form-control" id="tanggal" required />
                </div>

                <div class="col-md-4">
                  <label for="kodeFoto" class="form-label">4. Kode Foto Survei</label>
                  <input type="text" class="form-control" id="kodeFoto" />
                </div>

                <div class="col-md-6">
                  <label for="idUnik" class="form-label">5. ID Unik (ID Entitas Terdampak) Dalam Rumah Tangga</label>
                  <input type="text" class="form-control" id="idUnik" required />
                </div>

                <div class="col-md-6">
                  <label for="koordinat" class="form-label">6. Koordinat</label>
                  <input type="text" class="form-control" id="koordinat" placeholder="Contoh: -6.200000, 106.816666" />
                </div>

                <div class="col-12">
                  <button type="submit" class="btn btn-primary">Simpan</button>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useRouter } from 'vue-router'

const router = useRouter()

const handleSubmit = () => {
  alert('Data berhasil disimpan')
  router.push('/aset-inventori')
}

const handleSubmit2 = () => {
  alert('Data berhasil disimpan')
}
</script>

<style scoped>
</style>
