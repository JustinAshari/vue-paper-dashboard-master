<template>
  <div>
    <!-- Order Table -->
    <div class="order-table">
      <table class="table table-striped">
        <thead>
          <tr>
            <th>Order No</th>
            <th>Nama</th>
            <th>Pesanan</th>
            <th>Jumlah Pesanan</th>
            <th>Pembayaran</th>
            <th>Nominal</th>
            <th>Alamat</th>
            <th>Tanggal Pemesanan</th>
            <th>Status</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="order in orders" :key="order.orderNo">
            <td>{{ order.orderNo }}</td>
            <td>{{ order.nama }}</td>
            <td>{{ order.pesanan }}</td>
            <td>{{ order.jumlahPesanan }}</td>
            <td>{{ order.pembayaran }}</td>
            <td>{{ order.nominal }}</td>
            <td>{{ order.alamat }}</td>
            <td>{{ order.tanggalPemesanan }}</td>
            <td>{{ order.status }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      orders: [
        {
          orderNo: "1",
          nama: "John Doe",
          pesanan: "Wanpaku Sandwich",
          jumlahPesanan: 2,
          pembayaran: "Transfer",
          nominal: "Rp 24,000",
          alamat: "Jl. Example No. 123, Solo",
          tanggalPemesanan: "2024-10-27",
          status: "Selesai",
        },
        {
          orderNo: "2",
          nama: "Jane Smith",
          pesanan: "Fruit Sando",
          jumlahPesanan: 1,
          pembayaran: "Transfer",
          nominal: "Rp 10,000",
          alamat: "Jl. Another St. 456, Solo",
          tanggalPemesanan: "2024-10-27",
          status: "Selesai",
        },
        {
          orderNo: "3",
          nama: "Budi Santoso",
          pesanan: "Wanpaku Sandwich",
          jumlahPesanan: 3,
          pembayaran: "Tunai",
          nominal: "Rp 36,000",
          alamat: "Jl. Merdeka No. 789, Solo",
          tanggalPemesanan: "2024-10-28",
          status: "Selesai",
        },
        {
          orderNo: "4",
          nama: "Siti Aminah",
          pesanan: "Fruit Sando",
          jumlahPesanan: 2,
          pembayaran: "Transfer",
          nominal: "Rp 20,000",
          alamat: "Jl. Diponegoro No. 101, Solo",
          tanggalPemesanan: "2024-10-28",
          status: "Selesai",
        },
        {
          orderNo: "5",
          nama: "Ali Wijaya",
          pesanan: "Wanpaku Sandwich",
          jumlahPesanan: 1,
          pembayaran: "Tunai",
          nominal: "Rp 12,000",
          alamat: "Jl. Slamet Riyadi No. 303, Solo",
          tanggalPemesanan: "2024-10-29",
          status: "Pending",
        },
        {
          orderNo: "6",
          nama: "Cici Andriani",
          pesanan: "Fruit Sando",
          jumlahPesanan: 2,
          pembayaran: "Transfer",
          nominal: "Rp 20,000",
          alamat: "Jl. Kartini No. 505, Solo",
          tanggalPemesanan: "2024-10-29",
          status: "Pending",
        },
        {
          orderNo: "7",
          nama: "Dina Safitri",
          pesanan: "Wanpaku Sandwich",
          jumlahPesanan: 3,
          pembayaran: "Transfer",
          nominal: "Rp 36,000",
          alamat: "Jl. Sudirman No. 606, Solo",
          tanggalPemesanan: "2024-10-29",
          status: "Pending",
        },
      ],
    };
  },
};
</script>


<style>
.order-table {
  margin-top: 20px;
}
.table {
  width: 100%;
  border-collapse: collapse;
}
.table th,
.table td {
  padding: 10px;
  text-align: left;
  border: 1px solid #ddd;
}
.table th {
  background-color: #f2f2f2;
}
</style>
