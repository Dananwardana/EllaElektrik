<template>
    <div class="min-h-screen bg-[#F5F7FA]">

        <Head title="Detail Produk - Ella Elektrik" />

        <!-- Header -->
        <HeaderLayout />

        <!-- Main Content -->
        <main class="container mx-auto px-8 pt-28 pb-20">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-10">
                <!-- Kolom Kiri: Gambar Produk -->
                <div class="flex flex-col items-center justify-center">
                    <img :src="product.image" :alt="product.name"
                        class="w-full max-w-md rounded-xl shadow-md object-contain mb-6" />

                    <!-- Gambar Lain / Thumbnail -->
                    <div class="flex space-x-4 mt-4">
                        <img v-for="(img, i) in product.gallery" :key="i" :src="img" alt="Thumbnail"
                            class="w-28 h-28 rounded-lg object-cover cursor-pointer border border-gray-200 hover:border-gray-400 transition" />
                    </div>
                </div>

                <!-- Kolom Kanan: Detail Produk -->
                <div class="flex flex-col justify-between">
                    <div>
                        <h1 class="text-3xl font-bold mb-2">{{ product.name }}</h1>
                        <p class="text-2xl font-semibold text-gray-800 mb-4">
                            Rp. {{ product.price.toLocaleString('id-ID') }}
                        </p>

                        <p class="text-gray-600 mb-6 leading-relaxed">
                            {{ product.description }}
                        </p>

                        <!-- Spesifikasi Produk -->
                        <div class="mb-6">
                            <h3 class="font-semibold mb-3 text-lg">Spesifikasi Produk</h3>
                            <ul class="list-disc list-inside text-gray-700 leading-relaxed space-y-1">
                                <li>3 Kecepatan Angin</li>
                                <li>Diameter 16 cm</li>
                                <li>Motor Halus dan Hemat Listrik</li>
                                <li>Garansi 1 Tahun</li>
                            </ul>
                        </div>

                        <!-- Bagian Tombol & Jumlah -->
                        <div class="flex flex-col gap-4">
                            <!-- Baris: Masukkan Keranjang + Jumlah -->
                            <div class="flex flex-wrap items-center gap-4">
                                <!-- Tombol Masukkan Keranjang -->
                                <button
                                    class="flex items-center justify-center gap-2 bg-black text-white px-6 py-3 rounded-md hover:bg-gray-800 transition">
                                    <i class="fas fa-cart-plus"></i> Masukkan Keranjang
                                </button>

                                <!-- Jumlah -->
                                <div class="flex items-center space-x-3 border border-gray-300 rounded-md">
                                    <button @click="decreaseQty" class="px-3 py-1 text-lg font-bold hover:bg-gray-200">
                                        −
                                    </button>
                                    <span class="px-4">{{ quantity }}</span>
                                    <button @click="increaseQty" class="px-3 py-1 text-lg font-bold hover:bg-gray-200">
                                        +
                                    </button>
                                </div>
                            </div>

                            <!-- Tombol Bandingkan Produk -->
                            <Link href="/compare-products"
                                class="flex items-center justify-center gap-2 border bg-black text-white px-6 py-3 rounded-md hover:bg-gray-100 transition w-fit">
                            <i class="fas fa-scale-balanced"></i> Bandingkan Produk
                            </Link>
                        </div>
                    </div>
                </div>
            </div>
        </main>

        <!-- Footer -->
        <FooterLayout />
    </div>
</template>

<script setup>
import { Head, Link } from '@inertiajs/vue3'
import HeaderLayout from '@/components/HeaderLayout.vue'
import FooterLayout from '@/components/FooterLayout.vue'
import { ref } from 'vue'

// ✅ Data Dummy
const product = ref({
    name: 'Kipas Karakter',
    price: 100000,
    description:
        'Kipas angin karakter lucu dengan desain menarik dan kualitas terbaik. Dilengkapi 3 kecepatan angin, diameter 16 cm, serta motor halus dan hemat listrik.',
    image: '/images/kipas.png',
    gallery: [
        '/images/kipas1.png',
        '/images/kipas2.png',
        '/images/kipas3.png',
    ],
    specs: [
        '3 Kecepatan Angin',
        'Diameter 16 cm',
        'Motor Halus dan Hemat Listrik',
        'Garansi 1 Tahun',
    ],
})

// 🔢 Jumlah Produk
const quantity = ref(1)
const increaseQty = () => quantity.value++
const decreaseQty = () => {
    if (quantity.value > 1) quantity.value--
}
</script>

<style scoped>
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css');
</style>
