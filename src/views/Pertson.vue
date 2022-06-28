<template>
  <div>
       <el-dialog title="用户信息" :visible.sync="dialogFormVisible">
            <el-form label-width="120px">
                <el-form-item label="用户名" >
                <el-input v-model="form.username" autocomplete="off"></el-input>
                </el-form-item>
                <el-form-item label="昵称" >
                <el-input v-model="form.nickname" autocomplete="off"></el-input>
                </el-form-item>
                <el-form-item label="邮箱" >
                <el-input v-model="form.email" autocomplete="off"></el-input>
                </el-form-item>
                <el-form-item label="电话">
                <el-input v-model="form.phone" autocomplete="off"></el-input>
                </el-form-item>
                <el-form-item label="地址">
                <el-input v-model="form.address" autocomplete="off"></el-input>
                </el-form-item>
                
            </el-form>
            <div slot="footer" class="dialog-footer">
                <el-button @click="dialogFormVisible = false">取 消</el-button>
                <el-button type="primary" @click="save">确 定</el-button>
            </div>
        </el-dialog>
  </div>
</template>

<script>
export default {
    data(){
        return{
            from:{}
        }
    },
    methods:{
        save(){
        this.request.post("/user",this.form).then(res =>{
            if (res) {
                this.$message.success("保存成功")  
                 
            }else{
                this.$message.success("s失败") 
                
            }
            })
        }
    }
}
</script>

<style>

</style>