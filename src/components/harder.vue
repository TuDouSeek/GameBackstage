<template>
  <div>
    <div class="hed">
        <div class="yhm">
            <span>{{user.nickname}}</span>  
            </div>   
        <el-row class="block-col-2">
            <el-col :span="12">
              <el-dropdown >
                <span class="el-dropdown-link">
                   <img :src="user.imgurl" alt="" srcset="" class="tx" border="0"></span>
                <el-dropdown-menu slot="dropdown">
                    <el-dropdown-item icon="el-icon-plus">黄金糕</el-dropdown-item>
                    <el-dropdown-item icon="el-icon-circle-plus">狮子头</el-dropdown-item>
                    <el-dropdown-item icon="el-icon-circle-plus-outline">螺蛳粉</el-dropdown-item>
                    <el-dropdown-item icon="el-icon-check"><router-link to="/home/mainMessage">个人信息</router-link></el-dropdown-item>
                    <el-dropdown-item class="iconfont icon-tuichu4"><span @click="logout">退出</span></el-dropdown-item>
                </el-dropdown-menu>
              </el-dropdown>
            </el-col>
        </el-row>
         
  </div>
  </div>
</template>

<script>
export default {
   data(){
       return{
           user:localStorage.getItem("user") ?JSON.parse(localStorage.getItem("user")):{} 
       }
   },
  
   methods:{
       logout(){
           this.$router.push("/login")
           localStorage.removeItem('user')       //清除user里面的内容
           this.$message.success("退出成功")
       }
   }
}
</script>

<style>
@import url(//at.alicdn.com/t/font_3431695_4yji653dcf9.css);
.tx{
    width: 50px;
    height: 50px;
    border: 1px solid rgb(231 137 105);
    border-radius: 50%;
    margin-right: 10px;
}
.yhm{
    margin-right: 30px;
}
.hed{
    
    width:  100%;
    height: 100px;
    background-color: #4294d3;
    display: flex;
    align-items: center;
    flex-direction: row-reverse;
}
.login{
    margin-right: 50px;
}.block-col-2{
    position: absolute;
    right: 0;
}*{
    text-decoration: none;
}
</style>