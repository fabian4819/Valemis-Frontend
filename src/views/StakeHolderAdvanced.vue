<template>
  <div>
    <div class="app-content-header">
      <div class="container-fluid">
        <div class="row">
          <div class="col-sm-6">
            <h3 class="mb-0">Stakeholder Management System</h3>
          </div>
          <div class="col-sm-6">
            <ol class="breadcrumb float-sm-end">
              <li class="breadcrumb-item"><router-link to="/">Home</router-link></li>
              <li class="breadcrumb-item active">Stakeholder Management</li>
            </ol>
          </div>
        </div>
      </div>
    </div>

    <div class="app-content">
      <div class="container-fluid">
        <!-- Dashboard Cards -->
        <div class="row mb-4">
          <div class="col-lg-3 col-6">
            <div class="small-box bg-success">
              <div class="inner">
                <h3>{{ stats.proAktif }}</h3>
                <p>Pro - Aktif</p>
              </div>
              <div class="icon">
                <i class="bi bi-hand-thumbs-up-fill"></i>
              </div>
            </div>
          </div>
          <div class="col-lg-3 col-6">
            <div class="small-box bg-info">
              <div class="inner">
                <h3>{{ stats.proPasif }}</h3>
                <p>Pro - Pasif</p>
              </div>
              <div class="icon">
                <i class="bi bi-hand-thumbs-up"></i>
              </div>
            </div>
          </div>
          <div class="col-lg-3 col-6">
            <div class="small-box bg-warning">
              <div class="inner">
                <h3>{{ stats.kontraAktif }}</h3>
                <p>Kontra - Aktif</p>
              </div>
              <div class="icon">
                <i class="bi bi-hand-thumbs-down-fill"></i>
              </div>
            </div>
          </div>
          <div class="col-lg-3 col-6">
            <div class="small-box bg-danger">
              <div class="inner">
                <h3>{{ stats.kontraPasif }}</h3>
                <p>Kontra - Pasif</p>
              </div>
              <div class="icon">
                <i class="bi bi-hand-thumbs-down"></i>
              </div>
            </div>
          </div>
        </div>

        <!-- Stakeholder Network Visualization -->
        <div class="card mb-4">
          <div class="card-header">
            <h5 class="mb-0">
              <i class="bi bi-diagram-3"></i> Network Visualization & Sentiment Analysis
            </h5>
          </div>
          <div class="card-body">
            <div class="row">
              <div class="col-md-8">
                <canvas ref="networkCanvas" width="800" height="450"></canvas>
              </div>
              <div class="col-md-4">
                <h6>Legend:</h6>
                <ul class="list-unstyled">
                  <li><span class="badge bg-success">●</span> Pro Aktif (Arah: +, Level: 3-4)</li>
                  <li><span class="badge bg-info">●</span> Pro Pasif (Arah: +, Level: 1-2)</li>
                  <li><span class="badge bg-warning">●</span> Kontra Aktif (Arah: -, Level: 3-4)</li>
                  <li><span class="badge bg-danger">●</span> Kontra Pasif (Arah: -, Level: 1-2)</li>
                  <li><span class="badge bg-secondary">●</span> Netral</li>
                </ul>
                <hr>
                <h6>Connection Strength:</h6>
                <ul class="list-unstyled">
                  <li><span style="border-bottom: 3px solid #333; display: inline-block; width: 30px;"></span> Strong (Score > 70)</li>
                  <li><span style="border-bottom: 2px solid #666; display: inline-block; width: 30px;"></span> Medium (Score 40-70)</li>
                  <li><span style="border-bottom: 1px solid #999; display: inline-block; width: 30px;"></span> Weak (Score < 40)</li>
                </ul>
              </div>
            </div>
          </div>
        </div>

        <!-- Main Content Tabs -->
        <div class="card">
          <div class="card-header">
            <ul class="nav nav-tabs card-header-tabs" role="tablist">
              <li class="nav-item">
                <a 
                  class="nav-link" 
                  :class="{ active: activeTab === 'master' }"
                  @click="activeTab = 'master'"
                  href="javascript:void(0)"
                >
                  <i class="bi bi-person-badge"></i> Master Stakeholder
                </a>
              </li>
              <li class="nav-item">
                <a 
                  class="nav-link" 
                  :class="{ active: activeTab === 'background' }"
                  @click="activeTab = 'background'"
                  href="javascript:void(0)"
                >
                  <i class="bi bi-book"></i> Latar Belakang
                </a>
              </li>
              <li class="nav-item">
                <a 
                  class="nav-link" 
                  :class="{ active: activeTab === 'isu' }"
                  @click="activeTab = 'isu'"
                  href="javascript:void(0)"
                >
                  <i class="bi bi-flag"></i> Isu/Project
                </a>
              </li>
              <li class="nav-item">
                <a 
                  class="nav-link" 
                  :class="{ active: activeTab === 'interaksi' }"
                  @click="activeTab = 'interaksi'"
                  href="javascript:void(0)"
                >
                  <i class="bi bi-chat-dots"></i> Log Interaksi
                </a>
              </li>
              <li class="nav-item">
                <a 
                  class="nav-link" 
                  :class="{ active: activeTab === 'network' }"
                  @click="activeTab = 'network'"
                  href="javascript:void(0)"
                >
                  <i class="bi bi-diagram-2"></i> Network/Relasi
                </a>
              </li>
              <li class="nav-item">
                <a 
                  class="nav-link" 
                  :class="{ active: activeTab === 'evidence' }"
                  @click="activeTab = 'evidence'"
                  href="javascript:void(0)"
                >
                  <i class="bi bi-file-earmark-text"></i> Dokumen/Bukti
                </a>
              </li>
            </ul>
          </div>
          <div class="card-body">
            <!-- Tab 1: Master Stakeholder -->
            <div v-show="activeTab === 'master'">
              <div class="d-flex justify-content-between align-items-center mb-3">
                <h5>Daftar Stakeholder</h5>
                <button class="btn btn-primary" @click="openModalAdd('master')">
                  <i class="bi bi-plus-circle"></i> Tambah Stakeholder
                </button>
              </div>
              
              <div class="table-responsive">
                <table ref="masterTable" class="table table-bordered table-hover table-sm">
                  <thead class="table-light">
                    <tr>
                      <th>ID</th>
                      <th>Nama</th>
                      <th>Jenis</th>
                      <th>Peran</th>
                      <th>Pengaruh</th>
                      <th>Kepentingan</th>
                      <th>Klasifikasi</th>
                      <th>Aksi</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="sh in stakeholders" :key="sh.id">
                      <td>{{ sh.stakeholder_id }}</td>
                      <td>
                        <strong>{{ sh.nama_lengkap }}</strong><br>
                        <small class="text-muted">{{ sh.nama_panggilan }}</small>
                      </td>
                      <td>{{ sh.jenis_stakeholder }}</td>
                      <td>{{ sh.peran_di_proyek }}</td>
                      <td>
                        <span class="badge" :class="getBadgeInfluence(sh.level_pengaruh)">
                          {{ sh.level_pengaruh }}/5
                        </span>
                      </td>
                      <td>
                        <span class="badge" :class="getBadgeInterest(sh.level_kepentingan)">
                          {{ sh.level_kepentingan }}/5
                        </span>
                      </td>
                      <td>
                        <span class="badge" :class="getBadgeSentimen(sh.klasifikasi_sikap)">
                          {{ sh.klasifikasi_sikap }}
                        </span>
                      </td>
                      <td>
                        <div class="btn-group btn-group-sm">
                          <button class="btn btn-info" @click="viewDetail(sh)" title="Detail">
                            <i class="bi bi-eye"></i>
                          </button>
                          <button class="btn btn-warning" @click="editStakeholder(sh)" title="Edit">
                            <i class="bi bi-pencil"></i>
                          </button>
                          <button class="btn btn-danger" @click="deleteStakeholder(sh.id)" title="Hapus">
                            <i class="bi bi-trash"></i>
                          </button>
                        </div>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>

            <!-- Tab 2: Latar Belakang & Atribut Relasi -->
            <div v-show="activeTab === 'background'">
              <div class="d-flex justify-content-between align-items-center mb-3">
                <h5>Latar Belakang Stakeholder</h5>
                <button class="btn btn-primary" @click="openModalAdd('background')">
                  <i class="bi bi-plus-circle"></i> Tambah Data Background
                </button>
              </div>

              <div class="table-responsive">
                <table class="table table-bordered table-hover table-sm">
                  <thead class="table-light">
                    <tr>
                      <th>Stakeholder</th>
                      <th>Pendidikan</th>
                      <th>Pekerjaan</th>
                      <th>Organisasi</th>
                      <th>Kekerabatan</th>
                      <th>Lokasi</th>
                      <th>Aksi</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="bg in backgrounds" :key="bg.id">
                      <td><strong>{{ bg.stakeholder_nama }}</strong></td>
                      <td>
                        {{ bg.jenjang_pendidikan }}<br>
                        <small class="text-muted">{{ bg.universitas }} - {{ bg.jurusan }}</small><br>
                        <small class="text-muted">{{ bg.tahun_masuk }} - {{ bg.tahun_lulus }}</small>
                      </td>
                      <td>
                        {{ bg.pekerjaan_utama }}<br>
                        <small class="text-muted">{{ bg.instansi }}</small>
                      </td>
                      <td>
                        <span v-for="(org, idx) in bg.organisasi" :key="idx" class="badge bg-secondary me-1">
                          {{ org }}
                        </span>
                      </td>
                      <td>
                        <span v-if="bg.status_kekerabatan" class="badge bg-info">
                          {{ bg.detail_kekerabatan }}
                        </span>
                        <span v-else class="text-muted">-</span>
                      </td>
                      <td>{{ bg.dusun_rt_rw }}</td>
                      <td>
                        <div class="btn-group btn-group-sm">
                          <button class="btn btn-warning" @click="editBackground(bg)">
                            <i class="bi bi-pencil"></i>
                          </button>
                          <button class="btn btn-danger" @click="deleteBackground(bg.id)">
                            <i class="bi bi-trash"></i>
                          </button>
                        </div>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>

            <!-- Tab 3: Isu/Project per Stakeholder -->
            <div v-show="activeTab === 'isu'">
              <div class="d-flex justify-content-between align-items-center mb-3">
                <h5>Isu & Project Stakeholder</h5>
                <button class="btn btn-primary" @click="openModalAdd('isu')">
                  <i class="bi bi-plus-circle"></i> Tambah Data Isu
                </button>
              </div>

              <div class="table-responsive">
                <table class="table table-bordered table-hover table-sm">
                  <thead class="table-light">
                    <tr>
                      <th>Stakeholder</th>
                      <th>Project/Isu</th>
                      <th>Jenis Dampak</th>
                      <th>Besaran Dampak</th>
                      <th>Persepsi</th>
                      <th>Keberatan Utama</th>
                      <th>Aksi</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="isu in issuData" :key="isu.id">
                      <td><strong>{{ isu.stakeholder_nama }}</strong></td>
                      <td>
                        {{ isu.nama_project }}<br>
                        <small class="text-muted">{{ isu.isu_spesifik }}</small>
                      </td>
                      <td>
                        <span v-for="(dampak, idx) in isu.jenis_dampak" :key="idx" class="badge bg-warning text-dark me-1">
                          {{ dampak }}
                        </span>
                      </td>
                      <td>
                        <div class="progress" style="height: 20px;">
                          <div 
                            class="progress-bar" 
                            :class="getProgressClass(isu.besaran_dampak)"
                            :style="{ width: (isu.besaran_dampak * 20) + '%' }"
                          >
                            {{ isu.besaran_dampak }}/5
                          </div>
                        </div>
                      </td>
                      <td>
                        <span class="badge" :class="getBadgePersepsi(isu.persepsi_umum)">
                          {{ isu.persepsi_umum }}
                        </span>
                      </td>
                      <td>{{ isu.topik_keberatan || '-' }}</td>
                      <td>
                        <div class="btn-group btn-group-sm">
                          <button class="btn btn-warning" @click="editIsu(isu)">
                            <i class="bi bi-pencil"></i>
                          </button>
                          <button class="btn btn-danger" @click="deleteIsu(isu.id)">
                            <i class="bi bi-trash"></i>
                          </button>
                        </div>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>

            <!-- Tab 4: Log Interaksi & Sentimen -->
            <div v-show="activeTab === 'interaksi'">
              <div class="d-flex justify-content-between align-items-center mb-3">
                <h5>Log Interaksi & Sentimen</h5>
                <button class="btn btn-primary" @click="openModalAdd('interaksi')">
                  <i class="bi bi-plus-circle"></i> Tambah Log Interaksi
                </button>
              </div>

              <div class="table-responsive">
                <table class="table table-bordered table-hover table-sm">
                  <thead class="table-light">
                    <tr>
                      <th>Tanggal</th>
                      <th>Stakeholder</th>
                      <th>Jenis Interaksi</th>
                      <th>Peran</th>
                      <th>Pernyataan</th>
                      <th>Nada</th>
                      <th>Arah Sikap</th>
                      <th>Aktivitas</th>
                      <th>Aksi</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="log in interactionLogs" :key="log.id">
                      <td>
                        {{ formatDate(log.tanggal) }}<br>
                        <small class="text-muted">{{ log.lokasi }}</small>
                      </td>
                      <td><strong>{{ log.stakeholder_nama }}</strong></td>
                      <td>{{ log.jenis_interaksi }}</td>
                      <td>
                        <span class="badge bg-info">{{ log.peran_dalam_pertemuan }}</span>
                      </td>
                      <td>
                        <div style="max-width: 300px;">
                          <small>{{ log.ringkasan_pernyataan }}</small><br>
                          <span class="badge bg-secondary">{{ log.kategori_pernyataan }}</span>
                        </div>
                      </td>
                      <td>
                        <span class="badge" :class="getBadgeNada(log.nada)">
                          {{ log.nada }}
                        </span>
                      </td>
                      <td>
                        <span class="badge" :class="getBadgeArahSikap(log.arah_sikap)">
                          {{ getArahSikapLabel(log.arah_sikap) }}
                        </span>
                      </td>
                      <td>
                        <span class="badge" :class="getBadgeAktivitas(log.level_aktivitas)">
                          Level {{ log.level_aktivitas }}
                        </span>
                      </td>
                      <td>
                        <div class="btn-group btn-group-sm">
                          <button class="btn btn-info" @click="viewInteraksi(log)">
                            <i class="bi bi-eye"></i>
                          </button>
                          <button class="btn btn-warning" @click="editInteraksi(log)">
                            <i class="bi bi-pencil"></i>
                          </button>
                          <button class="btn btn-danger" @click="deleteInteraksi(log.id)">
                            <i class="bi bi-trash"></i>
                          </button>
                        </div>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>

            <!-- Tab 5: Network/Relasi -->
            <div v-show="activeTab === 'network'">
              <div class="d-flex justify-content-between align-items-center mb-3">
                <h5>Network & Relasi Stakeholder</h5>
                <button class="btn btn-primary" @click="openModalAdd('network')">
                  <i class="bi bi-plus-circle"></i> Tambah Relasi
                </button>
              </div>

              <div class="table-responsive">
                <table class="table table-bordered table-hover table-sm">
                  <thead class="table-light">
                    <tr>
                      <th>Stakeholder A</th>
                      <th>Relasi</th>
                      <th>Stakeholder B</th>
                      <th>Jenis Relasi</th>
                      <th>Frekuensi</th>
                      <th>Intensitas</th>
                      <th>Shared Attributes</th>
                      <th>Skor Kedekatan</th>
                      <th>Aksi</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="rel in relations" :key="rel.id">
                      <td><strong>{{ rel.stakeholder_a_nama }}</strong></td>
                      <td class="text-center">
                        <i class="bi bi-arrow-left-right"></i>
                      </td>
                      <td><strong>{{ rel.stakeholder_b_nama }}</strong></td>
                      <td>
                        <span class="badge bg-primary">{{ rel.jenis_relasi }}</span>
                      </td>
                      <td>{{ rel.frekuensi_interaksi }}</td>
                      <td>
                        <div class="progress" style="height: 20px;">
                          <div 
                            class="progress-bar bg-info" 
                            :style="{ width: (rel.intensitas_kedekatan * 20) + '%' }"
                          >
                            {{ rel.intensitas_kedekatan }}/5
                          </div>
                        </div>
                      </td>
                      <td>
                        <span v-if="rel.satu_universitas" class="badge bg-secondary me-1">Univ</span>
                        <span v-if="rel.satu_jurusan" class="badge bg-secondary me-1">Jurusan</span>
                        <span v-if="rel.satu_organisasi" class="badge bg-secondary me-1">Orgs</span>
                        <span v-if="rel.hubungan_kekerabatan" class="badge bg-secondary me-1">Keluarga</span>
                      </td>
                      <td>
                        <span class="badge" :class="getBadgeKedekatan(rel.skor_kedekatan_total)">
                          {{ rel.skor_kedekatan_total }}/100
                        </span>
                      </td>
                      <td>
                        <div class="btn-group btn-group-sm">
                          <button class="btn btn-warning" @click="editRelation(rel)">
                            <i class="bi bi-pencil"></i>
                          </button>
                          <button class="btn btn-danger" @click="deleteRelation(rel.id)">
                            <i class="bi bi-trash"></i>
                          </button>
                        </div>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>

            <!-- Tab 6: Evidence/Dokumen -->
            <div v-show="activeTab === 'evidence'">
              <div class="d-flex justify-content-between align-items-center mb-3">
                <h5>Dokumen & Bukti Pendukung</h5>
                <button class="btn btn-primary" @click="openModalAdd('evidence')">
                  <i class="bi bi-plus-circle"></i> Upload Dokumen
                </button>
              </div>

              <div class="row">
                <div class="col-md-4" v-for="doc in evidences" :key="doc.id">
                  <div class="card mb-3">
                    <div class="card-body">
                      <div class="d-flex justify-content-between align-items-start mb-2">
                        <h6 class="mb-0">
                          <i class="bi" :class="getFileIcon(doc.jenis_bukti)"></i>
                          {{ doc.jenis_bukti }}
                        </h6>
                        <div class="btn-group btn-group-sm">
                          <button class="btn btn-outline-primary" @click="viewDocument(doc)">
                            <i class="bi bi-eye"></i>
                          </button>
                          <button class="btn btn-outline-danger" @click="deleteEvidence(doc.id)">
                            <i class="bi bi-trash"></i>
                          </button>
                        </div>
                      </div>
                      <p class="mb-2"><small>{{ doc.deskripsi_pendek }}</small></p>
                      <div class="mb-2">
                        <small class="text-muted">
                          <i class="bi bi-person"></i> {{ doc.stakeholder_nama || 'Multiple' }}<br>
                          <i class="bi bi-calendar"></i> {{ formatDate(doc.tanggal_dokumen) }}<br>
                          <i class="bi bi-person-badge"></i> {{ doc.penanggung_jawab }}
                        </small>
                      </div>
                      <button class="btn btn-sm btn-outline-secondary w-100" @click="downloadDocument(doc)">
                        <i class="bi bi-download"></i> Download
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal for Forms (will be populated based on activeModal type) -->
    <div class="modal fade" :class="{ show: showModal, 'd-block': showModal }" v-if="showModal" tabindex="-1">
      <div class="modal-dialog modal-lg">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">{{ modalTitle }}</h5>
            <button type="button" class="btn-close" @click="closeModal"></button>
          </div>
          <div class="modal-body">
            <!-- Form Master Stakeholder -->
            <div v-if="modalType === 'master'">
              <div class="row">
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Nama Lengkap *</label>
                    <input type="text" class="form-control" v-model="masterForm.nama">
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">NIK *</label>
                    <input type="text" class="form-control" v-model="masterForm.nik">
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Role/Peran *</label>
                    <select class="form-select" v-model="masterForm.role">
                      <option value="">Pilih Role</option>
                      <option value="Pemilik Lahan">Pemilik Lahan</option>
                      <option value="Tokoh Adat">Tokoh Adat</option>
                      <option value="Tokoh Agama">Tokoh Agama</option>
                      <option value="Kepala Desa">Kepala Desa</option>
                      <option value="Ketua RT">Ketua RT</option>
                      <option value="Petani">Petani</option>
                      <option value="Pedagang">Pedagang</option>
                      <option value="LSM">Aktivis LSM</option>
                    </select>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Desa *</label>
                    <input type="text" class="form-control" v-model="masterForm.desa">
                  </div>
                </div>
                <div class="col-md-4">
                  <div class="mb-3">
                    <label class="form-label">Telepon</label>
                    <input type="text" class="form-control" v-model="masterForm.telepon">
                  </div>
                </div>
                <div class="col-md-4">
                  <div class="mb-3">
                    <label class="form-label">Level Pengaruh (1-5) *</label>
                    <input type="number" class="form-control" v-model.number="masterForm.level_pengaruh" min="1" max="5">
                  </div>
                </div>
                <div class="col-md-4">
                  <div class="mb-3">
                    <label class="form-label">Level Kepentingan (1-5) *</label>
                    <input type="number" class="form-control" v-model.number="masterForm.level_kepentingan" min="1" max="5">
                  </div>
                </div>
                <div class="col-12">
                  <div class="mb-3">
                    <label class="form-label">Catatan</label>
                    <textarea class="form-control" rows="3" v-model="masterForm.catatan"></textarea>
                  </div>
                </div>
              </div>
            </div>

            <!-- Form Background -->
            <div v-if="modalType === 'background'">
              <div class="row">
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Pilih Stakeholder *</label>
                    <select class="form-select" v-model="backgroundForm.stakeholder_id">
                      <option value="">Pilih Stakeholder</option>
                      <option v-for="sh in stakeholders" :key="sh.id" :value="sh.id">{{ sh.nama_lengkap }}</option>
                    </select>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Pendidikan Terakhir</label>
                    <select class="form-select" v-model="backgroundForm.jenjang_pendidikan">
                      <option value="SD">SD</option>
                      <option value="SMP">SMP</option>
                      <option value="SMA">SMA</option>
                      <option value="D3">D3</option>
                      <option value="S1">S1</option>
                      <option value="S2">S2</option>
                      <option value="S3">S3</option>
                    </select>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Universitas</label>
                    <input type="text" class="form-control" v-model="backgroundForm.universitas">
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Jurusan</label>
                    <input type="text" class="form-control" v-model="backgroundForm.jurusan">
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Pekerjaan Utama</label>
                    <input type="text" class="form-control" v-model="backgroundForm.pekerjaan_utama">
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Instansi</label>
                    <input type="text" class="form-control" v-model="backgroundForm.instansi">
                  </div>
                </div>
                <div class="col-md-12">
                  <div class="mb-3">
                    <label class="form-label">Kekerabatan dengan Stakeholder Lain</label>
                    <input type="text" class="form-control" v-model="backgroundForm.detail_kekerabatan" placeholder="Contoh: Sepupu dari Budi Santoso">
                  </div>
                </div>
              </div>
            </div>

            <!-- Form Isu -->
            <div v-if="modalType === 'isu'">
              <div class="row">
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Pilih Stakeholder *</label>
                    <select class="form-select" v-model="isuForm.stakeholder_id">
                      <option value="">Pilih Stakeholder</option>
                      <option v-for="sh in stakeholders" :key="sh.id" :value="sh.id">{{ sh.nama_lengkap }}</option>
                    </select>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Nama Project/Isu *</label>
                    <input type="text" class="form-control" v-model="isuForm.nama_project">
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Jenis Dampak *</label>
                    <select class="form-select" v-model="isuForm.jenis_dampak">
                      <option value="Ekonomi">Ekonomi</option>
                      <option value="Sosial">Sosial</option>
                      <option value="Lingkungan">Lingkungan</option>
                      <option value="Aset Lahan">Aset Lahan</option>
                      <option value="Infrastruktur">Infrastruktur</option>
                    </select>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Persepsi Umum *</label>
                    <select class="form-select" v-model="isuForm.persepsi_awal">
                      <option value="Positif">Positif</option>
                      <option value="Netral">Netral</option>
                      <option value="Negatif">Negatif</option>
                    </select>
                  </div>
                </div>
                <div class="col-12">
                  <div class="mb-3">
                    <label class="form-label">Topik Keberatan</label>
                    <textarea class="form-control" rows="3" v-model="isuForm.topik_keberatan"></textarea>
                  </div>
                </div>
              </div>
            </div>

            <!-- Form Interaksi -->
            <div v-if="modalType === 'interaksi'">
              <div class="row">
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Pilih Stakeholder *</label>
                    <select class="form-select" v-model="interaksiForm.stakeholder_id">
                      <option value="">Pilih Stakeholder</option>
                      <option v-for="sh in stakeholders" :key="sh.id" :value="sh.id">{{ sh.nama_lengkap }}</option>
                    </select>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Tanggal Interaksi *</label>
                    <input type="date" class="form-control" v-model="interaksiForm.tanggal_interaksi">
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Jenis Interaksi *</label>
                    <select class="form-select" v-model="interaksiForm.jenis_interaksi">
                      <option value="Rapat Desa">Rapat Desa</option>
                      <option value="Kunjungan Tim">Kunjungan Tim</option>
                      <option value="Sosialisasi">Sosialisasi</option>
                      <option value="Negosiasi">Negosiasi</option>
                      <option value="Diskusi">Diskusi</option>
                    </select>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Topik Pembahasan *</label>
                    <input type="text" class="form-control" v-model="interaksiForm.topik">
                  </div>
                </div>
                <div class="col-12">
                  <div class="mb-3">
                    <label class="form-label">Perilaku yang Diamati</label>
                    <textarea class="form-control" rows="2" v-model="interaksiForm.perilaku_observed"></textarea>
                  </div>
                </div>
                <div class="col-12">
                  <div class="mb-3">
                    <label class="form-label">Pernyataan Kunci</label>
                    <textarea class="form-control" rows="3" v-model="interaksiForm.pernyataan_kunci"></textarea>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Arah Sikap (-2 s/d +2) *</label>
                    <select class="form-select" v-model.number="interaksiForm.arah_sikap">
                      <option :value="-2">-2 (Sangat Kontra)</option>
                      <option :value="-1">-1 (Kontra)</option>
                      <option :value="0">0 (Netral)</option>
                      <option :value="1">+1 (Pro)</option>
                      <option :value="2">+2 (Sangat Pro)</option>
                    </select>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Level Aktivitas (1-4) *</label>
                    <select class="form-select" v-model.number="interaksiForm.level_aktivitas">
                      <option :value="1">1 (Pasif - Hanya dengar)</option>
                      <option :value="2">2 (Cukup - Sesekali bicara)</option>
                      <option :value="3">3 (Aktif - Sering bicara)</option>
                      <option :value="4">4 (Sangat Aktif - Dominan)</option>
                    </select>
                  </div>
                </div>
                <div class="col-12">
                  <div class="alert alert-info">
                    <strong>Klasifikasi Otomatis:</strong>
                    <span v-if="interaksiForm.arah_sikap > 0 && interaksiForm.level_aktivitas >= 3">
                      <span class="badge bg-success">Pro-Aktif</span>
                    </span>
                    <span v-else-if="interaksiForm.arah_sikap > 0 && interaksiForm.level_aktivitas < 3">
                      <span class="badge bg-info">Pro-Pasif</span>
                    </span>
                    <span v-else-if="interaksiForm.arah_sikap < 0 && interaksiForm.level_aktivitas >= 3">
                      <span class="badge bg-danger">Kontra-Aktif</span>
                    </span>
                    <span v-else-if="interaksiForm.arah_sikap < 0 && interaksiForm.level_aktivitas < 3">
                      <span class="badge bg-warning">Kontra-Pasif</span>
                    </span>
                    <span v-else>
                      <span class="badge bg-secondary">Netral</span>
                    </span>
                  </div>
                </div>
              </div>
            </div>

            <!-- Form Relasi -->
            <div v-if="modalType === 'relasi'">
              <div class="row">
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Stakeholder A *</label>
                    <select class="form-select" v-model="relationForm.stakeholder_a_id">
                      <option value="">Pilih Stakeholder A</option>
                      <option v-for="sh in stakeholders" :key="sh.id" :value="sh.id">{{ sh.nama_lengkap }}</option>
                    </select>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Stakeholder B *</label>
                    <select class="form-select" v-model="relationForm.stakeholder_b_id">
                      <option value="">Pilih Stakeholder B</option>
                      <option v-for="sh in stakeholders" :key="sh.id" :value="sh.id">{{ sh.nama_lengkap }}</option>
                    </select>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Jenis Relasi *</label>
                    <select class="form-select" v-model="relationForm.jenis_relasi">
                      <option value="Keluarga besar">Keluarga besar</option>
                      <option value="Keluarga inti">Keluarga inti</option>
                      <option value="Tetangga">Tetangga</option>
                      <option value="Rekan kerja">Rekan kerja</option>
                      <option value="Rekan organisasi">Rekan organisasi</option>
                      <option value="Teman">Teman</option>
                    </select>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Frekuensi Kontak *</label>
                    <select class="form-select" v-model="relationForm.frekuensi_kontak">
                      <option value="Harian">Harian</option>
                      <option value="Mingguan">Mingguan</option>
                      <option value="Bulanan">Bulanan</option>
                      <option value="Jarang">Jarang</option>
                    </select>
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Score Closeness (0-100) *</label>
                    <input type="number" class="form-control" v-model.number="relationForm.score_closeness" min="0" max="100">
                  </div>
                </div>
                <div class="col-md-6">
                  <div class="mb-3">
                    <label class="form-label">Arah Pengaruh *</label>
                    <select class="form-select" v-model="relationForm.arah_pengaruh">
                      <option value="A → B">A → B (A mempengaruhi B)</option>
                      <option value="B → A">B → A (B mempengaruhi A)</option>
                      <option value="Bidirectional">Bidirectional (Saling mempengaruhi)</option>
                    </select>
                  </div>
                </div>
                <div class="col-12">
                  <div class="mb-3">
                    <label class="form-label">Keterangan</label>
                    <textarea class="form-control" rows="2" v-model="relationForm.keterangan"></textarea>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" @click="closeModal">Batal</button>
            <button type="button" class="btn btn-primary" @click="saveForm">Simpan</button>
          </div>
        </div>
      </div>
    </div>
    <div class="modal-backdrop fade" :class="{ show: showModal }" v-if="showModal"></div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const activeTab = ref('master')
