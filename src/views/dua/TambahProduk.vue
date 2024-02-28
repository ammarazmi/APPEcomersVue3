<template>
    <!-- start breadcumb -->
    <div class="container">
        <div class="flex items-center text-primary md:ml-5 font-medium bg-primary py-4 px-4 rounded mt-10 mb-10">
            <RouterLink to="/" href="#" class="hover:text-opacity-80 text-white">Produk</RouterLink>
            <span class="mx-2 text-white">/</span>
            <RouterLink to="/menu" href="#" class=" text-white hover:text-opacity-80">Form Produk</RouterLink>
            <span class="mx-2 text-white">/</span>
            <span class="text-white"> Form Tambah Produk</span>
        </div>
    </div>
    <!-- end breadcumb -->

    <!-- start form input -->
    <div class="container">
        <div class="overflow-x-auto mb-5 mt-10">
            <h1 class="text-4xl text-center font-semibold text-primary mb-5">Form Tambah Produk</h1>
            <form action="" v-on:submit.prevent>
                <div class=" flex justify-center">
                    <div class=" w-3/4 bg-slate-100 bg-opacity-50 border-2 border-slate-950 rounded-lg">
                        <!-- <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                        <div class="text-primary py-2 px-4"><strong>ID Produk : </strong></div>
                        <div class="py-2 px-4">
                            <input type="text" class="w-full border-2 border-primary rounded-lg" />
                        </div>
                    </div> -->
                        <!-- <div class="hidden mt-5 text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                        <div class="text-primary py-2 px-4"><strong>Kode Produk :</strong></div>
                        <div class="py-2 px-4">
                            <input type="text" class="w-full border-2 border-primary rounded-lg" v-model="tambahProduk.Kode" />
                        </div>
                    </div> -->
                        <div class=" mt-5 hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                            <div class="text-primary py-2 px-4"><strong> Nama Produk :</strong></div>
                            <div class="py-2 px-4">
                                <input type="text" name="nama" id="nama" class="w-full rounded-lg border-2 border-primary"
                                    v-model="simpan.nama" />
                            </div>
                        </div>
                        <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                            <div class="text-primary py-2 px-4"><strong>Harga Produk : </strong></div>
                            <div class="py-2 px-4">
                                <input type="number" required name="harga" id="harga" min="0" value="0" step="any"
                                    class="w-full rounded-lg border-2 border-primary" v-model="simpan.harga" />
                            </div>
                        </div>
                        <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                            <div class="text-primary py-2 px-4"><strong>Status Stok : </strong></div>
                            <div class="py-2 px-4">
                                <select name="isready" id="isready" class="w-full rounded-lg border-2 border-primary"
                                    v-model="simpan.isready">
                                    <option value="option1">==Pilih==</option>
                                    <option value="option2">Ready</option>
                                    <option value="option3">Kosong</option>
                                </select>
                            </div>
                        </div>
                        <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                            <div class="text-primary py-2 px-4"><strong>Deskripsi : </strong></div>
                            <div class="py-2 px-4">
                                <textarea name="keterangan" id="keterangan"
                                    class="w-full border-2 border-primary rounded-lg"
                                    v-model="simpan.keterangan"></textarea>
                            </div>
                        </div>
                        <!-- <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                        <div class="text-primary"><strong> Link Produk : </strong></div>
                        <div class="py-2 px-4">
                            <textarea class="w-full border-2 border-primary rounded-lg"
                                v-model="tambahProduk.link"></textarea>
                        </div>
                    </div> -->
                        <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                            <div class="text-primary py-2 px-4"><strong>Upload Gambar : </strong></div>
                            <div class="py-2 px-4">
                                <input type="file" id="gambar" name="gambar" accept="image/*"
                                    class="-mr-10 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-highlight text-sm" />
                            </div>
                        </div>
                        <div class="hidden mt-10 mb-10 text-end sm:grid md:grid lg:grid xl:grid grid-cols-1">
                            <div class="py-2 px-4">
                                <RouterLink to="/formproduk" class="bg-red-500 p-3 m-2 rounded-lg">
                                    Kembali
                                </RouterLink>
                                <button class="bg-green-500 p-2 m-2 rounded-lg hover:opacity-80" @click="kirimProduct">
                                    Simpan
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </form>
        </div>
    </div>
    <!-- end form input -->
</template>


<script>
import axios from 'axios';

export default {
  name: 'TambahProduk',
  data() {
    return {
      simpan: {
        nama: '',
        harga: 0,
        isready: 'option1',
        keterangan: '',
      },
    };
  },
  methods: {
    simpanProduct() {
      // Logika penanganan pengiriman formulir di sini menggunakan this.simpan
      this.kirimProduct(this.simpan);
    },
    kirimProduct(dataProduk) {
      axios
        .post('https://localhost:7038/api/Product', dataProduk) // Gunakan URL relatif atau konfigurasi base URL secara global
        .then((response) => {
          // Penanganan respon sukses (misalnya, tampilkan pesan sukses)
          console.log('Produk berhasil dibuat:', response.data);
        })
        .catch((error) => {
          // Penanganan kesalahan (misalnya, tampilkan pesan kesalahan)
          console.error('Error saat membuat produk:', error);
        });
    },
    // ... metode yang sudah ada ...
  },
  mounted() {
    axios
      .get('https://localhost:7038/api/Product') // Gunakan URL relatif atau konfigurasi base URL secara global
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.error('Error mengambil data:', error));
  },
};
</script>

<style></style>