<template>
  <div class="table">
    <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="全选" name="first">
        <SelectAll></SelectAll>
      </el-tab-pane>
      <el-tab-pane label="配置管理" name="second">配置管理</el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import SelectAll from "./components/selectAll";
export default {
  components: {
    SelectAll
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