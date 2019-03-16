<template>
  <div class="vuc-header"><slot></slot></div>
</template>
<script>
  import HeadLeft from "./HeadLeft";
  import HeadRight from "./HeadRight";
  import HeadTitle from "./HeadTitle";

  export default {
    relativeComp: {
      HeadLeft, HeadRight, HeadTitle
    },
    name: 'vue-header'
  }
</script>
<style type="text/css" scoped>
.vuc-header{
  position: relative;
  z-index: 1;
}
</style>