const showModal = ref(false)
const modalType = ref('')
const modalTitle = ref('')
const networkCanvas = ref<HTMLCanvasElement | null>(null)

// Statistics
const stats = ref({
  total: 15,
  proAktif: 5,
  proPasif: 4,
  kontraAktif: 3,
  kontraPasif: 2,
  netral: 1
})

// Form Data Models
const masterForm = ref({
  id: null as number | null,
  nama: '',
  nik: '',
  role: '',
  desa: '',
  kecamatan: '',
  kabupaten: '',
  provinsi: '',
  telepon: '',
  email: '',
  level_pengaruh: 3,
  level_kepentingan: 3,
  sentiment_kategori: 'Netral',
  catatan: ''
})

const backgroundForm = ref({
  id: null as number | null,
  stakeholder_id: null as number | null,
  jenjang_pendidikan: '',
  universitas: '',
  jurusan: '',
  tahun_masuk: '',
  tahun_lulus: '',
  pekerjaan_utama: '',
  instansi: '',
  jabatan: '',
  tahun_mulai_kerja: '',
  organisasi: [] as string[],
  status_kekerabatan: false,
  detail_kekerabatan: '',
  dusun_rt_rw: ''
})

const isuForm = ref({
  id: null as number | null,
  stakeholder_id: null as number | null,
  nama_project: '',
  jenis_dampak: '',
  besaran_dampak: 0,
  persepsi_awal: 'Netral',
  topik_keberatan: '',
  tingkat_pengaruh_dampak: 3
})

