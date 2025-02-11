<template>
  <div id="app">
    <Navbar />
    <header class="container hero-section"></header>
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
