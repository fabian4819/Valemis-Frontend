<template>
  <div class="modern-dashboard">
    <!-- Stat Cards Row -->
    <div class="stats-grid">
      <!-- Total Sales Card -->
      <div class="stat-card gradient-primary">
        <div class="stat-icon">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <rect x="2" y="7" width="20" height="14" rx="2" ry="2"></rect>
            <path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"></path>
          </svg>
        </div>
        <div class="stat-content">
          <div class="stat-label">Total Lahan</div>
          <div class="stat-value">$612,917</div>
          <div class="stat-subtitle">Products vs last month</div>
        </div>
        <div class="stat-badge success">+92.09%</div>
      </div>

      <!-- Total Orders Card -->
      <div class="stat-card white">
        <div class="stat-header">
          <div class="stat-icon-simple">
            <svg width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
              <path d="M9 2a1 1 0 000 2h2a1 1 0 100-2H9z"></path>
              <path fill-rule="evenodd" d="M4 5a2 2 0 012-2 3 3 0 003 3h2a3 3 0 003-3 2 2 0 012 2v11a2 2 0 01-2 2H6a2 2 0 01-2-2V5zm3 4a1 1 0 000 2h.01a1 1 0 100-2H7zm3 0a1 1 0 000 2h3a1 1 0 100-2h-3zm-3 4a1 1 0 100 2h.01a1 1 0 100-2H7zm3 0a1 1 0 100 2h3a1 1 0 100-2h-3z" clip-rule="evenodd"></path>
            </svg>
          </div>
          <div class="stat-badge success">+15.03%</div>
        </div>
        <div class="stat-label">Pembebasan Lahan</div>
        <div class="stat-value dark">34,560</div>
        <div class="stat-subtitle">Orders vs last month</div>
      </div>

      <!-- Visitors Card -->
      <div class="stat-card white">
        <div class="stat-header">
          <div class="stat-icon-simple">
            <svg width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
              <path d="M9 6a3 3 0 11-6 0 3 3 0 016 0zM17 6a3 3 0 11-6 0 3 3 0 016 0zM12.93 17c.046-.327.07-.66.07-1a6.97 6.97 0 00-1.5-4.33A5 5 0 0119 16v1h-6.07zM6 11a5 5 0 015 5v1H1v-1a5 5 0 015-5z"></path>
            </svg>
          </div>
          <div class="stat-badge danger">-2.08%</div>
        </div>
        <div class="stat-label">Stakeholder</div>
        <div class="stat-value dark">14,987</div>
        <div class="stat-subtitle">Users vs last month</div>
      </div>

      <!-- Total Sold Products Card -->
      <div class="stat-card white">
        <div class="stat-header">
          <div class="stat-icon-simple">
            <svg width="20" height="20" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M10 2a4 4 0 00-4 4v1H5a1 1 0 00-.994.89l-1 9A1 1 0 004 18h12a1 1 0 00.994-1.11l-1-9A1 1 0 0015 7h-1V6a4 4 0 00-4-4zm2 5V6a2 2 0 10-4 0v1h4zm-6 3a1 1 0 112 0 1 1 0 01-2 0zm7-1a1 1 0 100 2 1 1 0 000-2z" clip-rule="evenodd"></path>
            </svg>
          </div>
          <div class="stat-badge success">+12.10%</div>
        </div>
        <div class="stat-label">Litigasi</div>
        <div class="stat-value dark">12,987</div>
        <div class="stat-subtitle">Products vs last month</div>
      </div>
    </div>
            </div>
          </div>

          <div class="col-lg-3 col-6">
            <div class="small-box">
              <div class="inner">
                <h3><sup style="font-size: 20px">Rp.</sup>13.000.000.000</h3>
                <p>Total Biaya</p>
              </div>
              <div class="icon">
                <i class="ion ion-stats-bars"></i>
              </div>
              <a href="#" class="small-box-footer">
                More info <i class="fas fa-arrow-circle-right"></i>
              </a>
            </div>
          </div>

          <div class="col-lg-3 col-6">
            <div class="small-box">
              <div class="inner">
                <h3>78<sup style="font-size: 20px">%</sup></h3>
                <p>Grafik Total</p>
              </div>
              <div class="icon">
                <i class="ion ion-stats-bars"></i>
              </div>
              <a href="#" class="small-box-footer">
                More info <i class="fas fa-arrow-circle-right"></i>
              </a>
            </div>
          </div>
        </div>

        <div class="row">
          <div class="col-md-6">
            <div class="card card">
              <div class="card-header">
                <h3 class="card-title">Luas Lahan</h3>
                <div class="card-tools">
                  <button type="button" class="btn btn-tool" data-card-widget="collapse">
                    <i class="fas fa-minus"></i>
                  </button>
                  <button type="button" class="btn btn-tool" data-card-widget="remove">
                    <i class="fas fa-times"></i>
                  </button>
                </div>
              </div>
              <div class="card-body" style="display: block">
                <div class="chart">
                  <canvas
                    ref="barChart1"
                    style="min-height: 250px; height: 250px; max-height: 250px; max-width: 100%"
                  ></canvas>
                </div>
              </div>
            </div>
          </div>

          <div class="col-md-6">
            <div class="card card">
              <div class="card-header">
                <h3 class="card-title">Lahan Di Bebaskan</h3>
                <div class="card-tools">
                  <button type="button" class="btn btn-tool" data-card-widget="collapse">
                    <i class="fas fa-minus"></i>
                  </button>
                  <button type="button" class="btn btn-tool" data-card-widget="remove">
                    <i class="fas fa-times"></i>
                  </button>
                </div>
              </div>
              <div class="card-body" style="display: block">
                <div class="chart">
                  <canvas
                    ref="barChart2"
                    style="min-height: 250px; height: 250px; max-height: 250px; max-width: 100%"
                  ></canvas>
                </div>
              </div>
            </div>
          </div>

          <div class="col-md-6">
            <div class="card card">
              <div class="card-header">
                <h3 class="card-title">Total Biaya</h3>
                <div class="card-tools">
                  <button type="button" class="btn btn-tool" data-card-widget="collapse">
                    <i class="fas fa-minus"></i>
                  </button>
                  <button type="button" class="btn btn-tool" data-card-widget="remove">
                    <i class="fas fa-times"></i>
                  </button>
                </div>
              </div>
              <div class="card-body" style="display: block">
                <div class="chart">
                  <canvas
                    ref="barChart3"
                    style="min-height: 250px; height: 250px; max-height: 250px; max-width: 100%"
                  ></canvas>
                </div>
              </div>
            </div>
          </div>

          <div class="col-md-6">
            <div class="card card">
              <div class="card-header">
                <h3 class="card-title">Grand Total</h3>
                <div class="card-tools">
                  <button type="button" class="btn btn-tool" data-card-widget="collapse">
                    <i class="fas fa-minus"></i>
                  </button>
                  <button type="button" class="btn btn-tool" data-card-widget="remove">
                    <i class="fas fa-times"></i>
                  </button>
                </div>
              </div>
              <div class="card-body" style="display: block">
                <div class="chart">
                  <canvas
                    ref="barChart4"
                    style="min-height: 250px; height: 250px; max-height: 250px; max-width: 100%"
                  ></canvas>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { Chart, registerables } from 'chart.js'