const interaksiForm = ref({
  id: null as number | null,
  stakeholder_id: null as number | null,
  tanggal_interaksi: '',
  jenis_interaksi: '',
  topik: '',
  perilaku_observed: '',
  pernyataan_kunci: '',
  arah_sikap: 0,
  level_aktivitas: 2,
  klasifikasi_sentimen: ''
})

const relationForm = ref({
  id: null as number | null,
  stakeholder_a_id: null as number | null,
  stakeholder_b_id: null as number | null,
  jenis_relasi: '',
  frekuensi_kontak: '',
  score_closeness: 50,
  arah_pengaruh: 'Bidirectional',
  keterangan: ''
})

// Sample data - Master Stakeholder
const stakeholders = ref([
  {
    id: 1,
    stakeholder_id: 'SH-001',
    nama_lengkap: 'Ahmad Sulaiman',
    nama_panggilan: 'Pak Ahmad',
    jenis_stakeholder: 'Individu',
    peran_di_proyek: 'Pemilik Lahan',
    level_pengaruh: 4,
    level_kepentingan: 5,
    klasifikasi_sikap: 'Kontra-Aktif',
    desa: 'Sukamaju',
    telepon: '081234567890'
  },
  {
    id: 2,
    stakeholder_id: 'SH-002',
    nama_lengkap: 'Budi Santoso',
    nama_panggilan: 'Pak Budi',
    jenis_stakeholder: 'Individu',
    peran_di_proyek: 'Tokoh Adat',
    level_pengaruh: 5,
    level_kepentingan: 3,
    klasifikasi_sikap: 'Pro-Aktif',
    desa: 'Makmur',
    telepon: '081234567891'
  },
  {
    id: 3,
    stakeholder_id: 'SH-003',
    nama_lengkap: 'Siti Aminah',
    nama_panggilan: 'Ibu Siti',
    jenis_stakeholder: 'Individu',
    peran_di_proyek: 'Ketua RT',
    level_pengaruh: 3,
    level_kepentingan: 4,
    klasifikasi_sikap: 'Pro-Pasif',
    desa: 'Sukamaju',
    telepon: '081234567892'
  },
  {
    id: 4,
    stakeholder_id: 'SH-004',
    nama_lengkap: 'Joko Widodo',
    nama_panggilan: 'Pak Joko',
    jenis_stakeholder: 'Individu',
    peran_di_proyek: 'Petani',
    level_pengaruh: 2,
    level_kepentingan: 5,
    klasifikasi_sikap: 'Kontra-Pasif',
    desa: 'Sejahtera',
    telepon: '081234567893'
  },
  {
    id: 5,
    stakeholder_id: 'SH-005',
    nama_lengkap: 'Dewi Lestari',
    nama_panggilan: 'Ibu Dewi',
    jenis_stakeholder: 'Individu',
    peran_di_proyek: 'Tokoh Perempuan',
    level_pengaruh: 4,
    level_kepentingan: 4,
    klasifikasi_sikap: 'Pro-Aktif',
    desa: 'Makmur',
    telepon: '081234567894'
  }
])

