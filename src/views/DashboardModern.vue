<template>
  <div class="modern-dashboard">
    <!-- Stat Cards Row -->
    <div class="stats-grid">
      <!-- Jumlah Luas Lahan Card -->
      <div class="stat-card gradient-primary">
        <div class="stat-label">Jumlah Luas Lahan</div>
        <div class="stat-value">53 <small style="font-size: 18px;">Ha</small></div>
      </div>

      <!-- Jumlah Lahan Di Bebaskan Card -->
      <div class="stat-card white">
        <div class="stat-badge success">More info →</div>
        <div class="stat-label">Jumlah Lahan Di Bebaskan</div>
        <div class="stat-value dark">53 <small style="font-size: 18px;">Parcil</small></div>
      </div>

      <!-- Total Biaya Card -->
      <div class="stat-card white">
        <div class="stat-badge success">More info →</div>
        <div class="stat-label">Total Biaya</div>
        <div class="stat-value dark"><small style="font-size: 14px;">Rp.</small> 13.000.000.000</div>
      </div>

      <!-- Grafik Total Card -->
      <div class="stat-card white">
        <div class="stat-badge success">More info →</div>
        <div class="stat-label">Grafik Total</div>
        <div class="stat-value dark">78 <small style="font-size: 18px;">%</small></div>
      </div>
    </div>

    <!-- Charts Row -->
    <div class="charts-grid">
      <!-- Luas Lahan Chart -->
      <div class="chart-card">
        <div class="card-header">
          <h3 class="card-title">Luas Lahan</h3>
          <div class="card-tools">
            <button class="tool-button" title="Collapse">
              <svg width="16" height="16" viewBox="0 0 16 16" fill="currentColor">
                <path fill-rule="evenodd" d="M8 4a.5.5 0 01.5.5v3h3a.5.5 0 010 1h-3v3a.5.5 0 01-1 0v-3h-3a.5.5 0 010-1h3v-3A.5.5 0 018 4z"></path>
              </svg>
            </button>
          </div>
        </div>
        <div class="card-body">
          <canvas ref="barChart1" height="250"></canvas>
        </div>
      </div>

      <!-- Lahan Di Bebaskan Chart -->
      <div class="chart-card">
        <div class="card-header">
          <h3 class="card-title">Lahan Di Bebaskan</h3>
          <div class="card-tools">
            <button class="tool-button" title="Collapse">
              <svg width="16" height="16" viewBox="0 0 16 16" fill="currentColor">
                <path fill-rule="evenodd" d="M8 4a.5.5 0 01.5.5v3h3a.5.5 0 010 1h-3v3a.5.5 0 01-1 0v-3h-3a.5.5 0 010-1h3v-3A.5.5 0 018 4z"></path>
              </svg>
            </button>
          </div>
        </div>
        <div class="card-body">
          <canvas ref="barChart2" height="250"></canvas>
        </div>
      </div>

      <!-- Total Biaya Chart -->
      <div class="chart-card">
        <div class="card-header">
          <h3 class="card-title">Total Biaya</h3>
          <div class="card-tools">
            <button class="tool-button" title="Collapse">
              <svg width="16" height="16" viewBox="0 0 16 16" fill="currentColor">
                <path fill-rule="evenodd" d="M8 4a.5.5 0 01.5.5v3h3a.5.5 0 010 1h-3v3a.5.5 0 01-1 0v-3h-3a.5.5 0 010-1h3v-3A.5.5 0 018 4z"></path>
              </svg>
            </button>
          </div>
        </div>
        <div class="card-body">
          <canvas ref="barChart3" height="250"></canvas>
        </div>
      </div>

      <!-- Grand Total Chart -->
      <div class="chart-card">
        <div class="card-header">
          <h3 class="card-title">Grand Total</h3>
          <div class="card-tools">
            <button class="tool-button" title="Collapse">
              <svg width="16" height="16" viewBox="0 0 16 16" fill="currentColor">
                <path fill-rule="evenodd" d="M8 4a.5.5 0 01.5.5v3h3a.5.5 0 010 1h-3v3a.5.5 0 01-1 0v-3h-3a.5.5 0 010-1h3v-3A.5.5 0 018 4z"></path>
              </svg>
            </button>
          </div>
        </div>
        <div class="card-body">
          <canvas ref="barChart4" height="250"></canvas>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
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
        backgroundColor: 'rgba(99, 102, 241, 0.8)', // Modern indigo
        borderColor: 'rgba(99, 102, 241, 1)',
        borderWidth: 2,
        borderRadius: 8,
        borderSkipped: false,
        hoverBackgroundColor: 'rgba(99, 102, 241, 0.9)',
        hoverBorderColor: 'rgba(79, 70, 229, 1)',
        hoverBorderWidth: 3,
        data: [28, 48, 40, 19, 86, 27, 90]
      },
      {
        label: 'Realisasi',
        backgroundColor: 'rgba(147, 197, 253, 0.6)', // Light blue
        borderColor: 'rgba(147, 197, 253, 1)',
        borderWidth: 2,
        borderRadius: 8,
        borderSkipped: false,
        hoverBackgroundColor: 'rgba(147, 197, 253, 0.8)',
        hoverBorderColor: 'rgba(96, 165, 250, 1)',
        hoverBorderWidth: 3,
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
    plugins: {
      legend: {
        display: true,
        position: 'top' as const,
        align: 'end' as const,
        labels: {
          usePointStyle: true,
          pointStyle: 'circle' as const,
          padding: 20,
          font: {
            family: 'Inter, sans-serif',
            size: 13,
            weight: 600
          },
          color: '#64748B'
        }
      },
      tooltip: {
        backgroundColor: 'rgba(15, 23, 42, 0.95)',
        titleColor: '#F1F5F9',
        bodyColor: '#F1F5F9',
        titleFont: {
          family: 'Inter, sans-serif',
          size: 14,
          weight: 700
        },
        bodyFont: {
          family: 'Inter, sans-serif',
          size: 13,
          weight: 500
        },
        padding: 14,
        cornerRadius: 10,
        displayColors: true,
        boxWidth: 12,
        boxHeight: 12,
        boxPadding: 6,
        borderColor: 'rgba(99, 102, 241, 0.3)',
        borderWidth: 1
      }
    },
    scales: {
      x: {
        grid: {
          display: false,
          drawBorder: false
        },
        ticks: {
          font: {
            family: 'Inter, sans-serif',
            size: 12,
            weight: 500
          },
          color: '#94A3B8',
          padding: 10
        }
      },
      y: {
        beginAtZero: true,
        grid: {
          color: 'rgba(226, 232, 240, 0.5)',
          drawBorder: false,
          lineWidth: 1
        },
        border: {
          display: false,
          dash: [5, 5]
        },
        ticks: {
          font: {
            family: 'Inter, sans-serif',
            size: 12,
            weight: 500
          },
          color: '#94A3B8',
          padding: 12,
          stepSize: 20
        }
      }
    },
    interaction: {
      intersect: false,
      mode: 'index' as const
    },
    animation: {
      duration: 800,
      easing: 'easeInOutQuart' as const
    }
  } as any

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
.modern-dashboard {
  padding: 0;
}

