<template>

    <!-- start breadcumb -->
    <div class="container">
        <div class="flex items-center text-primary md:ml-5 font-medium bg-primary py-4 px-4 rounded mt-10 mb-10">
            <RouterLink to="/" href="#" class="hover:text-opacity-80 text-white">Produk</RouterLink>
            <span class="mx-2 text-white">/</span>
            <RouterLink to="/menu" href="#" class=" text-white hover:text-opacity-80">From Produk</RouterLink>
            <span class="mx-2 text-white">/</span>
            <span class="text-white"> Form Tambah Produk</span>
        </div>
    </div>
    <!-- end breadcumb -->

    <!-- start form input -->
    <div class="container">
        <div class="overflow-x-auto mb-5 mt-10">
            <h1 class="text-4xl text-center font-semibold text-primary mb-5">Form Tambah Produk</h1>

            <div class="flex justify-center">
                <div class="w-3/4 bg-slate-100 bg-opacity-50 border-2 border-slate-950 rounded-lg">
                    <!-- <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                        <div class="text-primary py-2 px-4"><strong>ID Produk : </strong></div>
                        <div class="py-2 px-4">
                            <input type="text" class="w-full border-2 border-primary rounded-lg" />
                        </div>
                    </div> -->
                    <div class="hidden mt-5 text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                        <div class="text-primary py-2 px-4"><strong>Kode Produk :</strong></div>
                        <div class="py-2 px-4">
                            <input type="text" class="w-full border-2 border-primary rounded-lg" v-model="tambahproduk.Kode" />
                        </div>
                    </div>
                    <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                        <div class="text-primary py-2 px-4"><strong> Nama Produk :</strong></div>
                        <div class="py-2 px-4">
                            <input type="text" class="w-full rounded-lg border-2 border-primary" v-model="tambahproduk.nama" />
                        </div>
                    </div>
                    <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                        <div class="text-primary py-2 px-4"><strong>Harga Produk : </strong></div>
                        <div class="py-2 px-4">
                            <input type="text" class="w-full rounded-lg border-2 border-primary" v-model="tambahproduk.Harga" />
                        </div>
                    </div>
                    <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                        <div class="text-primary py-2 px-4"><strong>Status Stok : </strong></div>
                        <div class="py-2 px-4">
                            <select class="w-full rounded-lg border-2 border-primary" v-model="tambahproduk.is_ready" >
                                <option value="option1">==Pilih==</option>
                                <option value="option2">Ready</option>
                                <option value="option3">Kosong</option>
                            </select>
                        </div>
                    </div>
                    <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                        <div class="text-primary py-2 px-4"><strong>Deskripsi : </strong></div>
                        <div class="py-2 px-4">
                            <textarea class="w-full border-2 border-primary rounded-lg" v-model="tambahproduk.desc" ></textarea>
                        </div>
                    </div>
                    <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                        <div class="text-primary"><strong> Link Produk : </strong></div>
                        <div class="py-2 px-4">
                            <textarea class="w-full border-2 border-primary rounded-lg" v-model="tambahproduk.link" ></textarea>
                        </div>
                    </div>
                    <div class="hidden text-center sm:grid md:grid lg:grid xl:grid grid-cols-2">
                        <div class="text-primary py-2 px-4"><strong>Harga Produk : </strong></div>
                        <div class="py-2 px-4">
                            <textarea class="w-full border-2 border-primary rounded-lg" v-model="tambahproduk.harga" ></textarea>
                        </div>
                    </div>
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
                            <button class="bg-green-500 p-2 m-2 rounded-lg hover:opacity-80"
                            @click="tambahProduk">
                            Simpan
                        </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- end form input -->
</template>


<script>
import axios from 'axios'

export default {
    name: 'TambahProduk',
    components: {
        axios
    },
    data() {
        return {
            tambahproduk: {}
        }
    },
    methods: {
        setProduk(data) {
            this.tambahproduk = data;
        },
        tambahProduk() {
            if ( !this.tambahproduk.kode || !this.tambahproduk.nama || !this.tambahproduk.harga|| !this.tambahproduk.is_ready || !this.tambahproduk.desc || !this.tambahproduk.link || !this.tambahproduk.gambar )  {
            // Tangani kasus di mana kolom yang diperlukan tidak diisi
            console.error('Semua field wajib diisi');
            return;
            }
            // Kirim data produk baru ke server menggunakan POST request
            axios
                .post("http://localhost:3000/produks/", this.tambahproduk)
                .then((response) => {
                    // Handle respons jika diperlukan
                    console.log('Produk berhasil ditambahkan', response.data);
                    // Redirect atau lakukan tindakan lain setelah berhasil menambahkan produk
                    this.$router.push('/formproduk');
                })
                .catch((error) => {
                    // Handle error jika ada
                    console.error('Gagal menambahkan produk', error);
                });
            },
        
    },
    mounted() {
        axios
            .get("http://localhost:3000/produks/")
            .then((response) => this.setProduk(response.data))
            .catch((error) => console.log(error))

    }
}
</script>

<style>

</style>