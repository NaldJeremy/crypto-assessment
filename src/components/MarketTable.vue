<template>
  <div class="market-table">
    <div style="display: flex; align-items: flex-end">
      <div>
        <h2>Favorit</h2>
      </div>
      <div class="tabs">
        <span
          v-for="tab in tabs"
          :key="tab"
          :class="{ active: activeTab === tab }"
          @click="activeTab = tab"
        >
          {{ tab }}
        </span>
      </div>
    </div>
    <table>
      <thead>
        <tr>
          <th></th>
          <th class="table-connect" @click="sortTable('pair')">Pasangan</th>
          <th @click="sortTable('lastPrice')">Harga Terakhir</th>
          <th @click="sortTable('change24h')">Perubahan 24jam</th>
          <th @click="sortTable('highLow24h')">Tertinggi / Terendah 24jam</th>
          <th @click="sortTable('marketCap')">Kapitalisasi Pasar</th>
          <th @click="sortTable('volume24h')">Volume 24 Jam</th>
        </tr>
      </thead>
      <tbody class="table-data">
        <tr v-for="(market, index) in sortedMarkets" :key="index">
          <td @click="toggleFavorite(index)">
            <img
              :src="market.favorite ? favOn : favOff"
              alt="Fav Icon"
              class="fav-icon"
            />
          </td>
          <td>{{ market.pair }}</td>
          <td>{{ market.lastPrice }}</td>
          <td :class="market.change24h > 0 ? 'positive' : 'negative'">
            {{ market.change24h }}%
          </td>
          <td>{{ market.highLow24h }}</td>
          <td>{{ market.marketCap }}</td>
          <td>{{ market.volume24h }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import favOn from "@/assets/Fav-on.png";
import favOff from "@/assets/Fav-off.png";

export default {
  name: "MarketTable",
  data() {
    return {
      activeTab: "IDR",
      tabs: ["IDR", "USD", "BNB", "BTC", "ALTS"],
      sortKey: "",
      sortOrder: "asc",
      markets: [
        {
          pair: "BTC/DAI",
          lastPrice: "98,832.93 / Rp 1,612,213,281.72",
          change24h: 3.89,
          highLow24h: "102,451.34 / Rp 94,288.07",
          marketCap: "Rp 31,953.008T",
          volume24h: "1.538M",
          favorite: true,
        },
        {
          pair: "ETH/DAI",
          lastPrice: "98,832.93 / Rp 1,612,213,281.72",
          change24h: 3.89,
          highLow24h: "102,451.34 / Rp 94,288.07",
          marketCap: "Rp 31,953.008T",
          volume24h: "1.538M",
          favorite: false,
        },
        {
          pair: "XRP/ETH",
          lastPrice: "98,832.93 / Rp 1,612,213,281.72",
          change24h: -3.89,
          highLow24h: "102,451.34 / Rp 94,288.07",
          marketCap: "Rp 31,953.008T",
          volume24h: "1.538M",
          favorite: false,
        },
        {
          pair: "BTC/DAI",
          lastPrice: "98,832.93 / Rp 1,612,213,281.72",
          change24h: 3.89,
          highLow24h: "102,451.34 / Rp 94,288.07",
          marketCap: "Rp 31,953.008T",
          volume24h: "1.538M",
          favorite: false,
        },
        {
          pair: "BTC/DAI",
          lastPrice: "98,832.93 / Rp 1,612,213,281.72",
          change24h: 3.89,
          highLow24h: "102,451.34 / Rp 94,288.07",
          marketCap: "Rp 31,953.008T",
          volume24h: "1.538M",
          favorite: false,
        },
      ],
    };
  },
  computed: {
    sortedMarkets() {
      if (!this.sortKey) return this.markets;
      return [...this.markets].sort((a, b) => {
        let result = 0;
        if (typeof a[this.sortKey] === "string") {
          result = a[this.sortKey].localeCompare(b[this.sortKey]);
        } else {
          result = a[this.sortKey] - b[this.sortKey];
        }
        return this.sortOrder === "asc" ? result : -result;
      });
    },
  },
  methods: {
    toggleFavorite(index) {
      this.markets[index].favorite = !this.markets[index].favorite;
    },
    sortTable(key) {
      if (this.sortKey === key) {
        this.sortOrder = this.sortOrder === "asc" ? "desc" : "asc";
      } else {
        this.sortKey = key;
        this.sortOrder = "asc";
      }
    },
  },
};
</script>

<style scoped>
.market-table {
  width: 100%;
  margin-top: 20px;
  padding: 20px;
  border-radius: 12px;

  color: white;
}

.market-table h2 {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 10px;
}

.market-table table {
  width: 100%;
  border-collapse: collapse;
  font-size: 14px;
}

.market-table thead {
  background: transparent;
}

.market-table th {
  text-align: right;
  padding: 12px 16px;
  font-weight: 600;
  color: #b0b0b0;
  font-size: 14px;
}

.market-table td {
  padding: 12px 16px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.market-table tr:hover {
  background: rgba(255, 255, 255, 0.05);
}

.market-table .positive {
  color: #00ff00;
}

.market-table .negative {
  color: #ff4d4d;
}

.market-table img {
  width: 18px;
  height: 18px;
  margin-right: 8px;
  vertical-align: middle;
}

/* Styling for the Favorite Icon */
.favorite-icon {
  width: 20px;
  height: 20px;
  cursor: pointer;
}

.market-table tbody tr td:first-child {
  display: flex;
  align-items: center;
}

.market-table tbody tr:hover {
  background: rgba(255, 255, 255, 0.08);
}

.table-data {
  text-align: right;
}

@media (max-width: 1024px) {
  .market-table table {
    font-size: 12px;
  }
  .market-table th,
  .market-table td {
    padding: 10px;
  }
}
</style>
