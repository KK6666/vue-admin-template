<template>
  <div class="table">
    <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="全选" name="first">
        <SelectAll></SelectAll>
      </el-tab-pane>
      <el-tab-pane label="溢出隐藏" name="second">
        <RewriteCss></RewriteCss>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import SelectAll from "./components/selectAll";
import RewriteCss from "./components/rewriteCss";
export default {
  components: {
    SelectAll,
    RewriteCss
  },
  data() {
    return {
      activeName: "first"
    };
  },
  methods: {
    handleClick(tab, event) {
      console.log(tab, event);
    }
  }
};
</script>

<style>
</style>