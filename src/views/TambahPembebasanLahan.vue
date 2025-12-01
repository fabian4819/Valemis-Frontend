<template>
  <div>
    <div class="app-content-header">
      <div class="container-fluid">
        <div class="row">
          <div class="col-sm-6">
            <h3 class="mb-0">Tambah Pembebasan Lahan</h3>
          </div>
          <div class="col-sm-6">
            <ol class="breadcrumb float-sm-end">
              <li class="breadcrumb-item"><router-link to="/">Home</router-link></li>
              <li class="breadcrumb-item"><router-link to="/pembebasan-lahan">Pembebasan Lahan</router-link></li>
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
            <h5 class="card-title">Digitasi Lahan (Leaflet Draw)</h5>
          </div>
          <div class="card-body">
            <div id="map" style="height: 500px;"></div>
          </div>
        </div>

        <div class="card mb-4">
          <div class="card-header">
            <h5 class="card-title">Form Data Lahan</h5>
          </div>
          <div class="card-body">
            <form @submit.prevent="handleSubmit">
              <div class="row g-3">
                <div class="col-md-6">
                  <label for="parcelId" class="form-label">Parcel ID</label>
                  <input type="text" class="form-control" id="parcelId" required />
                </div>

                <div class="col-md-6">
                  <label for="luasLahan" class="form-label">Luas Lahan (m²)</label>
                  <input type="number" class="form-control" id="luasLahan" required />
                </div>

                <div class="col-md-6">
                  <label for="namaKepalaKeluarga" class="form-label">Nama Kepala Keluarga</label>
                  <input type="text" class="form-control" id="namaKepalaKeluarga" required />
                </div>

                <div class="col-md-6">
                  <label for="alamat" class="form-label">Alamat</label>
                  <input type="text" class="form-control" id="alamat" required />
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
                  <label for="statusPembebasan" class="form-label">Status Pembebasan</label>
                  <select class="form-select" id="statusPembebasan" required>
                    <option value="">Pilih status</option>
                    <option>Belum Dibebaskan</option>
                    <option>Dalam Proses</option>
                    <option>Sudah Dibebaskan</option>
                  </select>
                </div>

                <div class="col-md-6">
                  <label for="tanggalPembebasan" class="form-label">Tanggal Pembebasan</label>
                  <input type="date" class="form-control" id="tanggalPembebasan" />
                </div>

                <div class="col-12">
                  <label for="catatan" class="form-label">Catatan</label>
                  <textarea class="form-control" id="catatan" rows="3"></textarea>
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
import { onMounted } from 'vue'
import { useRouter } from 'vue-router'
import L from 'leaflet'
import 'leaflet-draw'

const router = useRouter()

onMounted(() => {
  const map = L.map('map').setView([-2.5489, 118.0149], 5)

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; OpenStreetMap contributors'
  }).addTo(map)

  const drawnItems = new L.FeatureGroup()
  map.addLayer(drawnItems)

  const drawControl = new L.Control.Draw({
    edit: {
      featureGroup: drawnItems
    },
    draw: {
      polygon: true,
      polyline: false,
      rectangle: true,
      circle: false,
      marker: false,
      circlemarker: false
    }
  })
  map.addControl(drawControl)

  map.on(L.Draw.Event.CREATED, (e: any) => {
    const layer = e.layer
    drawnItems.addLayer(layer)
    console.log('Polygon created:', layer.toGeoJSON())
  })
})

const handleSubmit = () => {
  alert('Data berhasil disimpan')
  router.push('/pembebasan-lahan')
}
</script>

<style scoped>
</style>