// Sample data - Background
const backgrounds = ref([
  {
    id: 1,
    stakeholder_id: 1,
    stakeholder_nama: 'Ahmad Sulaiman',
    jenjang_pendidikan: 'S1',
    universitas: 'Universitas Hasanuddin',
    jurusan: 'Teknik Sipil',
    tahun_masuk: 1995,
    tahun_lulus: 1999,
    pekerjaan_utama: 'Petani',
    instansi: 'Mandiri',
    organisasi: ['Kelompok Tani Sukamaju', 'Karang Taruna'],
    status_kekerabatan: true,
    detail_kekerabatan: 'Sepupu Budi Santoso',
    dusun_rt_rw: 'Dusun Mawar RT 02 RW 03'
  },
  {
    id: 2,
    stakeholder_id: 2,
    stakeholder_nama: 'Budi Santoso',
    jenjang_pendidikan: 'S1',
    universitas: 'Universitas Hasanuddin',
    jurusan: 'Hukum Adat',
    tahun_masuk: 1998,
    tahun_lulus: 2002,
    pekerjaan_utama: 'Tokoh Adat',
    instansi: 'Lembaga Adat',
    organisasi: ['Lembaga Adat Makmur', 'Forum Tokoh Masyarakat'],
    status_kekerabatan: true,
    detail_kekerabatan: 'Sepupu Ahmad Sulaiman',
    dusun_rt_rw: 'Dusun Melati RT 05 RW 02'
  },
  {
    id: 3,
    stakeholder_id: 3,
    stakeholder_nama: 'Siti Aminah',
    jenjang_pendidikan: 'SMA',
    universitas: '-',
    jurusan: '-',
    tahun_masuk: 0,
    tahun_lulus: 0,
    pekerjaan_utama: 'Ibu Rumah Tangga',
    instansi: '-',
    organisasi: ['PKK', 'Posyandu'],
    status_kekerabatan: false,
    detail_kekerabatan: '-',
    dusun_rt_rw: 'Dusun Mawar RT 02 RW 03'
  },
  {
    id: 4,
    stakeholder_id: 4,
    stakeholder_nama: 'Joko Widodo',
    jenjang_pendidikan: 'SMP',
    universitas: '-',
    jurusan: '-',
    tahun_masuk: 0,
    tahun_lulus: 0,
    pekerjaan_utama: 'Petani',
    instansi: 'Mandiri',
    organisasi: ['Kelompok Tani Sejahtera'],
    status_kekerabatan: false,
    detail_kekerabatan: '-',
    dusun_rt_rw: 'Dusun Kenanga RT 01 RW 01'
  },
  {
    id: 5,
    stakeholder_id: 5,
    stakeholder_nama: 'Dewi Lestari',
    jenjang_pendidikan: 'S2',
    universitas: 'Universitas Indonesia',
    jurusan: 'Sosiologi',
    tahun_masuk: 2005,
    tahun_lulus: 2009,
    pekerjaan_utama: 'Aktivis LSM',
    instansi: 'LSM Peduli Lingkungan',
    organisasi: ['LSM Peduli Lingkungan', 'Forum Perempuan', 'Komunitas Lingkungan'],
    status_kekerabatan: false,
    detail_kekerabatan: '-',
    dusun_rt_rw: 'Dusun Melati RT 03 RW 02'
  }
])

