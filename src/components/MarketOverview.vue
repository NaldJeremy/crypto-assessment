<template>
  <section class="market-overview text-white px-6">
    <div class="hero-content mb-8">
      <h1 class="text-5xl font-bold">Pasar</h1>
      <p class="text-gray-400 text-lg">
        Harga Kripto dalam Rupiah Hari ini di Market Terbesar Indonesia
      </p>
    </div>

    <!-- Market Cards -->
    <div class="cards-container">
      <div class="market-card" v-for="(market, index) in markets" :key="index">
        <div class="market-details">
          <h3 class="market-name">{{ market.name }}</h3>
          <p class="market-price">Rp {{ market.price }}</p>
          <p :class="market.change > 0 ? 'change-positive' : 'change-negative'">
            {{ market.change > 0 ? "+" + market.change : market.change }}%
          </p>
        </div>
        <div class="market-graph">
          <div class="chart">
            <canvas :id="'chart-' + index" class="chart"></canvas>
          </div>
          <div>
            <p class="market-volume">Volume: {{ market.volume }} IDR</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { Chart, registerables } from "chart.js";
Chart.register(...registerables);

export default {
  name: "MarketOverview",
  data() {
    return {
      markets: [
        {
          name: "TKO/IDR",
          price: "5,261.3",
          change: 3.82,
          volume: "2,258",
          trend: [10, 8, 6, 7, 5],
        },
        {
          name: "TKO/IDR",
          price: "5,261.3",
          change: -3.82,
          volume: "2,258",
          trend: [10, 8, 6, 7, 5],
        },
        {
          name: "TKO/IDR",
          price: "5,261.3",
          change: 3.82,
          volume: "2,258",
          trend: [10, 8, 6, 7, 5],
        },
        {
          name: "IDN/IDR",
          price: "5,261.3",
          change: -3.82,
          volume: "2,258",
          trend: [10, 8, 6, 7, 5],
        },
      ],
    };
  },
  mounted() {
    this.$nextTick(() => {
      this.renderCharts();
    });
  },
  methods: {
    renderCharts() {
      this.markets.forEach((market, index) => {
        const canvas = document.getElementById(`chart-${index}`);
        if (canvas) {
          const ctx = canvas.getContext("2d");

          // Clear previous chart instance if it exists
          if (canvas.chartInstance) {
            canvas.chartInstance.destroy();
          }

          canvas.chartInstance = new Chart(ctx, {
            type: "line",
            data: {
              labels: ["Day 1", "Day 2", "Day 3", "Day 4", "Day 5"],
              datasets: [
                {
                  data: market.trend,
                  borderColor: market.change > 0 ? "#22c55e" : "#ef4444",
                  fill: false,
                  borderWidth: 2.5,
                  tension: 0.3,
                },
              ],
            },
            options: {
              responsive: true,
              maintainAspectRatio: false,
              scales: { x: { display: false }, y: { display: false } },
              plugins: { legend: { display: false } },
            },
          });
        }
      });
    },
  },
};
</script>

<style scoped>
/* Section Background */
.market-overview {
  padding: 1rem 0;
}

/* Market Cards Container */
.cards-container {
  display: flex;
  justify-content: center;
  gap: 2rem;
  flex-wrap: wrap;
}

/* Market Card */
.market-card {
  background: rgba(20, 20, 20, 0.95);
  border-radius: 12px;
  padding: 16px;
  width: 260px;
  height: 130px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  transition: transform 0.3s ease-in-out;
}

.market-card:hover {
  transform: scale(1.05);
  box-shadow: 0 4px 25px rgba(255, 255, 255, 0.2);
}

/* Market Details */
.market-name {
  font-size: 0.85rem;
  font-weight: 500;
  color: #cbd5e1;
}

.market-price {
  font-size: 20px;
  font-weight: bold;
  color: #fff;
}

.change-positive {
  color: #22c55e;
}

.change-negative {
  color: #ef4444;
}

.market-graph .chart {
  width: 99% !important; /* Ensure it takes full width */
  height: 80px !important; /* Adjust height */
}

.chart {
  gap: 2rem;
}
/* Market Volume */
.market-volume {
  font-size: 0.8rem;
  color: #949494;
  text-align: right;
}

@media (min-width: 1024px) {
  .cards-container {
    display: flex;
    flex-wrap: nowrap; /* Prevents wrapping */
    justify-content: space-between; /* Even spacing */
    gap: 20px; /* Adds spacing between cards */
  }

  .market-card {
    width: 22%; /* Ensures four cards fit in one row */
    min-width: 230px;
    max-width: 260px;
    height: 140px; /* Adjust card height */
  }

  .market-graph {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem; /* Adds spacing between graph and volume text */
  }

  .market-graph .chart {
    width: 99% !important;
    height: 60px !important; /* Ensures smaller chart */
  }

  .market-volume {
    font-size: 0.8rem;
    color: #949494;
    text-align: center;
  }

  /* Adjustments for better UI on large screens */
  .market-details {
    padding-bottom: 5px; /* Adds space between price and graph */
  }
}

@media (min-width: 425px) {
  .market-card {
    width: 29rem;
  }
}
</style>
