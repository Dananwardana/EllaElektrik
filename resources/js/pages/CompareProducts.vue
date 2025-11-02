<script setup>
import { Head } from '@inertiajs/vue3'
import { ref, computed } from 'vue'
import HeaderLayout from '../components/HeaderLayout.vue'
import FooterLayout from '@/components/FooterLayout.vue'

//Data dummy
const products = [
  {
    id: 1,
    name: 'Kipas Miyako 16 Inch',
    price: 99,
    image: '/images/kipas-miyako.jpg',
    specs: ['Daya 50W', '3 Kecepatan', 'Garansi 1 Tahun', 'Putar Otomatis'],
  },
  {
    id: 2,
    name: 'Blender Philips HR2221',
    price: 120,
    image: '/images/blender-philips.jpg',
    specs: ['Kapasitas 1.5L', 'Mata pisau stainless', '5 kecepatan', 'Garansi 2 Tahun'],
  },
  {
    id: 3,
    name: 'Rice Cooker Cosmos CRJ-6601',
    price: 150,
    image: '/images/rice-cooker.jpg',
    specs: ['Kapasitas 2L', 'Anti lengket', 'Fungsi menghangatkan', 'Garansi 1 Tahun'],
  },
  {
    id: 4,
    name: 'Setrika Maspion HA-110',
    price: 80,
    image: '/images/setrika-maspion.jpg',
    specs: ['Daya 300W', 'Tapak anti lengket', 'Kabel fleksibel', 'Garansi 1 Tahun'],
  },
]

//Variabel
const searchLeft = ref('')
const searchRight = ref('')
const selectedLeft = ref('')
const selectedRight = ref('')
const leftProduct = ref(null)
const rightProduct = ref(null)

//Filter pencarian
const filteredLeftProducts = computed(() =>
  products.filter((p) =>
    p.name.toLowerCase().includes(searchLeft.value.toLowerCase())
  )
)
const filteredRightProducts = computed(() =>
  products.filter((p) =>
    p.name.toLowerCase().includes(searchRight.value.toLowerCase())
  )
)

//Logika pemilihan produk
function selectProduct(side) {
  const selected =
    side === 'left'
      ? products.find((p) => p.id === parseInt(selectedLeft.value))
      : products.find((p) => p.id === parseInt(selectedRight.value))

  if (side === 'left') leftProduct.value = selected
  else rightProduct.value = selected
}
</script>

<template>
  <div class="min-h-screen bg-gray-50">
    <Head title="Perbandingan Produk - Ella Elektrik" />

    <!-- Header -->
    <HeaderLayout />

    <main class="container mx-auto px-6 py-10">
      <h1 class="text-2xl font-bold mb-6 text-center">Perbandingan Produk</h1>

      <!-- Grid 2 kolom -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <!-- Kolom kiri -->
        <div class="bg-white shadow rounded-xl p-6">
          <label class="block font-semibold mb-2">Compare with</label>

          <input
            v-model="searchLeft"
            type="text"
            placeholder="Cari produk..."
            class="w-full border rounded-md p-2 mb-3"
          />

          <select
            v-model="selectedLeft"
            @change="selectProduct('left')"
            class="w-full border rounded-md p-2 mb-4"
          >
            <option value="">Pilih produk...</option>
            <option
              v-for="p in filteredLeftProducts"
              :key="p.id"
              :value="p.id"
            >
              {{ p.name }}
            </option>
          </select>

          <div v-if="leftProduct" class="text-center">
            <img
              :src="leftProduct.image"
              :alt="leftProduct.name"
              class="w-48 h-48 object-cover mx-auto rounded-lg"
            />
            <h2 class="mt-3 font-semibold">{{ leftProduct.name }}</h2>
            <p class="text-gray-500">${{ leftProduct.price }}</p>

            <div class="mt-4 text-left">
              <h3 class="font-bold mb-2">Spesifikasi:</h3>
              <ul class="space-y-1">
                <li
                  v-for="(s, i) in leftProduct.specs"
                  :key="i"
                  class="text-sm text-gray-600"
                >
                  • {{ s }}
                </li>
              </ul>
            </div>
          </div>
        </div>

        <!-- Kolom kanan -->
        <div class="bg-white shadow rounded-xl p-6">
          <label class="block font-semibold mb-2">Compare with</label>

          <input
            v-model="searchRight"
            type="text"
            placeholder="Cari produk..."
            class="w-full border rounded-md p-2 mb-3"
          />

          <select
            v-model="selectedRight"
            @change="selectProduct('right')"
            class="w-full border rounded-md p-2 mb-4"
          >
            <option value="">Pilih produk...</option>
            <option
              v-for="p in filteredRightProducts"
              :key="p.id"
              :value="p.id"
            >
              {{ p.name }}
            </option>
          </select>

          <div v-if="rightProduct" class="text-center">
            <img
              :src="rightProduct.image"
              :alt="rightProduct.name"
              class="w-48 h-48 object-cover mx-auto rounded-lg"
            />
            <h2 class="mt-3 font-semibold">{{ rightProduct.name }}</h2>
            <p class="text-gray-500">${{ rightProduct.price }}</p>

            <div class="mt-4 text-left">
              <h3 class="font-bold mb-2">Spesifikasi:</h3>
              <ul class="space-y-1">
                <li
                  v-for="(s, i) in rightProduct.specs"
                  :key="i"
                  class="text-sm text-gray-600"
                >
                  • {{ s }}
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </main>

    <!-- Footer -->
    <FooterLayout />
  </div>
</template>

