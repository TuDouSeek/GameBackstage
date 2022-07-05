<template> 
  <div>
    <div class="tree" style="float:left">
        <p class="name">分类</p>
        <li class="classify_name" @click="sj">动作</li>
        <li class="classify_name" @click="sj2">射击</li>
        <li class="classify_name">竞速</li>
        <li class="classify_name">模拟</li>
        <li class="classify_name">2D</li>
        <li class="classify_name">休闲</li>
   </div>
    <div class="content" style="float:left">
        <div style="display:flex;margin-bottom: 10px;">
          
           <el-button type="primary" @click="dialogFormVisible = true" icon="el-icon-circle-plus">新增</el-button>
          
            <el-input
                style="width:200px; margin:0px 10px 0px 50px;"
                placeholder="游戏名"
                suffix-icon="el-icon-search"
                v-model="input1">
              </el-input>
            <el-button type="info">搜索</el-button>
        </div>
        <div>
          <el-table
            class="table"
            scroll="no"
            :data="tableData"
            height="650px"
            style="width: 100%;"
            :row-style="tableRowStyle"
            :header-cell-style="tableHeaderColor"
            >
            <el-table-column
              prop="id"
              label="id"
              width="100">
            </el-table-column>

            <el-table-column  label="标题图" width="150">
            <template slot-scope="logo_img">
              <span v-for="(item,index) in logo_img" :key="index">
              <el-popover placement="left" trigger="hover" width="100" >
                  <img :src="item.img" width="100%" />
                    <img
                      slot="reference"
                      :src="item.img"
                      :alt="item.name"
                      style="max-height: 70px;max-width: 70px; "
                  />
              </el-popover>
                </span>
            </template>
          </el-table-column>

            
            <el-table-column
              prop="name"
              label="游戏名"
              width="200">
            </el-table-column>

            <el-table-column
              prop="details"
              label="详情"
              width="200">
            </el-table-column>

            <el-table-column
              prop="terrace"
              label="平台"
              width="150">
            </el-table-column>

            <el-table-column
              prop="size"
              label="大小"
              width="150">
            </el-table-column>

            <el-table-column
              prop=""
              label=""
              width="150">
            </el-table-column>

            <el-table-column
              prop=""
              label=""
              width="200">
            </el-table-column>

            <el-table-column
              prop="size"
              label="操作"
              width="150">
            </el-table-column>

          </el-table>
        </div>
        
        </div>
  
  <el-dialog title="收货地址" :visible.sync="dialogFormVisible">
    <el-form :model="form">
      <el-form-item label="活动名称" :label-width="formLabelWidth">
        <el-input v-model="form.name" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="游戏图片" :label-width="formLabelWidth">
        <div class="upload_img">
          <el-upload
          :limit= '10'
          action="https://jsonplaceholder.typicode.com/posts/"
          list-type="picture-card"
          :on-preview="handlePictureCardPreview"
	        :on-remove="handleRemove"
          >
          <i class="el-icon-plus" >最多10张</i>
        </el-upload>
        </div>
        <el-dialog :visible.sync="dialogVisible">
          <img width="100%" class="imgs" :src="dialogImageUrl" alt="">
        </el-dialog>
      </el-form-item>
    </el-form>
    <div slot="footer" class="dialog-footer">
      <el-button @click="dialogFormVisible = false">取 消</el-button>
      <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
    </div>
  </el-dialog>
  </div>
</template>

<script>
import axios from 'axios';
  export default {
    data() {
      return {
        game:[],
        game2:[],
        tableData:[],
        input1:'',
        dialogTableVisible: false,
        dialogFormVisible: false,
        form: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        },
        formLabelWidth: '120px',
       dialogImageUrl: '',
       dialogVisible: false,
       
      };
    },
    methods: {
      sj(){
        axios.get('http://localhost:4000/data').then(res => {
           console.log(res);
          this.game = res.data.Game
          this.tableData = res.data.Game
        })
      },sj2(){
        axios.get('http://localhost:4000/game2').then(res => {
          console.log(res);
          this.game2 = res.data.Game
          this.tableData = res.data.Game
          
        })
      },id(id){
        
        console.log(id);
      },
      handleNodeClick(data) {
        console.log(data);
      },
      tableRowStyle({ row, rowIndex }) {
      return 'background-color: #F7F6Fd;'   
      },
      // 修改table header的背景色
      tableHeaderColor({ row, column, rowIndex, columnIndex }) {
      if (rowIndex === 0) {
        return 'background-color: lightblue;color: #303133;font-weight: 500;font-size: 20px;' //font-size: 20px;为字体大小设置
      }
      },
     
     
      handlePictureCardPreview(file) {
        this.dialogImageUrl = file.url;
        this.dialogVisible = true;
      },
      imgs(){
        
      }
    },
    mounted(){
      
    } 
  };
</script>
<style >
*::-webkit-scrollbar {
				display: none;
			}
*{
  margin: 0;
}
.tree{
  width: 200px;
  height: calc( 100vh - 140px);
  padding: 10px;
  margin: 10px;
  border-radius: 30px;
  background: rgba( 255, 255, 255, 0.25 );
  box-shadow: 0 8px 32px 0 rgba( 31, 38, 135, 0.37 );
  backdrop-filter: blur( 4px );
  -webkit-backdrop-filter: blur( 4px );
  border-radius: 10px;
  border: 1px solid rgba( 255, 255, 255, 0.18 );
  }.name{
    text-align: center;
    font-size: 20px;
  }.classify_name{
    list-style: none;
    height: 30px;
    width: 100%;
  }.classify_name:hover{
    background: rgba(226, 226, 225, 0.224);
  }.content{
    width: calc(100% - 290px);
    height: calc( 100vh - 140px);
    padding: 10px;
    margin: 10px;
    border-radius: 30px;
    background: rgba( 255, 255, 255, 0.25 );
    box-shadow: 0 8px 32px 0 rgba( 31, 38, 135, 0.37 );
    backdrop-filter: blur( 4px );
    -webkit-backdrop-filter: blur( 4px );
    border-radius: 10px;
    border: 1px solid rgba( 255, 255, 255, 0.18 );
  }.game{
    padding: 10px;
    background: rgba( 255, 255, 255, 0.25 );
    box-shadow: 0 8px 32px 0 rgba( 31, 38, 135, 0.37 );
    backdrop-filter: blur( 4px );
    -webkit-backdrop-filter: blur( 4px );
    border-radius: 10px;
    border: 1px solid rgba( 255, 255, 255, 0.18 );
    margin: 0px 10px 0px 0px;
  }.classify_name_text{
    width: 158px;

  }.cell{
    text-align: center;
  }.table{
    -ms-overflow-style: none;
  }.is-leaf{
    font-size: 10px;
  }
</style>
