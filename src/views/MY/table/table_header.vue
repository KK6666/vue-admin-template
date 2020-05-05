<template>
  <div class="table_header">
    <span>搜索</span>
    <el-popover
      class="condition_popover"
      placement="bottom"
      width="100"
      trigger="click"
    >
      <span slot="reference">
        <i class="el-icon-arrow-down" style="margin:0 5px;cursor: pointer;"></i>
      </span>
      <div class="condition">
        <el-input v-model="search" size="mini" placeholder="输入关键字搜索" />
        <div class="click_btn" style="padding-top:5px;">
          <span
            style="float:right;cursor: pointer;"
            onmouseover="this.style.color='rgb(64, 158, 255)'"
            onmouseout="this.style.color='black'"
            @click="resetClick()"
            >重置</span
          >
          <span
            style="float:right;margin-right:5px;cursor: pointer;"
            onmouseover="this.style.color='rgb(64, 158, 255)'"
            onmouseout="this.style.color='black'"
            @click="searchClick()"
          >
            查询
          </span>
        </div>
      </div>
    </el-popover>
    <span class="sort">
      <i class="el-icon-caret-top" @click="upClick()"></i>
      <i class="el-icon-caret-bottom" @click="downClick()"></i>
    </span>
  </div>
</template>

<script>
export default {
  props: {
    scope: { type: Object, default: null }
  },
  data() {
    return {
      search: ""
    };
  },
  methods: {
    searchClick() {
      console.log(this.scope);
    },
    resetClick() {
      console.log(this.scope);
    },
    upClick() {
      console.log(this.scope);
    },
    downClick() {
      console.log(this.scope);
    }
  }
};
</script>

<style lang='scss'>
.table_header {
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