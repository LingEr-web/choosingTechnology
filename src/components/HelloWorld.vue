<template>
  <div class="hello">
    <!-- table -->
    <!-- <h3>双击编辑单元格，添加一行空数据</h3>
    <div class="header">
      <el-button type="primary" size="mini" @click="add">添加</el-button>
    </div>
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
    </el-table> -->

    <!-- table2 -->
    <h3>另一种方式实现编辑单元格，添加数据</h3>
    <div class="header">
      <el-button type="primary" size="mini" @click="add2">添加</el-button>
    </div>
    <el-table :data="tableData2" highlight-current-row header-row-class-name="table-headers" @cell-dblclick="tableDbEdit2" style="width: 100%">
      <el-table-column label="编号" type="index" width="50"></el-table-column>
      <el-table-column label="默认" width="65">
        <template slot-scope="scope">
          <div>
            <el-radio :label="scope.row.id" v-model="templateRadio" @change.native="getTemplateRow2(scope.$index,scope.row)">&nbsp;</el-radio>
          </div>
        </template>
      </el-table-column>
      <el-table-column property="date" label="日期">
        <template slot-scope="scope">
		      <el-date-picker v-if="scope.row.date.edit"
		        v-model="scope.row.date.value"
		        ref="date"
		        style="width: 100%"
		        type="date"
		        value-format="yyyy-MM-dd"
		        @blur="editBlur(scope.row,scope.row.date)">
		      </el-date-picker>
		      <span v-else>{{ scope.row.date.value }}</span>
		    </template>
      </el-table-column>
      <el-table-column property="name" label="姓名">
        <template slot-scope="scope">
		      <el-input v-if="scope.row.name.edit"
		        ref="name"
		        v-model="scope.row.name.value"
		        style="width: 100%"
		        @blur="editBlur(scope.row,scope.row.name)">
		      </el-input>
		      <span v-else>{{ scope.row.name.value }}</span>
		    </template>
      </el-table-column>
      <el-table-column property="address" label="地址">
        <template slot-scope="scope">
		      <el-input v-if="scope.row.address.edit"
		        ref="address"
		        v-model="scope.row.address.value"
		        style="width: 100%"
		        @blur="editBlur(scope.row,scope.row.address)">
		      </el-input>
		      <span v-else>{{ scope.row.address.value }}</span>
		    </template>
      </el-table-column>
    </el-table>
    <!-- 树形 -->
    <!-- <el-tree :data="treeData" :props="defaultProps" @node-click="handleNodeClick"></el-tree> -->
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      templateRadio:'1',
      /* tableData: [{
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
      */
      tableData2: [{
        id:'1',
        date: {value:'2016-05-02',edit:false},
        name: {value:"王一",edit:false},
        address: {value:"北京市丰台区1号",edit:false}
      }, {
        id:'2',
        date: {value:'2016-05-02',edit:false},
        name: {value:"王一",edit:false},
        address: {value:"北京市丰台区1号",edit:false}
      }, {
        id:'3',
        date: {value:'2016-05-02',edit:false},
        name: {value:"王一",edit:false},
        address: {value:"北京市丰台区1号",edit:false}
      }, {
        id:'4',
        date: {value:'2016-05-02',edit:false},
        name: {value:"王一",edit:false},
        address:{value:"北京市丰台区1号",edit:false}
      }],
      currentRow: null,
      /*treeData: [{
        label: '一级 1',
        children: [{
          label: '二级 1-1',
          children: [{
            label: '三级 1-1-1'
          }]
        }]
        }, {
          label: '一级 2',
          children: [{
            label: '二级 2-1',
            children: [{
              label: '三级 2-1-1'
            }]
          }, {
            label: '二级 2-2',
            children: [{
              label: '三级 2-2-1'
            }]
          }]
        }, {
          label: '一级 3',
          children: [{
            label: '二级 3-1',
            children: [{
              label: '三级 3-1-1'
            }]
          }, {
            label: '二级 3-2',
            children: [{
              label: '三级 3-2-1'
            }]
          }]
        }],
      defaultProps: {
        children: 'children',
        label: 'label'
      }*/
    }
  },
  methods: {
      // 单选
      /*getTemplateRow(index,row){
        console.log(index,row)
      },*/
      // 双击单元格可编辑
      /*tableDbEdit(row, column, cell, event){
        let _this = this;
        if (column.label != "单选") {
            let flag=true;
            let texts = event.target.innerText
            event.target.innerHTML = "";
            let cellInput = document.createElement("input");
            cellInput.value = texts;
            cellInput.setAttribute("type", "text");
            cellInput.style.width = "80%";
            cell.appendChild(cellInput);
            cellInput.focus()
            cellInput.onblur = function() {
              if(cellInput.value==""){
                _this.$notify.error({
                  title: '',
                  message: '内容不能为空！'
                });
                cellInput.focus()
              }else{
                _this.$notify.success({
                  title: '',
                  message: '修改成功！'
                });
                cell.removeChild(cellInput);
                event.target.innerHTML = cellInput.value;
                flag=true
              }
            };
        }
      },*/
      // 添加
      /*add(){
        this.tableData.push({
          date: '2016',
          name: '王2',
          address: '北京市丰台区2号'
        })
      },*/
      // 单选
      getTemplateRow2(index,row){
        console.log(index,row)
      },
      // 双击单元格可编辑
      tableDbEdit2(row, column, cell, event){
        let _this = this;
        if(row[column.property]){
          row[column.property].edit=true
          setTimeout(()=>{
            _this.$refs[column.property].focus()
          })
        }
      },
      // 失去焦点验证提交
      editBlur(row,td){
        td.edit=false
        this.$notify.success({
          title: '',
          message: '修改成功！'
        });
      },
      // 添加
      add2(){
        this.tableData2.push({
          id:this.tableData2[this.tableData2.length-1].id+1,
          date: {value:'',edit:true},
          name: {value:"",edit:true},
          address:{value:"",edit:true}
        })
      },
      // 树状
      /*handleNodeClick(data) {
        console.log(data);
      }*/
    }
}
</script>
<style scoped>
.pointer{
  cursor:pointer;
}
.header{
  width: 100%;
  display: flex;
  justify-content: flex-start;
}
.table-headers{
  background-color: blue;
}
</style>
<style lang="">
  .table-headers{
  background-color: blue;
}
</style>