// Sample data - Isu
const issuData = ref([
  {
    id: 1,
    stakeholder_id: 1,
    stakeholder_nama: 'Ahmad Sulaiman',
    project_id: 'PRJ-001',
    nama_project: 'Pembangunan Jalan Tambang',
    isu_spesifik: 'Lokasi trase jalan',
    jenis_dampak: ['Ekonomi', 'Sosial', 'Aset Lahan'],
    besaran_dampak: 5,
    persepsi_umum: 'Negatif',
    topik_keberatan: 'Jalan melewati lahan pertanian produktif'
  },
  {
    id: 2,
    stakeholder_id: 2,
    stakeholder_nama: 'Budi Santoso',
    project_id: 'PRJ-001',
    nama_project: 'Pembangunan Jalan Tambang',
    isu_spesifik: 'Kompensasi dan manfaat',
    jenis_dampak: ['Ekonomi', 'Sosial'],
    besaran_dampak: 3,
    persepsi_umum: 'Positif',
    topik_keberatan: '-'
  },
  {
    id: 3,
    stakeholder_id: 3,
    stakeholder_nama: 'Siti Aminah',
    project_id: 'PRJ-001',
    nama_project: 'Pembangunan Jalan Tambang',
    isu_spesifik: 'Akses jalan desa',
    jenis_dampak: ['Infrastruktur'],
    besaran_dampak: 4,
    persepsi_umum: 'Positif',
    topik_keberatan: '-'
  },
  {
    id: 4,
    stakeholder_id: 4,
    stakeholder_nama: 'Joko Widodo',
    project_id: 'PRJ-001',
    nama_project: 'Pembangunan Jalan Tambang',
    isu_spesifik: 'Nilai ganti rugi lahan',
    jenis_dampak: ['Ekonomi', 'Aset Lahan'],
    besaran_dampak: 5,
    persepsi_umum: 'Negatif',
    topik_keberatan: 'Nilai ganti rugi terlalu rendah'
  },
  {
    id: 5,
    stakeholder_id: 5,
    stakeholder_nama: 'Dewi Lestari',
    project_id: 'PRJ-001',
    nama_project: 'Pembangunan Jalan Tambang',
    isu_spesifik: 'Dampak lingkungan',
    jenis_dampak: ['Lingkungan', 'Sosial'],
    besaran_dampak: 4,
    persepsi_umum: 'Positif',
    topik_keberatan: 'Perlu kajian lingkungan lebih detail'
  }
])

