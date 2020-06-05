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
    <h3>编辑单元格，添加数据</h3>
    <div class="header">
      <el-button type="primary" size="mini" @click="add2" icon="el-icon-plus">新增</el-button>
    </div>
    <el-table border :data="tableData2" :header-cell-style="{background:'#0160c1',color:'#ffffff'}" highlight-current-row  @cell-dblclick="tableDbEdit2" style="width: 100%">
      <el-table-column label="序号" type="index" width="120"></el-table-column>

      <el-table-column label="编码" property="code">
        <template slot-scope="scope">
		      <el-input v-if="scope.row.code.edit && scope.row.explain.value!=='系统内置'"
		        ref="code"
		        v-model="scope.row.code.value"
		        style="width: 100%"
		        @blur="editBlur(scope.row,scope.row.code)">
		      </el-input>
		      <span v-else :class="{'grey': scope.row.explain.value =='系统内置'}">{{ scope.row.code.value }}</span>
		    </template>
      </el-table-column>

      <el-table-column property="name" label="名称">
        <template slot-scope="scope">
		      <el-input v-if="scope.row.name.edit && scope.row.explain.value!=='系统内置'"
		        ref="name"
		        v-model="scope.row.name.value"
		        style="width: 100%"
		        @blur="editBlur(scope.row,scope.row.name)">
		      </el-input>
		      <span v-else :class="{'grey': scope.row.explain.value =='系统内置'}">{{ scope.row.name.value }}</span>
		    </template>
      </el-table-column>

      <el-table-column label="默认">
        <template slot-scope="scope">
          <div>
            <el-radio :label="scope.row.id" v-model="templateRadio" @change.native="getTemplateRow2(scope.$index,scope.row)">&nbsp;</el-radio>
          </div>
        </template>
      </el-table-column>

      <el-table-column property="explain" label="说明">
        <template slot-scope="scope">
		      <el-input v-if="scope.row.explain.edit && scope.row.explain.value!=='系统内置'"
		        ref="explain"
		        v-model="scope.row.explain.value"
		        style="width: 100%"
		        @blur="editBlur(scope.row,scope.row.explain)">
		      </el-input>
		      <span v-else :class="{'grey': scope.row.explain.value =='系统内置'}">{{ scope.row.explain.value }}</span>
		    </template>
      </el-table-column>

      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button
            size="mini"
            type="danger"
            icon="el-icon-delete"
            :disabled = "scope.row.explain.value =='系统内置'"
            @click="del(scope.row.id)">删除</el-button>
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
          code: {value:'01',edit:false},
          name: {value:"公开",edit:false},
          explain: {value:"系统内置",edit:false}
        }, {
          id:'2',
          code: {value:'02',edit:false},
          name: {value:"内部",edit:false},
          explain: {value:"系统内置",edit:false}
        }, {
          id:'3',
          code: {value:'03',edit:false},
          name: {value:"秘密",edit:false},
          explain: {value:"系统内置",edit:false}
        }, {
          id:'4',
          code:{value:'04',edit:false},
          name: {value:"机密",edit:false},
          explain:{value:"系统内置",edit:false}
        },{
          id:'5',
          code:{value:'05',edit:false},
          name: {value:"绝密",edit:false},
          explain:{value:"系统内置",edit:false}
        },{
          id:'6',
          code:{value:'06',edit:false},
          name: {value:"非密",edit:false},
          explain:{value:"用户自定义",edit:false}
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
        if(row[column.property] && row.explain.value!=='系统内置'){
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
          id: this.tableData2[this.tableData2.length-1].id+1,
          code: {value:'03',edit:false},
          name: {value:"秘密",edit:false},
          explain: {value:"用户自定义",edit:false}
        })
      },
      // 删除
      del(id){
        let _this=this; 
        _this.$confirm('此操作将永久删除该数据, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          let index='';
          for(let i=0;i<_this.tableData2.length;i++){
            if(_this.tableData2[i].id==id){
              index=i;
              break;
            }
          }
          _this.tableData2.splice(index,1)
          _this.$notify.success({
            title: '',
            message: '删除成功'
          });
        }).catch(() => {
          _this.$notify.success({
            title: '',
            message: '取消删除'
          });        
        });
      }
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
  margin-bottom: 10px;
}
.table-headers{
  background-color: blue;
}
.grey{
  color: #aeb0b3;
}
</style>