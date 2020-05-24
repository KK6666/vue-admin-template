<template>
  <div class="table_header">
    <span class="heeader_name" :class="isActiveFilter ? 'active' : ''">{{
      headerName
    }}</span>
    <el-popover
      class="filter_popover"
      placement="bottom"
      width="150"
      trigger="click"
      v-model="visible"
    >
      <span slot="reference">
        <i class="el-icon-arrow-down" style="margin:0 5px;cursor: pointer;"></i>
      </span>
      <div class="filter">
        <!-- el-scrollbar必须给定固定高度 -->
        <el-scrollbar style="">
          <el-checkbox
            :indeterminate="isIndeterminate"
            v-model="checkAll"
            @change="handleCheckAllChange"
            >全选</el-checkbox
          >
          <el-checkbox-group
            v-model="checkedOptions"
            @change="handleCheckedOptionsChange"
          >
            <el-checkbox
              v-for="option in options"
              :label="option"
              :key="option"
              style="display:block;"
              >{{ option }}
            </el-checkbox>
          </el-checkbox-group>
        </el-scrollbar>

        <div class="click_btn" style="padding-top:5px;">
          <el-button
            type="text"
            style="float:right;padding:0;font-size:12px;color:#606266;"
            onmouseover="this.style.color='rgb(64, 158, 255)'"
            onmouseout="this.style.color='#606266'"
            @click="resetClick()"
            >重置</el-button
          >
          <el-button
            type="text"
            style="float:right;padding:0;font-size:12px;color:#606266;margin-right:5px;"
            :style="{ color: filter_forbid ? '' : '#606266' }"
            onmouseover="this.style.color='rgb(64, 158, 255)'"
            onmouseout="this.style.color='#606266'"
            @click="filterClick()"
            :disabled="filter_forbid"
            >查询</el-button
          >
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
      visible: false, //是否显示el-popovper
      checkedOptions: [],
      options: [
        "上海",
        "北京",
        "广州",
        "深圳",
        "上海6",
        "北京11",
        "广州11",
        "深圳11",
        "上海11",
        "北京2",
        "广州2",
        "深圳2",
        "上海2",
        "北京3",
        "广州3",
        "深圳3"
      ],
      isIndeterminate: false,
      checkAll: false,
      isActiveFilter: false, //判断当前是否为筛选激活装填
      filter_forbid: true
    };
  },
  watch: {
    clearNum: function() {
      this.checkedOptions = [];
      this.$refs.up.style.color = "";
      this.$refs.down.style.color = "";
    },
    checkedOptions: {
      handler() {
        this.filter_forbid = this.checkedOptions.length ? false : true;
      },
      deep: true
    }
  },
  methods: {
    // 查询点击
    filterClick() {
      // console.log(this.scope);
      this.$emit("filterClick", [this.scope, this.checkedOptions]);
      //关闭popover
      this.visible = false;
      this.isActiveFilter = true;
    },
    //重置点击
    resetClick() {
      this.$emit("resetClick", this.scope);
      //关闭popover
      this.visible = false;
      this.isActiveFilter = false;
      this.checkedOptions = [];
      this.handleCheckedOptionsChange(this.checkedOptions);
    },
    //向上排序点击
    upClick() {
      this.$emit("upClick", this.scope);
      //排序icon颜色变化
      this.$refs.up.style.color = "rgb(64, 158, 255)";
      setTimeout(() => {
        this.$refs.up.style.color = "";
      }, 500);
    },
    //向下排序点击
    downClick() {
      this.$emit("downClick", this.scope);
      //排序icon颜色变化
      this.$refs.down.style.color = "rgb(64, 158, 255)";
      setTimeout(() => {
        this.$refs.down.style.color = "";
      }, 500);
    },
    handleCheckAllChange(val) {
      this.checkedOptions = val ? this.options : [];
      this.isIndeterminate = false;
    },
    handleCheckedOptionsChange(value) {
      let checkedCount = value.length;
      this.checkAll = checkedCount === this.options.length;
      this.isIndeterminate =
        checkedCount > 0 && checkedCount < this.options.length;
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
    &.active {
      color: rgb(64, 158, 255);
    }
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

<style lang="scss">
.filter {
  .el-scrollbar {
    height: 150px;
    .el-scrollbar__wrap {
      overflow-y: scroll;
      overflow-x: hidden;
    }
  }
}
</style>