// Sample data - Interaction Logs
const interactionLogs = ref([
  {
    id: 1,
    stakeholder_id: 1,
    stakeholder_nama: 'Ahmad Sulaiman',
    tanggal: '2025-01-15',
    lokasi: 'Balai Desa',
    jenis_interaksi: 'Rapat Desa',
    peran_dalam_pertemuan: 'Menyampaikan keberatan',
    ringkasan_pernyataan: 'Jalan ini melewati lahan saya yang paling produktif. Kami menolak lokasi ini!',
    kategori_pernyataan: 'Keberatan teknis',
    nada: 'Konfrontatif',
    arah_sikap: -2,
    level_aktivitas: 4,
    klasifikasi_sentimen: 'Kontra-Aktif'
  },
  {
    id: 2,
    stakeholder_id: 1,
    stakeholder_nama: 'Ahmad Sulaiman',
    tanggal: '2025-01-22',
    lokasi: 'Rumah Ahmad',
    jenis_interaksi: 'Kunjungan Tim',
    peran_dalam_pertemuan: 'Menerima kunjungan',
    ringkasan_pernyataan: 'Saya tidak akan kompromi soal lokasi jalan ini',
    kategori_pernyataan: 'Penolakan',
    nada: 'Tegas',
    arah_sikap: -2,
    level_aktivitas: 3,
    klasifikasi_sentimen: 'Kontra-Aktif'
  },
  {
    id: 3,
    stakeholder_id: 2,
    stakeholder_nama: 'Budi Santoso',
    tanggal: '2025-01-16',
    lokasi: 'Balai Desa',
    jenis_interaksi: 'Rapat Desa',
    peran_dalam_pertemuan: 'Mediator',
    ringkasan_pernyataan: 'Proyek ini baik untuk desa, saya akan bantu koordinasi dengan masyarakat',
    kategori_pernyataan: 'Dukungan',
    nada: 'Kooperatif',
    arah_sikap: 2,
    level_aktivitas: 4,
    klasifikasi_sentimen: 'Pro-Aktif'
  },
  {
    id: 4,
    stakeholder_id: 2,
    stakeholder_nama: 'Budi Santoso',
    tanggal: '2025-01-20',
    lokasi: 'Kantor Desa',
    jenis_interaksi: 'Pertemuan Koordinasi',
    peran_dalam_pertemuan: 'Fasilitator',
    ringkasan_pernyataan: 'Saya akan mengumpulkan warga untuk sosialisasi minggu depan',
    kategori_pernyataan: 'Tindak lanjut',
    nada: 'Antusias',
    arah_sikap: 2,
    level_aktivitas: 4,
    klasifikasi_sentimen: 'Pro-Aktif'
  },
  {
    id: 5,
    stakeholder_id: 3,
    stakeholder_nama: 'Siti Aminah',
    tanggal: '2025-01-17',
    lokasi: 'Balai Desa',
    jenis_interaksi: 'Rapat Desa',
    peran_dalam_pertemuan: 'Peserta',
    ringkasan_pernyataan: 'Bagus jika ada jalan baru, tapi saya tidak mau terlalu banyak terlibat',
    kategori_pernyataan: 'Dukungan pasif',
    nada: 'Netral',
    arah_sikap: 1,
    level_aktivitas: 2,
    klasifikasi_sentimen: 'Pro-Pasif'
  },
  {
    id: 6,
    stakeholder_id: 4,
    stakeholder_nama: 'Joko Widodo',
    tanggal: '2025-01-18',
    lokasi: 'Rumah Joko',
    jenis_interaksi: 'Kunjungan Tim',
    peran_dalam_pertemuan: 'Menerima kunjungan',
    ringkasan_pernyataan: 'Nilai ganti rugi tidak cukup, tapi saya tidak mau ribut',
    kategori_pernyataan: 'Keluhan',
    nada: 'Pasif',
    arah_sikap: -1,
    level_aktivitas: 1,
    klasifikasi_sentimen: 'Kontra-Pasif'
  },
  {
    id: 7,
    stakeholder_id: 5,
    stakeholder_nama: 'Dewi Lestari',
    tanggal: '2025-01-19',
    lokasi: 'Kantor LSM',
    jenis_interaksi: 'Diskusi',
    peran_dalam_pertemuan: 'Pembicara',
    ringkasan_pernyataan: 'Kami mendukung proyek ini, asalkan ada kajian lingkungan yang proper',
    kategori_pernyataan: 'Dukungan bersyarat',
    nada: 'Profesional',
    arah_sikap: 2,
    level_aktivitas: 4,
    klasifikasi_sentimen: 'Pro-Aktif'
  }
])