/* Stats Grid */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 24px;
  margin-bottom: 24px;
}

.stat-card {
  background: white;
  border-radius: 16px;
  padding: 28px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
  position: relative;
  overflow: hidden;
  transition: all 0.3s ease;
  border: 1px solid rgba(0, 0, 0, 0.05);
}

.stat-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.1);
}

.stat-card.gradient-primary {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
}

.stat-card.white {
  background: white;
}

.stat-header {
  display: flex;
  justify-content: flex-end;
  align-items: flex-start;
  margin-bottom: 20px;
}

.stat-content {
  flex: 1;
}

.stat-label {
  font-size: 14px;
  font-weight: 600;
  margin-bottom: 12px;
  color: #64748B;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.stat-card.gradient-primary .stat-label {
  color: rgba(255, 255, 255, 0.95);
}

.stat-value {
  font-size: 36px;
  font-weight: 700;
  margin-bottom: 4px;
  line-height: 1.2;
  letter-spacing: -0.5px;
}

.stat-value.dark {
  color: #1E293B;
}

.stat-badge {
  padding: 8px 14px;
  border-radius: 10px;
  font-size: 12px;
  font-weight: 600;
  white-space: nowrap;
  transition: all 0.3s ease;
  cursor: pointer;
  position: absolute;
  top: 24px;
  right: 24px;
}

.stat-badge.success {
  background: rgba(16, 185, 129, 0.1);
  color: #10B981;
}

.stat-badge.success:hover {
  background: rgba(16, 185, 129, 0.15);
}

.stat-card.gradient-primary .stat-badge {
  background: rgba(255, 255, 255, 0.25);
  color: white;
  backdrop-filter: blur(10px);
}

/* Charts Grid */
.charts-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
  gap: 24px;
  margin-bottom: 24px;
}

.chart-card {
  background: white;
  border-radius: 16px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
  overflow: hidden;
  transition: all 0.3s ease;
  border: 1px solid rgba(0, 0, 0, 0.05);
}

.chart-card:hover {
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
}

.card-header {
  padding: 20px 24px;
  border-bottom: 1px solid #F1F5F9;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: linear-gradient(to bottom, #FAFBFC 0%, #FFFFFF 100%);
}

.card-title {
  font-size: 17px;
  font-weight: 700;
  color: #1E293B;
  margin: 0;
  letter-spacing: -0.3px;
}

.card-tools {
  display: flex;
  gap: 8px;
}

.tool-button {
  width: 32px;
  height: 32px;
  border-radius: 8px;
  border: 1px solid #E2E8F0;
  background: white;
  color: #64748B;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.2s ease;
}

.tool-button:hover {
  background: #F8FAFC;
  border-color: #CBD5E1;
  color: #475569;
  transform: scale(1.05);
}

.card-body {
  padding: 24px;
}

/* Responsive */
@media (max-width: 1200px) {
  .charts-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  .stats-grid {
    grid-template-columns: 1fr;
  }
  
  .modern-dashboard {
    padding: 16px;
  }
  
  .stat-card {
    padding: 24px;
  }
  
  .stat-value {
    font-size: 30px;
  }
}

@media (max-width: 640px) {
  .charts-grid {
    grid-template-columns: 1fr;
  }
}
</style>
