<template>
  <div class="hello">
    <!-- table -->
    <el-table :data="tableData" highlight-current-row  @cell-dblclick="tableDbEdit" style="width: 100%">
      <el-table-column label="编号" type="index" width="50"></el-table-column>
      <el-table-column label="默认" width="65">
        <template slot-scope="scope">
          <div>
            <el-radio :label="scope.row.date" v-model="templateRadio" @change.native="getTemplateRow(scope.$index,scope.row)">&nbsp;</el-radio>
          </div>
        </template>
      </el-table-column>
      <el-table-column property="date" label="日期"></el-table-column>
      <el-table-column property="name" label="姓名"></el-table-column>
      <el-table-column property="address" label="地址"></el-table-column>
    </el-table>
    <!-- 树形 -->
    
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      templateRadio:'2016-05-04',
      tableData: [{
          id:'1',
          date: '2016-05-02',
          name: '王1',
          address: '北京市丰台区1号'
        }, {
          id:'2',
          date: '2016-05-04',
          name: '王2',
          address: '北京市丰台区2号'
        }, {
          id:'3',
          date: '2016-05-01',
          name: '王3',
          address: '北京市丰台区3号'
        }, {
          id:'4',
          date: '2016-05-03',
          name: '王4',
          address: '北京市丰台区4号'
        }],
        currentRow: null
    }
  },
  methods: {
      getTemplateRow(index,row){
        console.log(index,row)
      },
      // 双击单元格可编辑
      tableDbEdit(row, column, cell, event){
        if (column.label != "单选") {
            let texts = event.target.innerText
            event.target.innerHTML = "";
            let cellInput = document.createElement("input");
            cellInput.value = texts;
            cellInput.setAttribute("type", "text");
            cellInput.style.width = "80%";
            cell.appendChild(cellInput);
            cellInput.focus()
            cellInput.onblur = function() {
              cell.removeChild(cellInput);
              event.target.innerHTML = cellInput.value;
            };
        }
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
</style>