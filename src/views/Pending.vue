<template>
  <div class="pending-container">
    <div>
      <el-button
        type="warning"
        icon="el-icon-star-off"
        circle
        size="mini"
        @click="checkedItem"
      ></el-button>

      {{ item.message }}
      <template slot-scope="scope">
        <el-button @click.native.prevent="deleteRow(scope.$index)" size="small">
          移除
        </el-button>
      </template>

      <i class="el-icon-delete" style="float:right" @click="deleteitem"></i>
    </div>
  </div>
</template>
<script>
export default {
  name: "Pending",
  data() {
    return {
      pendingList: []
    };
  },
  methods: {
    checkedItem() {
      this.$emit("add", {
        ind: this.index
      });
    },
    deleteitem() {
      this.$emit("del", {
        ind: this.index
      });
    }
  },
  props: {
    item: {
      type: Object,
      require: true
    },
    index: {
      type: Number
    }
  }
};
</script>
<style scoped lang="scss">
.pending-container {
  height: 30px;
  div {
    margin: 10px auto;
    padding: 10px auto;
  }
}
</style>
