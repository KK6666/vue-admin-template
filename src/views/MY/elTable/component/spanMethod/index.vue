<template>
  <div class="spanMethod">
    <el-table
      :data="tableData"
      :span-method="objectSpanMethod"
      border
      style="width: 100%; margin-top: 20px"
    >
      <el-table-column prop="id" label="ID" width="180"> </el-table-column>
      <el-table-column prop="name" label="姓名"> </el-table-column>
      <el-table-column prop="amount1" label="数值 1（元）"> </el-table-column>
      <el-table-column prop="amount2" label="数值 2（元）"> </el-table-column>
      <el-table-column prop="amount3" label="数值 3（元）"> </el-table-column>
    </el-table>
  </div>
</template>

<script>
// 项目要求：
// （1）第一列合并的行数根据后台传来的数据进行判断，同一类的就进行合并，所以这个需要判断每一类都多少个数据，就合并多少行 getSpanArr方法功能就是知道合并的行数
// （2）每一类的最后一行都进行合并，合并除了第一列之外的所有的列，所以这个需要知道你要合并的所有的列是在第几行

export default {
  data() {
    return {
      tableData: [
        {
          id: "11",
          name: "王小虎",
          amount1: "234",
          amount2: "3.2",
          amount3: 10
        },
        {
          id: "11",
          name: "王小虎",
          amount1: "165",
          amount2: "4.43",
          amount3: 12
        },
        {
          id: "22",
          name: "王小虎",
          amount1: "324",
          amount2: "1.9",
          amount3: 9
        },
        {
          id: "33",
          name: "王小虎",
          amount1: "621",
          amount2: "2.2",
          amount3: 17
        },
        {
          id: "33",
          name: "王小虎",
          amount1: "539",
          amount2: "4.1",
          amount3: 15
        },
        {
          id: "44",
          name: "王小虎",
          amount1: "539",
          amount2: "4.1",
          amount3: 15
        },
        {
          id: "44",
          name: "王小虎",
          amount1: "539",
          amount2: "4.1",
          amount3: 15
        }
      ],
      spanArr: [],
      pos: null
    };
  },
  created() {
    this.getSpanArr(this.tableData);
  },
  methods: {
    getSpanArr(data) {
      console.log(data); //从后台获取的数据
      this.spanArr = [];
      for (var i = 0; i < data.length; i++) {
        if (i === 0) {
          // 如果是第一条记录（即索引是0的时候），向数组中加入１
          this.spanArr.push(1);
          this.pos = 0;
        } else {
          if (data[i].id === data[i - 1].id) {
            // 如果useName相等就累加，并且push 0
            this.spanArr[this.pos] += 1;
            this.spanArr.push(0);
          } else {
            // 不相等push 1
            this.spanArr.push(1);
            this.pos = i;
          }
        }
      }
      console.log(this.spanArr);
    },
    objectSpanMethod({ row, column, rowIndex, columnIndex }) {
      // columnIndex === 0 找到第一列，实现合并随机出现的行数
      if (columnIndex === 0) {
        const _row = this.spanArr[rowIndex];
        const _col = _row > 0 ? 1 : 0;
        return {
          rowspan: _row,
          colspan: _col
        };
      }
      // columnIndex === 1 找到第二列，实现合并第2到最后一列
      else if (columnIndex === 1) {
        for (var i = 0; i < this.spanArr.length; i++) {
          // 筛选数组中数值不是0的数
          if (this.spanArr[i] > 1) {
            // console.log(i, this.spanArr[i])
            // 发现的规律：当前索引 + 索引所对应的数值 - 1 = 所要合并的第几行
            if (rowIndex === i + this.spanArr[i] - 1) {
              this.$nextTick(() => {
                console.log(
                  document.querySelectorAll(
                    `tr:nth-of-type(${i + this.spanArr[i]})`
                  ),
                  i + this.spanArr[i]
                );
                document.querySelectorAll(
                  `tr:nth-of-type(${i + this.spanArr[i]}) td div`
                )[0].style.float = "right";
                document.querySelectorAll(
                  `tr:nth-of-type(${i + this.spanArr[i]}) td div`
                )[0].style.marginRight = "10%";
              }, 0);
              return {
                rowspan: 1,
                colspan: 4
              };
            }
          }
        }
      }
    }
  }
};
</script>

<style>
</style>