<template>
  <div class="table_header">
    <span class="heeader_name">{{ headerName }}</span>
    <el-popover
      class="filter_popover"
      placement="bottom"
      width="100"
      trigger="click"
      v-model="visible"
    >
      <span slot="reference">
        <i class="el-icon-arrow-down" style="margin:0 5px;cursor: pointer;"></i>
      </span>
      <div class="filter">
        <el-input v-model="search" size="mini" placeholder="输入关键字搜索" />
        <div class="click_btn" style="padding-top:5px;">
          <span
            style="float:right;cursor: pointer;font-size:12px;color:'#606266'"
            onmouseover="this.style.color='rgb(64, 158, 255)'"
            onmouseout="this.style.color='#606266'"
            @click="resetClick()"
            >重置</span
          >
          <span
            style="float:right;margin-right:5px;cursor: pointer;font-size:12px;color:'#606266'"
            onmouseover="this.style.color='rgb(64, 158, 255)'"
            onmouseout="this.style.color='#606266'"
            @click="filterClick()"
          >
            查询
          </span>
        </div>
      </div>
    </el-popover>
    <span class="sort">
      <i ref="up" class="el-icon-caret-top" @click="upClick()"></i>
      <i ref="down" class="el-icon-caret-bottom" @click="downClick()"></i>
    </span>
  </div>
</template>

<script>
export default {
  props: {
    //表头名字
    headerName: { type: String, default: "" },
    //当前操作列数据
    scope: { type: Object, default: null },
    //改变触发清空筛选排序状态
    clearNum: { type: Number, default: 0 }
  },
  data() {
    return {
      search: "",
      visible: false,
      isForbidClick: true
    };
  },
  watch: {
    clearNum: function() {
      this.search = "";
      this.$refs.up.style.color = "";
      this.$refs.down.style.color = "";
    },
    search: function() {
      // this.isForbidClick = this.search ? false : true;
    }
  },
  methods: {
    // 查询点击
    filterClick() {
      // console.log(this.scope);
      this.$emit("filterClick", this.scope);
      //关闭popover
      this.visible = false;
    },
    //重置点击
    resetClick() {
      this.search = "";
      this.$emit("resetClick", this.scope);
      //关闭popover
      this.visible = false;
    },
    //向上排序点击
    upClick() {
      this.$emit("upClick", this.scope);
      //排序icon颜色变化
      this.$refs.up.style.color = "rgb(64, 158, 255)";
      this.$refs.down.style.color = "";
    },
    //向下排序点击
    downClick() {
      this.$emit("downClick", this.scope);
      //排序icon颜色变化
      this.$refs.down.style.color = "rgb(64, 158, 255)";
      this.$refs.up.style.color = "";
    }
  }
};
</script>

<style lang='scss' scoped>
.table_header {
  display: flex;
  align-items: center;
  .heeader_name {
    font-size: 14px;
  }
  .sort {
    height: 10px;
    display: inline-flex;
    flex-direction: column;
    justify-content: center;
    i {
      display: inline-flex;
      height: 8px;
      line-height: 8px;
      cursor: pointer;
    }
  }
}
</style>