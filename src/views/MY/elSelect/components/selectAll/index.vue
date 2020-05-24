<template>
  <div class="selectAll">
    <KSelectAll
      :options="options"
      :valueDefault="valueDefault"
      size="mini"
    ></KSelectAll>
  </div>
</template>

<script>
import KSelectAll from "./components/KSelectAll.vue";
export default {
  components: { KSelectAll },
  data() {
    return {
      options: [
        { value: "all", label: "全选" },
        {
          value: "1",
          label: "黄金糕"
        },
        {
          value: "2",
          label: "双皮奶"
        },
        {
          value: "3",
          label: "蚵仔煎"
        },
        {
          value: "4",
          label: "龙须面"
        },
        {
          value: "5",
          label: "北京烤鸭"
        }
      ],
      valueDefault: ["1", "2"]
    };
  },
  computed: {},
  methods: {}
};
</script>


<style>
</style>