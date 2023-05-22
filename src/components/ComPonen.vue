<template>
   <div class="box">
    <div class="box2">
        <div class="box3">
            <h1 class="jakarta">{{jkt}}</h1>
            <div class="box5">
                <img class="awan" :src="iconjkt" alt="">
            </div>
            <div class="box4">
                <h2 class="berawan">{{cuacajkt}} , {{suhujkt}}</h2>
            </div>
            <div class="garis">

            </div>
            <div class="keep">
                <h2 class="keep">Keep save</h2>
            </div>
            
        </div>
    </div>
    <HelloWorld/>
   </div>
   
</template>



<script>
import HelloWorld from './HelloWorld.vue';

    export default{
    name: "ComPonen",
    components: { HelloWorld },

    data() {
     return {
       bks: '',
       iconbks: '',
       suhubks: '',
       jkt: '',
       iconjkt:'',
       suhujkt: '',
       cuacajkt: '',
      
     }
   },
   mounted() {
    //kalau cuman manggil 1 data dari api
    //  fetch('https://api.weatherbit.io/v2.0/current?key=dbf7284b79e941d0a04e7c4f788d7afd&include=minutely&city=bekasi&lang=id')
    //    .then(res => res.json())
    let fetch1 =fetch('https://api.weatherbit.io/v2.0/current?key=dbf7284b79e941d0a04e7c4f788d7afd&include=minutely&city=bekasi&lang=id')
    .then(res => res.json())
    let fetch2 =fetch('https://api.weatherbit.io/v2.0/current?key=dbf7284b79e941d0a04e7c4f788d7afd&include=minutely&city=jakarta&lang=id')
    .then(res => res.json())
    
    
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
          this.cuacajkt = jakarta.data[0].weather.description

        //   console.log(jakarta)
        })
   },
   methods: {
     source(test) {
       return `https://cdn.weatherbit.io/static/img/icons/${test}.png`
     }
   }
}
</script>

<style>
   .box{
    width: auto;
    height: 795px;
    
    background-image: linear-gradient(160deg, #0093E9 0%, #80D0C7 100%);
    
   }
   .box2{
    width: 650px;
    height: 795px;
    
    float: left;
   }
   .box3{
    width: 550px;
    height: 795px;

    float: right;
 
   }
   .jakarta{
    color: white;
    font-size: 130px;
    margin-top: 170px;
   }
   .box4{
    width: 450px;
    height: 90px;
    background-color: #cbcfd1;
    margin-left: 20px;
    border-radius: 20px;
    opacity: 80%;

   }
   .box5{
    width: 90px;
    height: 90px;

    position: absolute;


   }
   .awan{
    width: 120px;
    height: 120px;
    position: relative;
    float: right;
    z-index: 999;

   }
   .berawan{
    font-size: 40px;
    padding-left: 60px;
    color: white;
    font-weight: 100;
    padding-top: 18px;
   }
   .garis{
    width: auto;
    height: 5px;
    background-color: aliceblue;
    margin-top: 20px;
   }
   .keep{
    color: white;
    font-weight: 150px;
    font-size: 55px;
   }
</style>
