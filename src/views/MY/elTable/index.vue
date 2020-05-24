<template>
  <div class="table">
    <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="重写表头" name="first">
        <RewriteHeader></RewriteHeader>
      </el-tab-pane>
      <el-tab-pane label="配置管理" name="second">配置管理</el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import RewriteHeader from "./component/rewriteHeader";
export default {
  components: {
    RewriteHeader
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