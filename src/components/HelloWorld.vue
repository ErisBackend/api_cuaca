<template>
  <div class="hello">
    <div class="hari">
      <h3>Kamis, 8 November 2021</h3>
      <div class="garis2">

      </div>
    </div>

    <div class="car">
      <h4 class="kota">{{ jkt }}</h4>
      <img class="cuaca1" :src="iconjkt" alt="">
      <h1 class="derajat">{{ suhujkt }}</h1>
    </div>
    <div class="car">
      <h4 class="kota">{{bks}}</h4>
      <img class="cuaca1" :src="iconbks" alt="">
      <h1 class="derajat">{{ suhubks }}</h1>
    </div>
  </div>

 <div class="kotakjam">
    <div class="waktu">
      <h1 class="timer"></h1>
    </div>
    <div class="titik2">:</div>
    <div class="waktu">
      <h1 class="timer">00</h1>
    </div >
 </div>
</template>


 <script>
 export default {
   name: 'HelloWorld',
   data() {
     return {
       bks: '',
       iconbks: '',
       suhubks: '',
       jkt: '',
       iconjkt:'',
       suhujkt: '',
      
     }
   },
   mounted() {
    //kalau cuman manggil 1 data dari api
    //  fetch('https://api.weatherbit.io/v2.0/current?key=dbf7284b79e941d0a04e7c4f788d7afd&include=minutely&city=bekasi&lang=id')
    //    .then(res => res.json())
    let fetch1 =fetch('https://api.weatherbit.io/v2.0/current?key=dbf7284b79e941d0a04e7c4f788d7afd&include=minutely&city=bekasi&lang=id').then(res => res.json())
    let fetch2 =fetch('https://api.weatherbit.io/v2.0/current?key=dbf7284b79e941d0a04e7c4f788d7afd&include=minutely&city=jakarta&lang=id').then(res => res.json())
    
    
      //  .then(res => {
      //    this.cuaca = res.data[0].weather.description
      //    this.kota = res.data[0].city_name
      //    this.icon = this.source(res.data[0].weather.icon)
      //    this.suhu = res.data[0].app_temp

      //    console.log(res)
      //  })
      Promise.all([fetch1,fetch2])
      .then(([bekasi, jakarta ]) => {
          this.bks = bekasi.data[0].city_name
          this.iconbks = this.source(bekasi.data[0].weather.icon)
          this.suhubks = bekasi.data[0].app_temp
          this.jkt = jakarta.data[0].city_name
          this.iconjkt = this.source(jakarta.data[0].weather.icon)
          this.suhujkt = jakarta.data[0].app_temp

          // console.log(bekasi)
        })
   },
   methods: {
     source(test) {
       return `https://cdn.weatherbit.io/static/img/icons/${test}.png`
     }
   }
 }
 </script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .hello{
    width: 700px;
    height: 400px;

    float: left;
    margin-top: 200px; 
  }
  .hari{
    width: auto;
    height: 50px;

  }
  h3{
    color:white;
    padding-top: 15px;
    padding-left: 80px;
    float: left;
  }
  .garis2{
    width: 290px;
    height: 5px;
    background-color: white;
    margin-left: 340px;
    position: absolute;
    margin-top: 20px;
  
  }
  .car{
    width: 250px;
    height: 300px;
    background-color: white;
    float: left;
    margin-left: 65px;
    border-radius: 20px;
  }
  .kota{
    text-align: center;
    margin-top: 30px;
    font-size: 30px;
    font-weight: 50;
  }
  .cuaca1{
    width: 150px;
    height: 150px;
    margin-left: 40px;
  }
  .kotakjam{
    width: 300px;
    height: 150px;
    position: absolute;
    bottom: 0px;
    margin-left: 1000px;
  }
  
  .derajat{
    text-align: center;
  }
  .waktu{
    width: 100px;
    height: 149px;
    border: solid white;
    float: left;
    margin-left: 35px;
    border-radius: 15px ;
  }
  .titik2{
    float: left;
    font-size:100px;
    position: absolute;
    left: 145px;
    bottom: 20px;
    color: white;
  }
  .timer{
    font-size: 70px;
    color: white;
    margin-top: 40px;
    margin-left: 10px;
  }
</style>
