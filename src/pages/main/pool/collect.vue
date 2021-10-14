<template>
  <div class="wrapper" style="height: auto; min-height: 100%;">
    <common-header></common-header>
    <common-sidebar></common-sidebar>
    <collect></collect>
  </div>
</template>
<script>
import CommonHeader from "@/components/common/CommonHeader";
import CommonSidebar from "@/components/common/CommonSidebar";
import Collect from "@/components/main/pool/Collect";
export default {
  components: {
    CommonHeader,
    CommonSidebar,
    Collect
  }
};
</script>

<style scoped>

</style>