// Sample data - Relations
const relations = ref([
  {
    id: 1,
    stakeholder_a_id: 1,
    stakeholder_a_nama: 'Ahmad Sulaiman',
    stakeholder_b_id: 2,
    stakeholder_b_nama: 'Budi Santoso',
    jenis_relasi: 'Keluarga besar',
    frekuensi_interaksi: 'Mingguan',
    intensitas_kedekatan: 4,
    satu_universitas: true,
    satu_jurusan: false,
    satu_organisasi: true,
    hubungan_kekerabatan: true,
    skor_kedekatan_total: 75
  },
  {
    id: 2,
    stakeholder_a_id: 1,
    stakeholder_a_nama: 'Ahmad Sulaiman',
    stakeholder_b_id: 3,
    stakeholder_b_nama: 'Siti Aminah',
    jenis_relasi: 'Tetangga',
    frekuensi_interaksi: 'Harian',
    intensitas_kedekatan: 3,
    satu_universitas: false,
    satu_jurusan: false,
    satu_organisasi: true,
    hubungan_kekerabatan: false,
    skor_kedekatan_total: 55
  },
  {
    id: 3,
    stakeholder_a_id: 2,
    stakeholder_a_nama: 'Budi Santoso',
    stakeholder_b_id: 5,
    stakeholder_b_nama: 'Dewi Lestari',
    jenis_relasi: 'Rekan kerja',
    frekuensi_interaksi: 'Bulanan',
    intensitas_kedekatan: 3,
    satu_universitas: false,
    satu_jurusan: false,
    satu_organisasi: true,
    hubungan_kekerabatan: false,
    skor_kedekatan_total: 45
  },
  {
    id: 4,
    stakeholder_a_id: 3,
    stakeholder_a_nama: 'Siti Aminah',
    stakeholder_b_id: 4,
    stakeholder_b_nama: 'Joko Widodo',
    jenis_relasi: 'Tetangga',
    frekuensi_interaksi: 'Mingguan',
    intensitas_kedekatan: 2,
    satu_universitas: false,
    satu_jurusan: false,
    satu_organisasi: false,
    hubungan_kekerabatan: false,
    skor_kedekatan_total: 30
  },
  {
    id: 5,
    stakeholder_a_id: 1,
    stakeholder_a_nama: 'Ahmad Sulaiman',
    stakeholder_b_id: 4,
    stakeholder_b_nama: 'Joko Widodo',
    jenis_relasi: 'Rekan kelompok tani',
    frekuensi_interaksi: 'Mingguan',
    intensitas_kedekatan: 3,
    satu_universitas: false,
    satu_jurusan: false,
    satu_organisasi: true,
    hubungan_kekerabatan: false,
    skor_kedekatan_total: 50
  }
])

// Sample data - Evidence
const evidences = ref([
  {
    id: 1,
    stakeholder_id: 1,
    stakeholder_nama: 'Ahmad Sulaiman',
    jenis_bukti: 'Notulen',
    deskripsi_pendek: 'Notulen rapat desa tanggal 15 Jan 2025',
    tanggal_dokumen: '2025-01-15',
    penanggung_jawab: 'Tim Community Relations'
  },
  {
    id: 2,
    stakeholder_id: 2,
    stakeholder_nama: 'Budi Santoso',
    jenis_bukti: 'Foto',
    deskripsi_pendek: 'Foto pertemuan dengan tokoh adat',
    tanggal_dokumen: '2025-01-16',
    penanggung_jawab: 'Tim Dokumentasi'
  },
  {
    id: 3,
    stakeholder_id: 1,
    stakeholder_nama: 'Ahmad Sulaiman',
    jenis_bukti: 'Rekaman Audio',
    deskripsi_pendek: 'Rekaman pernyataan Ahmad di rapat desa',
    tanggal_dokumen: '2025-01-15',
    penanggung_jawab: 'Tim Community Relations'
  },
  {
    id: 4,
    stakeholder_id: 5,
    stakeholder_nama: 'Dewi Lestari',
    jenis_bukti: 'Surat',
    deskripsi_pendek: 'Surat dukungan dari LSM Peduli Lingkungan',
    tanggal_dokumen: '2025-01-19',
    penanggung_jawab: 'Tim Legal'
  },
  {
    id: 5,
    stakeholder_id: 4,
    stakeholder_nama: 'Joko Widodo',
    jenis_bukti: 'Dokumen',
    deskripsi_pendek: 'Surat keberatan nilai ganti rugi',
    tanggal_dokumen: '2025-01-18',
    penanggung_jawab: 'Tim LARAP'
  }
])

// Helper functions
const getBadgeInfluence = (level: number) => {
  if (level >= 4) return 'bg-danger'
  if (level >= 3) return 'bg-warning'
  return 'bg-secondary'
}

const getBadgeInterest = (level: number) => {
  if (level >= 4) return 'bg-primary'
  if (level >= 3) return 'bg-info'
  return 'bg-secondary'
}

const getBadgeSentimen = (sikap: string) => {
  if (sikap.includes('Pro-Aktif')) return 'bg-success'
  if (sikap.includes('Pro-Pasif')) return 'bg-info'
  if (sikap.includes('Kontra-Aktif')) return 'bg-danger'
  if (sikap.includes('Kontra-Pasif')) return 'bg-warning'
  return 'bg-secondary'
}

const getProgressClass = (level: number) => {
  if (level >= 4) return 'bg-danger'
  if (level >= 3) return 'bg-warning'
  return 'bg-success'
}

const getBadgePersepsi = (persepsi: string) => {
  if (persepsi === 'Positif') return 'bg-success'
  if (persepsi === 'Negatif') return 'bg-danger'
  if (persepsi === 'Netral') return 'bg-secondary'
  return 'bg-warning'
}

const getBadgeNada = (nada: string) => {
  if (nada === 'Kooperatif') return 'bg-success'
  if (nada === 'Konfrontatif') return 'bg-danger'
  if (nada === 'Kritis') return 'bg-warning'
  return 'bg-secondary'
}

const getBadgeArahSikap = (arah: number) => {
  if (arah >= 1) return 'bg-success'
  if (arah <= -1) return 'bg-danger'
  return 'bg-secondary'
}

