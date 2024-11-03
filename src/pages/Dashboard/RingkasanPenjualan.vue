<template>
  <div>
    <!-- Sales Overview -->
    <div class="sales-overview">
      <h3>Ringkasan Penjualan</h3>
      <p><strong>Total Pendapatan:</strong> {{ totalPendapatan }}</p>
      <p><strong>Jumlah Pesanan:</strong> {{ jumlahPesanan }} Orang</p>
      <p><strong>Pesanan Selesai:</strong> {{ pesananSelesai }} Orang</p>
      <p><strong>Pesanan Baru:</strong> {{ pesananBaru }} Orang</p>
      <p><strong>Pendapatan Per Produk:</strong></p>
      <ul>
        <li v-for="(revenue, product) in pendapatanPerProduk" :key="product">
          {{ product }}: {{ revenue }}
        </li>
      </ul>
      <p><strong>Metode Pembayaran Populer:</strong> {{ metodePembayaranPopuler }}</p>
    </div>
  </div>
</template>



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
    };
  },
  computed: {
    // Total Pendapatan dari semua pesanan yang berhasil (status: "Selesai")
    totalPendapatan() {
      return this.orders
        .filter(order => order.status === "Selesai")
        .reduce((total, order) => total + parseInt(order.nominal.replace(/[^0-9]/g, ""), 10), 0)
        .toLocaleString("id-ID", { style: "currency", currency: "IDR" });
    },

    // Jumlah total pesanan
    jumlahPesanan() {
      return this.orders.length;
    },

    // Pesanan Selesai
    pesananSelesai() {
      return this.orders.filter(order => order.status === "Selesai").length;
    },

    // Pesanan Baru (Pending)
    pesananBaru() {
      return this.orders.filter(order => order.status === "Pending").length;
    },

    // Pendapatan Per Produk
    pendapatanPerProduk() {
      const revenuePerProduct = {};
      this.orders.forEach(order => {
        if (order.status === "Selesai") {
          const productName = order.pesanan;
          const nominal = parseInt(order.nominal.replace(/[^0-9]/g, ""), 10);
          revenuePerProduct[productName] = (revenuePerProduct[productName] || 0) + nominal;
        }
      });
      // Format nilai dalam format mata uang Indonesia
      Object.keys(revenuePerProduct).forEach(key => {
        revenuePerProduct[key] = revenuePerProduct[key].toLocaleString("id-ID", { style: "currency", currency: "IDR" });
      });
      return revenuePerProduct;
    },

    // Metode Pembayaran Populer
    metodePembayaranPopuler() {
      const paymentMethods = {};
      this.orders.forEach(order => {
        paymentMethods[order.pembayaran] = (paymentMethods[order.pembayaran] || 0) + 1;
      });
      const sortedMethods = Object.entries(paymentMethods).sort((a, b) => b[1] - a[1]);
      return sortedMethods[0] ? sortedMethods[0][0] : "Tidak ada data";
    },
  },
};
</script>

<style>
.sales-overview {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  max-width: 500px;
  margin: auto;
}
</style>
