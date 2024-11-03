<template>
  <div class="row">
    <div class="col-md-6 col-12">
      <Ringkasan-Penjualan> </Ringkasan-Penjualan>
    </div>
    <div class="col-md-6 col-12">
      <Statistik-Produk> </Statistik-Produk>
    </div>
  </div>
</template>
<script>
import RingkasanPenjualan from "./Dashboard/RingkasanPenjualan.vue";
import StatistikProduk from "./Dashboard/StatistikProduk.vue";
export default {
  components: {
    RingkasanPenjualan,
    StatistikProduk,
  },
};
</script>
<style></style>
