<template>
  <div class="rewrite_header">
    <h1>重写表头，支持筛选、搜索</h1>
    <div class="content">
      <el-table style="width: 100%" :data="tableData" border>
        <el-table-column label="Date" prop="date"> </el-table-column>
        <el-table-column label="Name" prop="name">
          <template slot="header" slot-scope="scope">
            <!-- 
              表头组件说明：
              headerName-表头名
              scope-当前列的scope
              filterClick-查询点击
              resetClick-重置点击
              upClick-向上排序点击
              downClick-向下排序点击
              clearNum-通过该变该数值，触发组件内筛选排序状态清空
             -->
            <TableHeaderInput
              headerName="输入框"
              :scope="scope"
              :clearNum="clearNum"
              @filterClick="filterClick"
              @resetClick="resetClick"
              @upClick="upClick"
              @downClick="downClick"
            ></TableHeaderInput>
          </template>
        </el-table-column>
        <el-table-column prop="name">
          <template slot="header" slot-scope="scope">
            <!-- 
              表头组件说明：
              headerName-表头名
              scope-当前列的scope
              filterClick-查询点击
              resetClick-重置点击
              upClick-向上排序点击
              downClick-向下排序点击
              clearNum-通过该变该数值，触发组件内筛选排序状态清空
             -->
            <TableHeaderCheck
              headerName="选择框"
              :scope="scope"
              :clearNum="clearNum"
              @filterClick="filterClick"
              @resetClick="resetClick"
              @upClick="upClick"
              @downClick="downClick"
            ></TableHeaderCheck>
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>
import TableHeaderInput from "./TableHeaderInput.vue";
import TableHeaderCheck from "./TableHeaderCheck.vue";
export default {
  components: {
    TableHeaderInput,
    TableHeaderCheck
  },
  data() {
    return {
      tableData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄"
        },
        {
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1517 弄"
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1519 弄"
        },
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1516 弄"
        }
      ],
      clearNum: 0
    };
  },
  methods: {
    filterClick(data) {
      // data[0]-scope，data[1]-input或多选框的值
      console.log(data);
    },
    resetClick(scope) {
      console.log(scope);
      // console.log(row);
    },
    upClick(scope) {
      console.log(scope);
      // console.log(row);
    },
    downClick(scope) {
      console.log(scope);
      // console.log(row);
    }
  }
};
</script>

<style lang='scss'>
.wrap {
  display: flex;
  align-items: center;
  .sort {
    display: inline-flex;
    flex-direction: column;
    justify-content: center;
    i {
      height: 6px;
      line-height: 6px;
      cursor: pointer;
    }
  }
}
</style>

<style lang='scss' scoped>
.rewrite_header {
  padding: 10px;
}
</style>