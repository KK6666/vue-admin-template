<template>
  <div class="table">
    <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="重写表头" name="first">
        <RewriteHeader></RewriteHeader>
      </el-tab-pane>
      <el-tab-pane label="合并行或列" name="second">
        <SpanMethod></SpanMethod>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import RewriteHeader from "./component/rewriteHeader";
import SpanMethod from "./component/spanMethod";

export default {
  components: {
    RewriteHeader,
    SpanMethod
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