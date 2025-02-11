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
          <th
            class="cursor-pointer flex items-center"
            @click="sortTable('pair')"
            style="text-align: left"
          >
            Pasangan
            <span v-if="sortKey === 'pair'">
              <i
                :class="[
                  sortOrder === 'asc' ? 'fa fa-arrow-up' : 'fa fa-arrow-down',
                  'sort-icon',
                  sortKey === 'pair' ? 'active' : '',
                ]"
              ></i>
            </span>
          </th>
          <th></th>
          <th
            class="cursor-pointer flex items-center"
            @click="sortTable('lastPrice')"
          >
            Harga Terakhir
            <span v-if="sortKey === 'lastPrice'">
              <i
                :class="[
                  sortOrder === 'asc' ? 'fa fa-arrow-up' : 'fa fa-arrow-down',
                  'sort-icon',
                  sortKey === 'lastPrice' ? 'active' : '',
                ]"
              ></i>
            </span>
          </th>
          <th
            class="cursor-pointer flex items-center"
            @click="sortTable('change24h')"
          >
            Perubahan 24jam
            <span v-if="sortKey === 'change24h'">
              <i
                :class="[
                  sortOrder === 'asc' ? 'fa fa-arrow-up' : 'fa fa-arrow-down',
                  'sort-icon',
                  sortKey === 'change24h' ? 'active' : '',
                ]"
              ></i>
            </span>
          </th>
          <th
            class="cursor-pointer flex items-center"
            @click="sortTable('highLow24h')"
          >
            Tertinggi / Terendah 24jam
            <span v-if="sortKey === 'highLow24h'">
              <i
                :class="[
                  sortOrder === 'asc' ? 'fa fa-arrow-up' : 'fa fa-arrow-down',
                  'sort-icon',
                  sortKey === 'highLow24h' ? 'active' : '',
                ]"
              ></i>
            </span>
          </th>
          <th
            class="cursor-pointer flex items-center"
            @click="sortTable('marketCap')"
          >
            Kapitalisasi Pasar
            <span v-if="sortKey === 'marketCap'">
              <i
                :class="[
                  sortOrder === 'asc' ? 'fa fa-arrow-up' : 'fa fa-arrow-down',
                  'sort-icon',
                  sortKey === 'marketCap' ? 'active' : '',
                ]"
              ></i>
            </span>
          </th>
          <th
            class="cursor-pointer flex items-center"
            @click="sortTable('volume24h')"
          >
            Volume 24 Jam
            <span v-if="sortKey === 'volume24h'">
              <i
                :class="[
                  sortOrder === 'asc' ? 'fa fa-arrow-up' : 'fa fa-arrow-down',
                  'sort-icon',
                  sortKey === 'volume24h' ? 'active' : '',
                ]"
              ></i>
            </span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(market, index) in sortedMarkets" :key="index">
          <td @click="toggleFavorite(index)">
            <svg
              :class="market.favorite ? 'fav-icon active' : 'fav-icon'"
              viewBox="0 0 24 24"
              width="24"
              height="24"
              fill="currentColor"
            >
              <path
                v-if="market.favorite"
                d="M12 17.75L5.5 21l1.25-7.25L2 9l7.25-1L12 2l2.75 6L22 9l-4.75 4.75L18.5 21z"
              />
              <path
                v-else
                d="M12 2l2.75 6L22 9l-4.75 4.75L18.5 21 12 17.75 5.5 21l1.25-7.25L2 9l7.25-1z"
                stroke="currentColor"
                stroke-width="2"
                fill="none"
              />
            </svg>
          </td>
          <td>{{ market.pair }}</td>
          <td>{{ market.lastPrice }}</td>
          <td :class="market.change24h > 0 ? 'positive' : 'negative'">
            {{
              market.change24h > 0 ? "+" + market.change24h : market.change24h
            }}%
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
          lastPrice: "98,832.93",
          change24h: +3.89,
          highLow24h: "102,451.34 / Rp 94,288.07",
          marketCap: "Rp 31,953.008T",
          volume24h: "1.538M",
          favorite: true,
        },
        {
          pair: "ETH/DAI",
          lastPrice: "98,832.93",
          change24h: +3.89,
          highLow24h: "102,451.34 / Rp 94,288.07",
          marketCap: "Rp 31,953.008T",
          volume24h: "1.538M",
          favorite: false,
        },
        {
          pair: "XRP/ETH",
          lastPrice: "98,832.93",
          change24h: -3.89,
          highLow24h: "102,451.34 / Rp 94,288.07",
          marketCap: "Rp 31,953.008T",
          volume24h: "1.538M",
          favorite: false,
        },
        {
          pair: "BTC/DAI",
          lastPrice: "98,832.93",
          change24h: +3.89,
          highLow24h: "102,451.34 / Rp 94,288.07",
          marketCap: "Rp 31,953.008T",
          volume24h: "1.538M",
          favorite: false,
        },
        {
          pair: "BTC/DAI",
          lastPrice: "98,832.93",
          change24h: +3.89,
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
      return [...this.markets]
        .sort((a, b) => b.favorite - a.favorite)
        .sort((a, b) => {
          if (!this.sortKey) return 0;
          let result =
            typeof a[this.sortKey] === "string"
              ? a[this.sortKey].localeCompare(b[this.sortKey])
              : a[this.sortKey] - b[this.sortKey];
          return this.sortOrder === "asc" ? result : -result;
        });
    },
  },
  methods: {
    toggleFavorite(index) {
      this.markets[index].favorite = !this.markets[index].favorite;
    },
    sortTable(key) {
      this.sortOrder =
        this.sortKey === key
          ? this.sortOrder === "asc"
            ? "desc"
            : "asc"
          : "asc";
      this.sortKey = key;
    },
  },
};
</script>

<style scoped>
.sort-icon {
  margin-left: 5px;
  color: white;
}
.sort-icon.active {
  color: #fbb05b;
}
.fav-icon {
  width: 24px;
  height: 24px;
  cursor: pointer;
  transition: fill 0.3s ease;
  fill: white;
}
.fav-icon.active {
  fill: #fbb05b;
}
</style>
