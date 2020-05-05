<template>
  <div class="rewrite_header">
    <h1>重写表头，支持筛选、搜索</h1>
    <div class="content">
      <el-table style="width: 100%" :data="tableData" border>
        <el-table-column label="Date" prop="date"> </el-table-column>
        <el-table-column label="Name" prop="name"> </el-table-column>
        <el-table-column prop="name">
          <template slot="header" slot-scope="scope">
            <TableHeader :scope="scope"></TableHeader>
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>
import TableHeader from "./table_header.vue";
export default {
  components: {
    TableHeader
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
      search: ""
    };
  },
  methods: {
    searchClick(scope) {
      console.log(scope);
      // console.log(row);
    },
    resetClick(scope) {
      console.log(scope);
      // console.log(row);
    },

    /////////////////////////////////////////
    handleEdit(index, row) {
      console.log(index, row);
    },
    handleDelete(index, row) {
      console.log(index, row);
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