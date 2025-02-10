<template>
  <div id="app">
    <Navbar />
    <header class="container hero-section">
      <!-- <div class="hero-content">
        <h1>Pasar</h1>
        <p>Harga Kripto dalam Rupiah Hari ini di Market Terbesar Indonesia</p>
      </div> -->
    </header>
    <main class="container">
      <MarketOverview />
      <MarketTable />
    </main>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import MarketOverview from "./components/MarketOverview.vue";
import MarketTable from "./components/MarketTable.vue";
import "./style.css";

export default {
  components: {
    Navbar,
    MarketOverview,
    MarketTable,
  },
};
</script>
