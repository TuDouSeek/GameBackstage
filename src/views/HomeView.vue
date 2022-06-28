<template>
  <div class="bj">
    
        <div class="feft">
          <el-col :span="12">
            
            </el-col>
        </div>
        <div class="rigth" style="padding:0;">
            
            <router-view></router-view>
            <div style="margin-bottom: 0px;    margin-top: 10px;padding: 10px;">
              <el-input v-model="username" suffix-icon="el-icon-s-order"  style="width:200px;margin-right: 10px;" placeholder="请输入姓名"></el-input>
              <el-input v-model="phone" suffix-icon="el-icon-s-comment"  style="width:200px;margin-right: 10px;" placeholder="请输入电话"></el-input>
              <el-input v-model="address" suffix-icon="el-icon-office-building"  style="width:200px;margin-right: 10px;" placeholder="请输入地址"></el-input>
              <el-button @click="load" type="primary">搜索</el-button>
              <el-button @click="reset" type="primary">重置</el-button>
               <div style="margin:10px 0px">
                  <el-button type="primary" @click="handAdd">新增<i class="el-icon-circle-plus-outline"></i></el-button>
                  
               </div>
            </div> 
               <div style="overflow: auto;height: 580px;" class="bg">
                 <el-table
                  ref="multipleTable"
                  :data="tableData"
                  tooltip-effect="dark"
                  style="width: 100%;overflow: overlay;"
                  @selection-change="handleSelectionChange">
                  <el-table-column  type="selection"  width="55" > </el-table-column>
                  <el-table-column prop="username" label="用户名"  width="120"></el-table-column>
                  <el-table-column prop="nickname" label="昵称" width="120"> </el-table-column>
                  <el-table-column prop="email" label="邮箱" show-overflow-tooltip></el-table-column>
                  <el-table-column prop="phone" label="电话"  width="120"></el-table-column>
                  <el-table-column prop="address" label="地址" show-overflow-tooltip></el-table-column>

                  <el-table-column label="操作">
                    <template slot-scope="scope">
                      <el-button
                        size="mini"
                        @click="handleEdit(scope.row)">编辑</el-button>
                        <el-popover
                          placement="top"
                          width="150px"
                         
                          >
                          <p>这是一段内容这是一段内容确定删除吗？</p>
                           <div style="text-align: right; margin: 0">
                              <el-button size="mini" type="text" @click="visible = false">取消</el-button>
                              <el-button type="primary" size="mini" @click="handleDelete(scope.row.id)">确定</el-button>
                            </div>
                          <el-button size="mini" style="margin-left: 10px;background: #ff8585;" slot="reference">删除</el-button>
                        </el-popover>
                     
                    </template>
                  </el-table-column>
                </el-table>
               </div>
                <div style="margin-top: 15px">
                  <el-button @click="toggleSelection([tableData[1], tableData[2]])">切换第二、第三行的选中状态</el-button>
                  <el-button @click="toggleSelection()">取消选择</el-button>
                </div>
            <div>
              <div class="block" style="text-align: center;">
                
                <el-pagination
                  @size-change="handleSizeChange"
                  @current-change="handleCurrentChange"
                  :current-page="pageNum"
                  :page-sizes="[ 10, 15, 20]"
                  :page-size="pageSize"
                  layout="total, sizes, prev, pager, next, jumper"
                  :total="total">
                </el-pagination>
              </div>
            </div>

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
  </div>
</template>
<script>

import Data from '../components/Datas.vue'
  export default {
    components: {
      Data
    },
    data() {
      return {
        
        isCollapse: true,
        tableData: [],
        total:0,
        username:'',
        phone:'',
        address:'',
        form:{},
        dialogFormVisible:false,
        
        pageNum:1,
        pageSize:10,
        currentPage1: 5,
        currentPage2: 5,
        currentPage3: 5,
        currentPage4: 4
      };
    },
    created () {
      this.load()
    },
    methods: {
      load(){
        this.request.get("/user/page", {
            params:{
              pageNum:this.pageNum,
              pageSize:this.pageSize,
              username:this.username,
              phone:this.phone,
              address:this.address,
            }
        }
        ).then(res =>{
          console.log(res);
          this.tableData = res.records
          this.total = res.total
        })
      },
      save(){
      this.request.post("/user",this.form).then(res =>{
          if (res) {
            this.$message.success("保存成功")  
            this.dialogFormVisible = false 
            this.load()         
          }else{
            this.$message.success("s失败") 
            console.log(res);
          }
        })
      },
      handAdd(){
        this.dialogFormVisible = true
        this.form = {}
      },
      handleEdit(row){
        this.form = this.form = JSON.parse(JSON.stringify(row))
        this.dialogFormVisible = true
        
      },
      handleDelete(id){
        this.request.delete("/user/" +id).then(res =>{
           if(res){
          this.$message.success("删除成功")  
        this.load()
        }else{
           this.$message.success("删除失败")  
        }
        })
       
      },
      reset(){
          this.username = ""
          this.phone = ""
          this.address = ""
          this.load()
      },
        handleSizeChange(pageSize) {
        console.log(`每页 ${pageSize} 条`);
        this.pageSize = pageSize
        this.load()
      },
      handleCurrentChange(pageNum) {
        console.log(`当前页: ${pageNum}`);
        this.pageNum = pageNum
        this.load()
      },
      activeIndex(){},
      handleSelect(){},
     
      
      toggleSelection(rows) {
        if (rows) {
          rows.forEach(row => {
            this.$refs.multipleTable.toggleRowSelection(row);
          });
        } else {
          this.$refs.multipleTable.clearSelection();
        }
      },
      handleSelectionChange(val) {
        this.multipleSelection = val;
      }
    }

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
  
  
}.el-table{
  height: auto;
}.inputs{
  width: 100px;
}.harder{
  background: linear-gradient(126deg,#3ba3d0,#73a6c8);
    width: 100%;
    margin-bottom: 40px;
    
    height: 80px;
}::-webkit-scrollbar{display:none}
</style>
