<template>
  <div class="selectAll">
    <el-select
      v-model="valueCurrent"
      @change="changeValue"
      multiple
      placeholder="请选择"
      collapse-tags
      :size="size"
    >
      <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value"
      >
      </el-option>
    </el-select>
  </div>
</template>

<script>
// 组件说明：
// 根据el-select改写，添加全选功能
export default {
  props: {
    //选项数组（包含label。value）
    options: { type: Array, default: () => [] },
    // 初始化默认选中项
    valueDefault: { type: Array, default: () => [] },
    size: { type: String, default: "mini" }
  },
  data() {
    return {
      valueCurrent: this.valueDefault,
      allChecked: true //全选标志
    };
  },
  computed: {
    //所有选项全部选中数组（例如valueAll: ["all", "1", "2", "3", "4", "5"],）
    valueAll: function() {
      return this.options.map(item => item.value);
    }
  },
  methods: {
    changeValue(val) {
      if (this.allChecked) {
        if (val.length === this.options.length - 1 && val.includes("all")) {
          // console.log("删除全选按钮");
          val.shift();
          this.allChecked = false;
          // console.log(this.valueCurrent);
        }
        if (!val.includes("all") && this.options.length - 1 === val.length) {
          // console.log("点击取消全选");
          // console.log(val);
          this.valueCurrent = [];
          this.allChecked = false;
        }
      } else {
        if (val.includes("all")) {
          // console.log("点击全选");
          // console.log(val);
          this.valueCurrent = this.valueAll;
          this.allChecked = true;
        }
        if (!val.includes("all") && val.length === this.options.length - 1) {
          // console.log("选择完了所有按钮");
          val.unshift("all");
          this.allChecked = true;
        }
      }
    }
  }
};
</script>


<style>
</style>