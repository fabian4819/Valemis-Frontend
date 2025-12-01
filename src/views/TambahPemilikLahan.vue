<template>
  <div>
    <div class="app-content-header">
      <div class="container-fluid">
        <div class="row">
          <div class="col-sm-6">
            <h3 class="mb-0">Tambah Pemilik Lahan</h3>
          </div>
          <div class="col-sm-6">
            <ol class="breadcrumb float-sm-end">
              <li class="breadcrumb-item"><router-link to="/">Home</router-link></li>
              <li class="breadcrumb-item"><router-link to="/pembebasan-lahan">Pembebasan Lahan</router-link></li>
              <li class="breadcrumb-item active" aria-current="page">Tambah Pemilik</li>
            </ol>
          </div>
        </div>
      </div>
    </div>

    <div class="app-content">
      <div class="container-fluid">
        <div class="card">
          <div class="card-header">
            <h5 class="card-title">Form Data Pemilik Lahan</h5>
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

                <div class="col-md-6">
                  <label for="nik" class="form-label">NIK</label>
                  <input type="text" class="form-control" id="nik" maxlength="16" placeholder="16 digit NIK" required />
                </div>

                <div class="col-md-6">
                  <label for="nomorTelepon" class="form-label">Nomor Telepon</label>
                  <input type="tel" class="form-control" id="nomorTelepon" placeholder="0812xxxxxxx" />
                </div>

                <div class="col-md-12">
                  <label for="alamat" class="form-label">Alamat</label>
                  <textarea class="form-control" id="alamat" rows="2" required></textarea>
                </div>

                <div class="col-md-4">
                  <label for="desa" class="form-label">Desa</label>
                  <input type="text" class="form-control" id="desa" required />
                </div>

                <div class="col-md-4">
                  <label for="kecamatan" class="form-label">Kecamatan</label>
                  <input type="text" class="form-control" id="kecamatan" required />
                </div>

                <div class="col-md-4">
                  <label for="kabupaten" class="form-label">Kabupaten</label>
                  <input type="text" class="form-control" id="kabupaten" required />
                </div>

                <div class="col-md-6">
                  <label for="statusKepemilikan" class="form-label">Status Kepemilikan</label>
                  <select class="form-select" id="statusKepemilikan" required>
                    <option value="">Pilih status</option>
                    <option>Kepala Keluarga</option>
                    <option>Pasangan</option>
                    <option>Anak</option>
                    <option>Ahli Waris</option>
                    <option>Lainnya</option>
                  </select>
                </div>

                <div class="col-md-6">
                  <label for="hubunganKeluarga" class="form-label">Hubungan Keluarga</label>
                  <input type="text" class="form-control" id="hubunganKeluarga" />
                </div>

                <div class="col-12">
                  <button type="submit" class="btn btn-primary">Simpan</button>
                  <router-link to="/pembebasan-lahan" class="btn btn-secondary ms-2">Batal</router-link>
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
  alert('Data pemilik lahan berhasil disimpan')
  router.push('/pembebasan-lahan')
}
</script>

<style scoped>
</style>
