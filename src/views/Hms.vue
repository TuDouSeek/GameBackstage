<template>
  <div id="app">
    <svg :class="{top:y1 , class1:y2}"  xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320"><path fill="#0099ff" fill-opacity="1" d="M0,192L0,64L160,64L160,160L320,160L320,64L480,64L480,160L640,160L640,288L800,288L800,192L960,192L960,256L1120,256L1120,192L1280,192L1280,128L1440,128L1440,0L1280,0L1280,0L1120,0L1120,0L960,0L960,0L800,0L800,0L640,0L640,0L480,0L480,0L320,0L320,0L160,0L160,0L0,0L0,0Z"></path></svg>
      <div to="" style="position: absolute;top:50%;right:50%;transform: translate(50%, -50%);">
        <el-button type="primary" @click="routerLink(),classTsst()">主要按钮</el-button>
      </div>
    <svg :class="{db:y1 , class1:y2}" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320"><path fill="#0099ff" fill-opacity="1" d="M0,192L0,64L160,64L160,160L320,160L320,64L480,64L480,160L640,160L640,288L800,288L800,192L960,192L960,256L1120,256L1120,192L1280,192L1280,128L1440,128L1440,320L1280,320L1280,320L1120,320L1120,320L960,320L960,320L800,320L800,320L640,320L640,320L480,320L480,320L320,320L320,320L160,320L160,320L0,320L0,320Z"></path></svg>
  </div>
</template>

<script>

export default {
  data(){
    return {
      y1:true,
      y2:false
    }
  },
  mounted(){
    
  },
  methods:{
    
    classTsst(){
      this.y1 =! this.y1
      this.y2 =! this.y2
    },
    routerLink(){
      const timer = setInterval(()=>{
         this.$router.push({path:'/home'})
        console.log("hell");
      },3000)
      this.$once('hook:beforeDestroy', ()=>{
        clearInterval(timer)
     })  
    },
  }
}
</script>

<style>
.top{
  position: absolute;
  bottom: 54%;
  right: 0;
}
.db{
position: absolute;
bottom:0;
right: 0;
}
.class1{
  position: absolute;
  bottom: 40%;
  transition: 3s ;
}
</style>