const getArahSikapLabel = (arah: number) => {
  if (arah === 2) return 'Sangat Mendukung'
  if (arah === 1) return 'Mendukung'
  if (arah === 0) return 'Netral'
  if (arah === -1) return 'Menolak'
  if (arah === -2) return 'Sangat Menolak'
  return 'Netral'
}

const getBadgeAktivitas = (level: number) => {
  if (level === 4) return 'bg-danger'
  if (level === 3) return 'bg-warning'
  if (level === 2) return 'bg-info'
  return 'bg-secondary'
}

const getBadgeKedekatan = (skor: number) => {
  if (skor >= 70) return 'bg-success'
  if (skor >= 50) return 'bg-info'
  if (skor >= 30) return 'bg-warning'
  return 'bg-secondary'
}

const getFileIcon = (jenis: string) => {
  if (jenis.includes('Foto')) return 'bi-image'
  if (jenis.includes('Video')) return 'bi-camera-video'
  if (jenis.includes('PDF') || jenis.includes('Surat')) return 'bi-file-pdf'
  if (jenis.includes('Notulen')) return 'bi-file-text'
  return 'bi-file-earmark'
}

const formatDate = (date: string) => {
  return new Date(date).toLocaleDateString('id-ID', { 
    day: '2-digit', 
    month: 'short', 
    year: 'numeric' 
  })
}

// Modal functions
const openModalAdd = (type: string) => {
  modalType.value = type
  modalTitle.value = `Tambah Data ${type.charAt(0).toUpperCase() + type.slice(1)}`
  showModal.value = true
}

const closeModal = () => {
  showModal.value = false
}

const saveForm = () => {
  // Save logic here
  console.log('Saving', modalType.value)
  closeModal()
}

// CRUD functions
const viewDetail = (sh: any) => {
  console.log('View detail:', sh)
}

const editStakeholder = (sh: any) => {
  console.log('Edit:', sh)
}

const deleteStakeholder = (id: number) => {
  if (confirm('Yakin ingin menghapus stakeholder ini?')) {
    console.log('Delete:', id)
  }
}

const editBackground = (bg: any) => {
  console.log('Edit background:', bg)
}

const deleteBackground = (id: number) => {
  if (confirm('Yakin ingin menghapus data background ini?')) {
    console.log('Delete background:', id)
  }
}

const editIsu = (isu: any) => {
  console.log('Edit isu:', isu)
}

const deleteIsu = (id: number) => {
  if (confirm('Yakin ingin menghapus data isu ini?')) {
    console.log('Delete isu:', id)
  }
}

const viewInteraksi = (log: any) => {
  console.log('View interaksi:', log)
}

const editInteraksi = (log: any) => {
  console.log('Edit interaksi:', log)
}

const deleteInteraksi = (id: number) => {
  if (confirm('Yakin ingin menghapus log interaksi ini?')) {
    console.log('Delete interaksi:', id)
  }
}

const editRelation = (rel: any) => {
  console.log('Edit relation:', rel)
}

const deleteRelation = (id: number) => {
  if (confirm('Yakin ingin menghapus relasi ini?')) {
    console.log('Delete relation:', id)
  }
}

const viewDocument = (doc: any) => {
  console.log('View document:', doc)
}

const downloadDocument = (doc: any) => {
  console.log('Download document:', doc)
}

const deleteEvidence = (id: number) => {
  if (confirm('Yakin ingin menghapus dokumen ini?')) {
    console.log('Delete evidence:', id)
  }
}

// Draw network visualization
const drawNetwork = () => {
  if (!networkCanvas.value) return
  
  const canvas = networkCanvas.value
  const ctx = canvas.getContext('2d')
  if (!ctx) return

  // Clear canvas
  ctx.clearRect(0, 0, canvas.width, canvas.height)

  // Define node positions (circular layout)
  const centerX = canvas.width / 2
  const centerY = canvas.height / 2
  const radius = 150
  const nodes = stakeholders.value.map((sh, index) => {
    const angle = (index * 2 * Math.PI) / stakeholders.value.length
    return {
      x: centerX + radius * Math.cos(angle),
      y: centerY + radius * Math.sin(angle),
      ...sh
    }
  })

  // Draw connections first (so they appear behind nodes)
  relations.value.forEach(rel => {
    const nodeA = nodes.find(n => n.id === rel.stakeholder_a_id)
    const nodeB = nodes.find(n => n.id === rel.stakeholder_b_id)
    
    if (nodeA && nodeB) {
      ctx.beginPath()
      ctx.moveTo(nodeA.x, nodeA.y)
      ctx.lineTo(nodeB.x, nodeB.y)
      
      // Line thickness based on closeness score
      if (rel.skor_kedekatan_total > 70) {
        ctx.lineWidth = 3
        ctx.strokeStyle = '#333'
      } else if (rel.skor_kedekatan_total > 40) {
        ctx.lineWidth = 2
        ctx.strokeStyle = '#666'
      } else {
        ctx.lineWidth = 1
        ctx.strokeStyle = '#999'
      }
      
      ctx.stroke()
      
      // Draw closeness score in the middle of line
      const midX = (nodeA.x + nodeB.x) / 2
      const midY = (nodeA.y + nodeB.y) / 2
      ctx.fillStyle = '#000'
      ctx.font = '10px Arial'
      ctx.fillText(rel.skor_kedekatan_total.toString(), midX, midY)
    }
  })

  // Draw nodes
  nodes.forEach(node => {
    // Determine color based on sentiment
    let color = '#6c757d' // default gray
    if (node.klasifikasi_sikap?.includes('Pro-Aktif')) {
      color = '#28a745' // green
    } else if (node.klasifikasi_sikap?.includes('Pro-Pasif')) {
      color = '#17a2b8' // cyan
    } else if (node.klasifikasi_sikap?.includes('Kontra-Aktif')) {
      color = '#dc3545' // red
    } else if (node.klasifikasi_sikap?.includes('Kontra-Pasif')) {
      color = '#ffc107' // yellow
    }

    // Draw circle
    ctx.beginPath()
    ctx.arc(node.x, node.y, 30, 0, 2 * Math.PI)
    ctx.fillStyle = color
    ctx.fill()
    ctx.strokeStyle = '#fff'
    ctx.lineWidth = 3
    ctx.stroke()

    // Draw name
    ctx.fillStyle = '#000'
    ctx.font = 'bold 11px Arial'
    ctx.textAlign = 'center'
    ctx.fillText(node.nama_panggilan || node.nama_lengkap || '', node.x, node.y + 50)
    
    // Draw role
    ctx.font = '9px Arial'
    ctx.fillStyle = '#666'
    ctx.fillText(node.peran_di_proyek || '', node.x, node.y + 62)
  })
}

onMounted(() => {
  // Initialize network visualization
  setTimeout(() => {
    drawNetwork()
  }, 100)
})
</script>

<style scoped>
.modal.show {
  display: block;
}

.modal-backdrop.show {
  opacity: 0.5;
}

.table th {
  font-size: 0.875rem;
  white-space: nowrap;
}

.table td {
  font-size: 0.875rem;
  vertical-align: middle;
}

.badge {
  font-size: 0.75rem;
}

.progress {
  min-width: 80px;
}

.card {
  box-shadow: 0 0 1px rgba(0,0,0,.125), 0 1px 3px rgba(0,0,0,.2);
}
</style>
