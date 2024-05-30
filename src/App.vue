<template>
  <q-layout view="hHh lpR fFf">
    <!-- Header -->
    <q-header elevated class="bg-black text-white" height-hint="98">
      <q-input
        outlined
        rounded
        dense
        placeholder="Cari Produk..."
        class="q-ml-md q-mr-md"
        aria-label="Cari Produk"
      >
        <template v-slot:append>
          <q-icon name="search" />
        </template>
      </q-input>
      <q-space />
      <q-tabs align="left" class="text-white bg-primary">
        <q-tab v-for="(tab, index) in tabs" :key="index" :label="tab" />
      </q-tabs>
    </q-header>

    <!-- Carousel -->
    <q-page-container>
      <q-carousel
        v-model="slide"
        swipeable
        animated
        infinite
        autoplay
        autoplay-interval="5000"
        class="bg-grey-2"
        height="400px"
        aria-roledescription="carousel"
      >
        <q-carousel-slide
          v-for="(slide, index) in slides"
          :key="index"
          :name="index"
          :img-src="slide.img"
        >
          <div class="absolute-bottom text-center text-white q-pa-md overlay-text">
            <h4>RIZA UMAMI AYMAN</h4>
          </div>
        </q-carousel-slide>
      </q-carousel>

      <!-- Product Cards -->
      <div class="row q-pa-md card-list">
        <q-card v-for="product in products" :key="product.id" class="q-mb-md product-card">
          <q-img :src="product.img" :alt="product.name" />
          <q-card-section>
            <q-card-title>{{ product.name }}</q-card-title>
            <q-card-subtitle>{{ product.price }}</q-card-subtitle>
            <q-rating size="20px" value="4" readonly class="q-mb-sm" />
            <div class="row justify-between">
              <q-btn outline color="primary" label="Add to Cart" />
              <q-btn flat color="primary" label="View Details" />
              <q-btn flat color="negative" label="Delete" @click="deleteProduct(product.id)" />
            </div>
          </q-card-section>
        </q-card>
      </div>
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  data() {
    return {
      slide: 0,
      tabs: ["ATASAN", "LUARAN", "BAWAHAN", "TAS", "TOPI", "DASI", "AKSESORIS", "KAOS KAKI", "OUTDOOR", "ANAK", "MUSLIM"],
      slides: [
        { img: 'https://highlight.id/wp-content/uploads/2018/07/merek-fashion-branded-lokal-indonesia-produk-koleksi-pakaian-baju-cewek-terbaru-keren-ngehits_03.jpg' },
        { img: 'https://asset-2.tstatic.net/surabaya/foto/bank/images/ilustrasi-baju.jpg' },
        { img: 'https://asset.kompas.com/crops/x3g2zpraz3io8LV8NoEcIf9Yv_g=/0x0:5472x3648/750x500/data/photo/2022/03/26/623eec09cb861.jpg' },
      ],
      products: [
        { id: 1, name: 'Cardigan Rajut', price: 'Rp 100.000', img: 'https://i.pinimg.com/564x/5d/48/f8/5d48f8934a33039178e32cb362a65fa3.jpg' },
        { id: 2, name: 'Celana Jeans', price: 'Rp 200.000', img: 'https://i.pinimg.com/564x/dd/4d/1e/dd4d1ecf8db6974079a09062a61f2890.jpg' },
        { id: 3, name: 'Kemeja', price: 'Rp 300.000', img: 'https://i.pinimg.com/564x/4f/bc/ef/4fbcef586b85f966729e7c9c0518252f.jpg' },
        { id: 4, name: 'Totebag', price: 'Rp 130.000', img: 'https://i.pinimg.com/736x/4e/50/f6/4e50f647bd35fee2186671a71ef766a5.jpg' },
        { id: 5, name: 'Tas Selempang', price: 'Rp 140.000', img: 'https://i.pinimg.com/564x/4f/54/35/4f54354ef47575b54d2f4f89e43ed402.jpg' },
        { id: 6, name: 'Totebag', price: 'Rp 500.000', img: 'https://i.pinimg.com/564x/1e/67/3a/1e673a4a3d23bbf76862da4f4ed46eff.jpg' },
      ],
    }
  },
  methods: {
    deleteProduct(id) {
      this.products = this.products.filter(product => product.id !== id);
    }
  }
}
</script>

<style>
.row {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.q-pa-md {
  padding: 16px;
}
.card-list {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: center;
}
.product-card {
  width: calc(33% - 16px);
  min-width: 250px;
  transition: transform 0.3s, box-shadow 0.3s;
}
.product-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 12px 20px rgba(0, 0, 0, 0.2);
}
.overlay-text {
  background-color: rgba(0, 0, 0, 0.6);
  padding: 10px;
}
@media (max-width: 768px) {
  .product-card {
    width: calc(50% - 16px);
  }
}
@media (max-width: 480px) {
  .product-card {
    width: 100%;
  }
}
</style>
