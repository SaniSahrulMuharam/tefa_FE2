<template>
<div class="container-fluid">
  <div class="row my-5">
    <div class="col-lg-6">
      <nuxt-link to="/pengunjung/tambah">
        <div class="card bg-pengunjung rounded-5 m-3">
          <div class="card-body">
            <h2>pengunjung</h2>
          </div>
        </div>
      </nuxt-link>
    </div>

    <div class="col-lg-6">
      <nuxt-link to="/buku">
        <div class="card bg-buku rounded-5 m-3">
          <div class="card-body">
            <h2>cari buku</h2>
          </div>
        </div>
      </nuxt-link>
    </div>
  </div>
</div>
  <h2 style="margin: 30px;"><strong>STATISTIK</strong></h2>
  <div class="container-fluid">
    <div class="row justify-content-evenly rounded-5">
      <div class="col-5">
        <div class="raccing"><nuxt-link to="/pengunjung">
          <h2>{{ visitors.length }} pengunjung</h2>
      </nuxt-link>
      </div>
      </div>
      <div class="col-5">
        <div class="raccing1">
          <h2>{{ books.length }} Buku</h2>
      </div>
    </div>
  </div>
  </div>
</template>

<style scoped>
.card{
  height: 250px;
  box-shadow: 1px 1px 10px #424242;
}
.card.bg-pengunjung{
  background-image: url('../assets/img/kunjungan.webp');
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}
.card.bg-buku{
  background: url('../assets/img/cari-buku.webp');
  background-size: cover;
}
.raccing{
  height: 200px;
  box-shadow: 1px 1px 10px;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color:yellow;
}
.raccing1{
  height: 200px;
  box-shadow: 1px 1px 10px;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgb(60, 241, 60);
}
</style>
<script setup>
const supabase = useSupabaseClient()
const books = ref([])
const visitors = ref ([])

const totalPengunjung = async () => {
  const { data, error } = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
  if(data) visitors.value = data
}



const totalBuku = async () => {
  const { data, error } = await supabase.from('buku').select(`*, kategori(*)`)
  if(data) books.value = data
}

onMounted(() => {
  totalBuku()
  totalPengunjung()
})

</script>
