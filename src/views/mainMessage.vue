<template>
  <div class="input">
      <el-input class="el_input" v-model="input" placeholder="昵称"></el-input>
      <el-input class="el_input" v-model="input" placeholder="邮箱"></el-input>
      <el-input class="el_input" v-model="input" placeholder="电话"></el-input>
      <el-input class="el_input" v-model="input" placeholder="地址"></el-input>
      <el-upload
        class="avatar-uploader"
        action="https://jsonplaceholder.typicode.com/posts/"
        :show-file-list="false"
        :on-success="handleAvatarSuccess"
        :before-upload="beforeAvatarUpload">
        <img v-if="imageUrl" :src="imageUrl" class="avatar">
        <i v-else class="el-icon-plus avatar-uploader-icon" placeholder="hell"></i>
        </el-upload>
        <el-button @click="updata()"> hello</el-button>
  </div>
</template>

<script>
import request from '@/utils/request';
  export default {
    data() {
      return {
        imageUrl: ''
      };
    },
    methods: {
        updata(){
            request.post('/user').then(res =>{
                              
            })
        },
      handleAvatarSuccess(res, file) {
        this.imageUrl = URL.createObjectURL(file.raw);
      },
      beforeAvatarUpload(file) {
        const isJPG = file.type === 'image/jpeg';
        const isLt2M = file.size / 1024 / 1024 < 2;

        if (!isJPG) {
          this.$message.error('上传头像图片只能是 JPG 格式!');
        }
        if (!isLt2M) {
          this.$message.error('上传头像图片大小不能超过 2MB!');
        }
        return isJPG && isLt2M;
      }
    }
  }
</script>

<style>
.input{
    border-radius: 10px;
    padding: 20px;
    position: absolute;
    width: 400px;
    left: 50%;
    transform: translate(-50%,50%);
    box-shadow: 0px 0px 12px 0px #969c9f;
}

.el_input{
    margin-top: 10px;
}  .avatar-uploader .el-upload {
    border: 1px dashed #d9d9d9;
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }
  .avatar-uploader .el-upload:hover {
    border-color: #409EFF;
  }
  .avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    line-height: 178px;
    text-align: center;
  }
  .avatar {
    width: 178px;
    height: 178px;
    display: block;
  }
</style>