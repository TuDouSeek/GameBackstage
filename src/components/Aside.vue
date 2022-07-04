<template>
  <div>
    
      <div class="logo_back">
        <img src="../../public/gameicon.png" alt="" srcset="">
      </div>
   
      <el-menu
        background-color="#0078d4"
        default-active="2"
        class="el-menu-vertical-demo"
        @open="handleOpen"
        @close="handleClose">
        <div class="log">
            <img src="" alt="" srcset="">
        </div>
        <router-link to="/home/about" style="text-decoration: none;">
        <el-menu-item class="a" style="background-color: rgb(253 253 253 / 16%);">
            <i class="el-icon-menu"></i>
            <span slot="title">首页</span>
        </el-menu-item>
         </router-link>
        <router-link to="/home/HomeView" style="text-decoration: none;">
        <el-menu-item class="a" style="background-color: rgb(253 253 253 / 16%);">
            <i class="el-icon-setting"></i>
            <span slot="title">用户管理</span>
        </el-menu-item>
        </router-link>
       <router-link to="/home" style="text-decoration: none;">
        <el-menu-item class="a" style="background-color: rgb(253 253 253 / 16%);">
            <i class="el-icon-setting"></i>
            <span slot="title">静态文件</span>
        </el-menu-item>
        </router-link>
        <router-link to="/home/Manag" style="text-decoration: none;">
        <el-menu-item class="a" style="background-color: rgb(253 253 253 / 16%);">
            <i class="el-icon-s-tools"></i>
            <span slot="title">游戏管理</span>
        </el-menu-item>
        </router-link>
        </el-menu>
  </div>
</template>

<script>
export default {
    methods: {
         handleOpen(key, keyPath) {
         console.log(key, keyPath);
      },
      handleClose(key, keyPath) {
        console.log(key, keyPath);
      },
    }
}
</script>

<style>
@import url(../assets/page.css);
.a:hover{
   color: rgb(74, 155, 192);
    
}.logo_back{
  position: absolute;
  z-index: 10;
}.logo_back img{
  width: 100px;
  transform: translate(50%,20%);
}
</style>
