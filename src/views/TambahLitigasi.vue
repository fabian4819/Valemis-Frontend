<template>
  <div>
    <div class="app-content-header">
      <div class="container-fluid">
        <div class="row">
          <div class="col-sm-6">
            <h3 class="mb-0">Tambah Litigasi</h3>
          </div>
          <div class="col-sm-6">
            <ol class="breadcrumb float-sm-end">
              <li class="breadcrumb-item"><router-link to="/">Home</router-link></li>
              <li class="breadcrumb-item"><router-link to="/litigasi">Litigasi</router-link></li>
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
            <h5 class="card-title">Peta Lokasi Sengketa</h5>
          </div>
          <div class="card-body">
            <div id="map" style="height: 400px;"></div>
          </div>
        </div>

        <div class="card">
          <div class="card-header">
            <h5 class="card-title">Form Data Litigasi</h5>
          </div>
          <div class="card-body">
            <form @submit.prevent="handleSubmit">
              <div class="row g-3">
                <div class="col-md-6">
                  <label for="claimId" class="form-label">Claim ID</label>
                  <input type="text" class="form-control" id="claimId" required />
                </div>

                <div class="col-md-6">
                  <label for="jenisClaim" class="form-label">Jenis Claim</label>
                  <select class="form-select" id="jenisClaim" required>
                    <option value="">Pilih jenis claim</option>
                    <option>Sengketa Batas Lahan</option>
                    <option>Sengketa Kepemilikan</option>
                    <option>Sengketa Kompensasi</option>
                    <option>Lainnya</option>
                  </select>
                </div>

                <div class="col-md-6">
                  <label for="namaPenggugat" class="form-label">Nama Penggugat</label>
                  <input type="text" class="form-control" id="namaPenggugat" required />
                </div>

                <div class="col-md-6">
                  <label for="nik" class="form-label">NIK</label>
                  <input type="text" class="form-control" id="nik" maxlength="16" required />
                </div>

                <div class="col-md-6">
                  <label for="nomorTelepon" class="form-label">Nomor Telepon</label>
                  <input type="tel" class="form-control" id="nomorTelepon" placeholder="0812xxxxxxx" />
                </div>

                <div class="col-md-6">
                  <label for="tanggalPengajuan" class="form-label">Tanggal Pengajuan</label>
                  <input type="date" class="form-control" id="tanggalPengajuan" required />
                </div>

                <div class="col-md-12">
                  <label for="alamat" class="form-label">Alamat Penggugat</label>
                  <textarea class="form-control" id="alamat" rows="2" required></textarea>
                </div>

                <div class="col-md-12">
                  <label for="deskripsi" class="form-label">Deskripsi Claim</label>
                  <textarea class="form-control" id="deskripsi" rows="4" required></textarea>
                </div>

                <div class="col-md-6">
                  <label for="status" class="form-label">Status</label>
                  <select class="form-select" id="status" required>
                    <option value="">Pilih status</option>
                    <option>Baru</option>
                    <option>Dalam Proses</option>
                    <option>Mediasi</option>
                    <option>Selesai</option>
                    <option>Ditolak</option>
                  </select>
                </div>

                <div class="col-md-6">
                  <label for="dokumen" class="form-label">Upload Dokumen Pendukung</label>
                  <input type="file" class="form-control" id="dokumen" multiple />
                </div>

                <div class="col-12">
                  <button type="submit" class="btn btn-primary">Simpan</button>
                  <router-link to="/litigasi" class="btn btn-secondary ms-2">Batal</router-link>
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
import { onMounted } from 'vue'
import { useRouter } from 'vue-router'
import L from 'leaflet'

const router = useRouter()

onMounted(() => {
  const map = L.map('map').setView([-2.5489, 118.0149], 13)

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; OpenStreetMap contributors'
  }).addTo(map)

  map.on('click', (e: any) => {
    L.marker([e.latlng.lat, e.latlng.lng]).addTo(map)
  })
})

const handleSubmit = () => {
  alert('Data litigasi berhasil disimpan')
  router.push('/litigasi')
}
</script>

<style scoped>
</style>
