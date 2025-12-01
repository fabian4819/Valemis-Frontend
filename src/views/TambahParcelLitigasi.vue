<template>
  <div>
    <div class="app-content-header">
      <div class="container-fluid">
        <div class="row">
          <div class="col-sm-6">
            <h3 class="mb-0">Tambah Parcel Litigasi</h3>
          </div>
          <div class="col-sm-6">
            <ol class="breadcrumb float-sm-end">
              <li class="breadcrumb-item"><router-link to="/">Home</router-link></li>
              <li class="breadcrumb-item"><router-link to="/litigasi">Litigasi</router-link></li>
              <li class="breadcrumb-item active" aria-current="page">Tambah Parcel</li>
            </ol>
          </div>
        </div>
      </div>
    </div>

    <div class="app-content">
      <div class="container-fluid">
        <div class="card mb-4">
          <div class="card-header">
            <h5 class="card-title">Digitasi Parcel Sengketa (Leaflet Draw)</h5>
          </div>
          <div class="card-body">
            <div id="map" style="height: 500px;"></div>
          </div>
        </div>

        <div class="card">
          <div class="card-header">
            <h5 class="card-title">Form Data Parcel</h5>
          </div>
          <div class="card-body">
            <form @submit.prevent="handleSubmit">
              <div class="row g-3">
                <div class="col-md-6">
                  <label for="parcelId" class="form-label">Parcel ID</label>
                  <input type="text" class="form-control" id="parcelId" required />
                </div>

                <div class="col-md-6">
                  <label for="claimId" class="form-label">Claim ID (Litigasi terkait)</label>
                  <select class="form-select" id="claimId" required>
                    <option value="">Pilih claim</option>
                    <option>CLM-001 - Ahmad Yani</option>
                    <option>CLM-002 - Siti Aminah</option>
                    <option>CLM-003 - Budi Santoso</option>
                  </select>
                </div>

                <div class="col-md-6">
                  <label for="luasParcel" class="form-label">Luas Parcel (m²)</label>
                  <input type="number" class="form-control" id="luasParcel" required />
                </div>

                <div class="col-md-6">
                  <label for="statusParcel" class="form-label">Status Parcel</label>
                  <select class="form-select" id="statusParcel" required>
                    <option value="">Pilih status</option>
                    <option>Disengketakan</option>
                    <option>Dalam Mediasi</option>
                    <option>Selesai</option>
                  </select>
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

                <div class="col-12">
                  <label for="keterangan" class="form-label">Keterangan</label>
                  <textarea class="form-control" id="keterangan" rows="3"></textarea>
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
      polygon: {},
      polyline: false,
      rectangle: {},
      circle: false,
      marker: false,
      circlemarker: false
    }
  })
  map.addControl(drawControl)

  map.on(L.Draw.Event.CREATED, (e: any) => {
    const layer = e.layer
    drawnItems.addLayer(layer)
    const geojson = layer.toGeoJSON()
    console.log('Parcel polygon created:', geojson)
    
    // Calculate area
    const area = (L.GeometryUtil as any).geodesicArea(layer.getLatLngs()[0])
    console.log('Area:', area.toFixed(2), 'm²')
  })
})

const handleSubmit = () => {
  alert('Data parcel berhasil disimpan')
  router.push('/litigasi')
}
</script>

<style scoped>
</style>