Chart.register(...registerables)

const barChart1 = ref<HTMLCanvasElement | null>(null)
const barChart2 = ref<HTMLCanvasElement | null>(null)
const barChart3 = ref<HTMLCanvasElement | null>(null)
const barChart4 = ref<HTMLCanvasElement | null>(null)

onMounted(() => {
  const areaChartData = {
    labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
    datasets: [
      {
        label: 'Plan',
        backgroundColor: 'rgba(60,141,188,0.9)',
        borderColor: 'rgba(60,141,188,0.8)',
        pointRadius: false,
        pointColor: '#3b8bba',
        pointStrokeColor: 'rgba(60,141,188,1)',
        pointHighlightFill: '#fff',
        pointHighlightStroke: 'rgba(60,141,188,1)',
        data: [28, 48, 40, 19, 86, 27, 90]
      },
      {
        label: 'Realisasi',
        backgroundColor: 'rgba(210, 214, 222, 1)',
        borderColor: 'rgba(210, 214, 222, 1)',
        pointRadius: false,
        pointColor: 'rgba(210, 214, 222, 1)',
        pointStrokeColor: '#c1c7d1',
        pointHighlightFill: '#fff',
        pointHighlightStroke: 'rgba(220,220,220,1)',
        data: [65, 59, 80, 81, 56, 55, 40]
      }
    ]
  }

  const barChartData = JSON.parse(JSON.stringify(areaChartData))
  const temp0 = areaChartData.datasets[0]
  const temp1 = areaChartData.datasets[1]
  barChartData.datasets[0] = temp1
  barChartData.datasets[1] = temp0

  const barChartOptions = {
    responsive: true,
    maintainAspectRatio: false,
    datasetFill: false
  }

  if (barChart1.value) {
    new Chart(barChart1.value, {
      type: 'bar',
      data: barChartData,
      options: barChartOptions
    })
  }

  if (barChart2.value) {
    new Chart(barChart2.value, {
      type: 'bar',
      data: barChartData,
      options: barChartOptions
    })
  }

  if (barChart3.value) {
    new Chart(barChart3.value, {
      type: 'bar',
      data: barChartData,
      options: barChartOptions
    })
  }

  if (barChart4.value) {
    new Chart(barChart4.value, {
      type: 'bar',
      data: barChartData,
      options: barChartOptions
    })
  }
})
</script>

<style scoped>
</style>
