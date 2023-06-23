<template>
  <header>
    <div class="navbar sticky top-0 bg-primary">
      <div class="flex-1">
        <a class="btn btn-ghost normal-case text-white text-xl">Nilai Siswa</a>
      </div>
      <div class="flex-none">
        <ul class="menu text-white menu-horizontal px-1">
          <li><a href="/">Home</a></li>
        </ul>
      </div>
    </div>
  </header>
  <main>
    <div class="flex justify-center mt-10">
      <h1 class="font-bold text-3xl">Nilai Siswa</h1>
    </div>
    <div class="flex p-12 flex-col space-y-4">


      <FormSiswa :dataForm="dataForm" @submit="submitNilai" />
      <p>Nilai Rata Rata Siswa : {{ this?.average }}</p>

      <CardSiswa v-for="(task, key) in dataSiswa" :key="key" :keyC="key" :data="task" @delete="deleteData" />

      <div class="alert alert-warning" v-if="dataSiswa.length <= 0">
        <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current shrink-0 h-6 w-6" fill="none" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
            d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
        </svg>
        <span>Belum ada nilai</span>
      </div>

      <button class="btn btn-outline btn-warning" @click="handleAverage" type="reset">AVERAGE</button>

    </div>
  </main>
</template>

<script>

import CardSiswa from '@/components/CardSiswa'
import FormSiswa from '@/components/FormSiswa.vue';

export default {


  data() {
    return {
      average: null,
      dataForm: {
        nis: null,
        nama: null,
        nilai: null,
      },
      dataSiswa: [{
        nis: '191.101.221',
        nama: 'Reza Khoirul Wijaya Putra',
        nilai: 10
      }],
    };
  },

  components: {
    CardSiswa,
    FormSiswa
  },

  methods: {
    deleteData(id) {
      this.dataSiswa.splice(id, 1);
      this.refreshAverage();
    },
    submitNilai(e) {
      // validasi
      for (const key in this.dataForm) {
        if (!this.dataForm[key]) return alert('semua form harus di isi ya :D')
      }
      // menambah data
      this.dataSiswa.push({ ...this.dataForm });
      e.target.reset();
      // mengosongkan semua data form
      for (const key in this.dataForm) {
        this.dataForm[key] = null
      }

      this.refreshAverage()
    },

    totalNilaiSiswa() {
      return this.dataSiswa.map(n => n.nilai)
    },

    refreshAverage() {
      this.average = this.averageF(this.totalNilaiSiswa())
    },

    averageF(nilaiSiswa = []) {
      let totalNilai = 0;

      for (const n of nilaiSiswa) {
        totalNilai += n;
      }

      return Math.round(totalNilai / nilaiSiswa.length)
    },

    handleAverage() {
      const result = this.averageF(this.totalNilaiSiswa());
      this.average = result;
      return alert("Nilai rata-rata siswa : " + result)
    }
  },

  mounted() {
    this.average = this.averageF(this.totalNilaiSiswa())
  },
};
</script>
