<template>
  <div class="hello">
    <el-table ref="singleTable" :data="tableData" highlight-current-row @current-change="handleCurrentChange" style="width: 100%">
    <el-table-column type="index" width="50"></el-table-column>
    <el-table-column label="" width="65">
      <template slot-scope="scope">
        <div>
          <el-radio :label="scope.row.date" v-model="templateRadio" @change.native="getTemplateRow(scope.$index,scope.row)">
             &nbsp;
          </el-radio>
        </div>
      </template>
    </el-table-column>
    <el-table-column property="date" label="日期"></el-table-column>
    <el-table-column label="姓名" width="180">
      <template slot-scope="scope">
        <div>
          <input type="text" v-model="scope.row.name" :ref="`myInput${scope.$index}`">
          <div @dblclick="edit(scope.$index)" style="width:130px;border:none;cursor:pointer;">{{scope.row.name}}</div>
        </div>
      </template>
    </el-table-column>
    <el-table-column property="address" label="地址">
      <template slot-scope="scope">
        <div @dblclick="edit">
          <input type="text" :disabled="editName" :class="{'pointer':editName}" v-model="scope.row.address" @blur="handleEdit(scope.$index, scope.row)" placeholder="请输入内容" >
        </div>
      </template>
    </el-table-column>
  </el-table>
  <!-- <div style="margin-top: 20px">
    <el-button @click="setCurrent(tableData[1])">选中第二行</el-button>
    <el-button @click="setCurrent()">取消选择</el-button>
  </div> -->
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      templateRadio:'2016-05-04',
      editName:false,
      tableData: [{
          date: '2016-05-02',
          name: '王1',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王2',
          address: '上海市普陀区金沙江路 1517 弄'
        }, {
          date: '2016-05-01',
          name: '王3',
          address: '上海市普陀区金沙江路 1519 弄'
        }, {
          date: '2016-05-03',
          name: '王4',
          address: '上海市普陀区金沙江路 1516 弄'
        }],
        currentRow: null
    }
  },
  methods: {
      setCurrent(row) {
        this.$refs.singleTable.setCurrentRow(row);
      },
      handleCurrentChange(val) {
        this.currentRow = val;
      },
      getTemplateRow(index,row){
        console.log(index,row)
      },
      edit(index){
        console.log(index,`myInput${index}`)
        this.editName=false;
        this.$refs[`myInput${index}`].focus()
      },
      handleEdit(index,row){
        // console.log(index, row);
        this.editName=true;
      },
      changeInput(){

      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello{
  margin-left: 100px;
}
.pointer{
  cursor:pointer;
}
.focus{

}
.isborder{
  border:none;
}
</style>