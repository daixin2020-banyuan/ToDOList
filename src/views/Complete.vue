<template>
  <div class="com-container">
    <div
      v-for="(item, index) in Complete"
      :key="'Complete' + index"
      class="list-container"
    >
      <el-button
        type="success"
        icon="el-icon-check"
        circle
        size="mini"
      ></el-button>

      {{ item.message }}
      <i class="el-icon-delete" style="float:right" @click="deleteItem"></i>
    </div>
  </div>
</template>
<script>
export default {
  name: "Complete",
  data() {
    return {
      Complete: []
    };
  },
  created() {
    this.Complete = this.$route.query.listC;
  },
  methods: {
    deleteItem() {
      console.log(1);
      // this.$router.push({
      //   query: {
      //     index: this.Complete.index
      //   }
      // });
    }
  }
};
</script>
<style scoped lang="scss">
.com-container {
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
