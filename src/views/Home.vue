<template>
  <div class="bj">
        <div class="feft">
          <el-col :span="12">
            <Aisde/>
            </el-col>
        </div>
        <div class="rigth" style="padding:0;">
            <Haeder></Haeder> 
            <Data></Data>
            <router-view></router-view>
        </div>
  </div>
</template>
<script>
import Aisde from '../components/Aside.vue'
import Haeder from '../components/harder.vue'
import Data from '../components/Datas.vue'
  export default {
    components: {
      Aisde,Haeder,Data
    },
  }
</script>

<style>
@import url(../assets/page.css);
*{
  padding: 0;
}
.log{
  width: 100%;
  height: 150px;
   background-color:"#545c64"
}
  .el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 200px;
    min-height: 100vh;
  }.bj{
    display: flex;
  }.el-menu--collapse {
    width: 140px;
}.rigth{
  width: 100%;
  height: 700px;
  position: relative;
  
}.el-table{
  height: 600px;
}.inputs{
  width: 100px;
}.harder{
  background: linear-gradient(126deg,#42a3e4,#4dabea);
    width: 100%;
    margin-bottom: 40px;
    
    height: 80px;
}
</style>
