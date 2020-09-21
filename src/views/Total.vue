<template>
  <div class="total-container">
    <div
      v-for="(item, index) in totalList"
      :key="'total' + index"
      class="list-container"
    >
      <el-button icon="el-icon-search" circle size="mini"></el-button>

      {{ item.message }}
    </div>
  </div>
</template>
<script>
export default {
  name: "Total",
  data() {
    return {
      totalList: []
    };
  },
  created() {
    this.totalList = this.$route.query.list;
  }
  // watch: {
  //   $route: {
  //     handler(newV) {
  //       this.totalList = this.$route.query.list;
  //     },
  //     deep: true,
  //     immediate: true
  //   }
  // }
};
</script>
<style lang="scss">
.total-container {
  .list-container {
    height: 30px;
    line-height: 30px;
    font-size: 14px;
  }
  div {
    margin: 10px auto;
    padding: 10px auto;
  }
}
</style>
