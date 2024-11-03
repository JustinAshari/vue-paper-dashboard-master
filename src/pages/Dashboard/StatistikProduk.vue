<template>
  <div>
    <!-- Product Statistics for Pre-Order -->
    <div class="product-statistics">
      <h3>Statistik Produk (Pre-order)</h3>
      <p><strong>Total Produk Terlaris:</strong></p>
      <ul>
        <li v-for="(item, index) in produkTerlaris" :key="index">
          {{ item.produk }} - {{ item.jumlah }} unit dipesan
        </li>
      </ul>
      <p><strong>Jumlah Produk Aktif:</strong> {{ jumlahProdukAktif }}</p>
      <p><strong>Produk Populer:</strong> {{ produkPopuler }}</p>
      <p><strong>Jumlah Pesanan Selesai (berdasarkan unit):</strong></p>
      <ul>
        <li>Wanpaku Sandwich - {{ jumlahPesananSelesai.wanpaku }} unit</li>
        <li>Fruit Sando - {{ jumlahPesananSelesai.fruitSando }} unit</li>
      </ul>
      <p><strong>Jumlah Pesanan Pending (berdasarkan unit):</strong></p>
      <ul>
        <li>Wanpaku Sandwich - {{ jumlahPesananPending.wanpaku }} unit</li>
        <li>Fruit Sando - {{ jumlahPesananPending.fruitSando }} unit</li>
      </ul>
    </div>
  </div>
</template>

<style>
.product-statistics {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  max-width: 500px;
  margin: auto;
}
</style>

<script>
export default {
  data() {
    return {
      orders: [
        { orderNo: "1", nama: "John Doe", pesanan: "Wanpaku Sandwich", jumlahPesanan: 2, pembayaran: "Transfer", nominal: "Rp 24,000", alamat: "Jl. Example No. 123, Solo", tanggalPemesanan: "2024-10-27", status: "Selesai" },
        { orderNo: "2", nama: "Jane Smith", pesanan: "Fruit Sando", jumlahPesanan: 1, pembayaran: "Transfer", nominal: "Rp 10,000", alamat: "Jl. Another St. 456, Solo", tanggalPemesanan: "2024-10-27", status: "Selesai" },
        { orderNo: "3", nama: "Budi Santoso", pesanan: "Wanpaku Sandwich", jumlahPesanan: 3, pembayaran: "Tunai", nominal: "Rp 36,000", alamat: "Jl. Merdeka No. 789, Solo", tanggalPemesanan: "2024-10-28", status: "Selesai" },
        { orderNo: "4", nama: "Siti Aminah", pesanan: "Fruit Sando", jumlahPesanan: 2, pembayaran: "Transfer", nominal: "Rp 20,000", alamat: "Jl. Diponegoro No. 101, Solo", tanggalPemesanan: "2024-10-28", status: "Selesai" },
        { orderNo: "5", nama: "Ali Wijaya", pesanan: "Wanpaku Sandwich", jumlahPesanan: 1, pembayaran: "Tunai", nominal: "Rp 12,000", alamat: "Jl. Slamet Riyadi No. 303, Solo", tanggalPemesanan: "2024-10-29", status: "Pending" },
        { orderNo: "6", nama: "Cici Andriani", pesanan: "Fruit Sando", jumlahPesanan: 2, pembayaran: "Transfer", nominal: "Rp 20,000", alamat: "Jl. Kartini No. 505, Solo", tanggalPemesanan: "2024-10-29", status: "Pending" },
        { orderNo: "7", nama: "Dina Safitri", pesanan: "Wanpaku Sandwich", jumlahPesanan: 3, pembayaran: "Transfer", nominal: "Rp 36,000", alamat: "Jl. Sudirman No. 606, Solo", tanggalPemesanan: "2024-10-29", status: "Pending" },
      ],
      products: [
        { nama: "Wanpaku Sandwich" },
        { nama: "Fruit Sando" },
      ],
    };
  },

  computed: {
    // Produk Terlaris: Berdasarkan jumlah total unit pesanan
    produkTerlaris() {
      const produkCount = {};
      this.orders.forEach(order => {
        const produk = order.pesanan;
        produkCount[produk] = (produkCount[produk] || 0) + order.jumlahPesanan;
      });

      return Object.entries(produkCount)
        .sort((a, b) => b[1] - a[1])
        .map(([produk, jumlah]) => ({ produk, jumlah }));
    },

    // Jumlah Produk Aktif: Total produk yang tersedia untuk pre-order
    jumlahProdukAktif() {
      return this.products.length;
    },

    // Produk Populer: Produk yang paling sering dipesan
    produkPopuler() {
      return this.produkTerlaris[0] ? this.produkTerlaris[0].produk : "Tidak ada data";
    },

    // Jumlah unit Pesanan Selesai berdasarkan produk
    jumlahPesananSelesai() {
      return {
        wanpaku: this.orders
          .filter(order => order.pesanan === "Wanpaku Sandwich" && order.status === "Selesai")
          .reduce((total, order) => total + order.jumlahPesanan, 0),
        fruitSando: this.orders
          .filter(order => order.pesanan === "Fruit Sando" && order.status === "Selesai")
          .reduce((total, order) => total + order.jumlahPesanan, 0),
      };
    },

    // Jumlah unit Pesanan Pending berdasarkan produk
    jumlahPesananPending() {
      return {
        wanpaku: this.orders
          .filter(order => order.pesanan === "Wanpaku Sandwich" && order.status === "Pending")
          .reduce((total, order) => total + order.jumlahPesanan, 0),
        fruitSando: this.orders
          .filter(order => order.pesanan === "Fruit Sando" && order.status === "Pending")
          .reduce((total, order) => total + order.jumlahPesanan, 0),
      };
    },
  },
};
</script>
