<template>
  <div class="home">
    <header>
      <h1>To Do List</h1>
      <input
        type="text"
        v-model="message"
        @keyup.enter="enterNew"
        placeholder="请输入新的任务"
      />
    </header>
    <div class="main">
      <div class="aside">
        <div @click="toHome" :class="isClick === 'pending' ? 'on' : ''">
          未完成（{{ totalList.length }}）
        </div>
        <div @click="toComplete" :class="isClick === 'complete' ? 'on' : ''">
          已完成（{{ completeList.length }}）
        </div>
        <div @click="toTotal" :class="isClick === 'total' ? 'on' : ''">
          全部任务（{{ allList.length }}）
        </div>
      </div>
      <div class="center">
        <div
          v-show="isShow"
          v-for="(item, index) in totalList"
          :key="'pending' + index"
          class="list-container"
        >
          <Pending
            :item="item"
            :index="index"
            @add="addToComplete"
            @del="delItem"
          ></Pending>
        </div>
        <router-view></router-view>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Pending from "./Pending";

export default {
  name: "Home",
  components: {
    Pending
  },
  data() {
    return {
      isShow: true,
      message: "",
      isClick: "pending",
      totalList: [
        { flag: false, message: "今天星期日" },
        { flag: false, message: "明天星期一" },
        { flag: false, message: "后天是星期二" }
      ],
      completeList: []
    };
  },
  computed: {
    allList() {
      return this.totalList.concat(this.completeList);
    }
  },
  // watch: {
  //   $route: {
  //     handler(newV) {
  //       console.log(this.$router.query);
  //       // if (this.$router.query.index) {
  //       //   this.completeList.splice(this.$router.query.index, 1);
  //       // }
  //     },
  //     deep: true,
  //     immediate: true
  //   }
  // },
  methods: {
    enterNew() {
      if (this.message !== "") {
        this.totalList.push({ flag: false, message: this.message });
      } else {
        alert("任务栏不为空");
      }
      this.$router.push({
        query: {
          list: this.allList
        }
      });
      this.message = "";
    },
    toTotal() {
      this.isShow = false;
      this.isClick = "total";

      this.$router.push({
        name: "Total",
        query: {
          list: this.allList
        }
      });
    },
    toComplete() {
      this.isShow = false;
      this.isClick = "complete";

      this.$router.push({
        name: "Complete",
        query: {
          listC: this.completeList
        }
      });
    },
    toHome() {
      this.isShow = true;
      this.isClick = "pending";
      this.$router.push({
        name: "home",
        query: {
          list: this.allList
        }
      });
    },
    addToComplete(data) {
      let arr = this.totalList;
      this.completeList.push(arr[data.ind]);
      arr.splice(data.ind, 1);
    },
    delItem(data) {
      let arr = this.totalList;
      arr.splice(data.ind, 1);
    }
  }
};
</script>
<style lang="scss">
.home {
  width: 800px;
  height: 500px;
  margin: 50px auto;
  overflow: hidden;
  border: 2px solid #ccc;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  header {
    width: 100%;
    height: 150px;
    margin: 0 auto;
    text-align: center;
    border-bottom: 1px solid #ccc;
    color: rgb(63, 63, 62);
    input {
      width: 80%;
      height: 20%;
      outline: none;
      padding: 5px 15px;
      border-radius: 10px;
      font-size: 20px;
    }
  }
  .main {
    display: flex;
    flex: 1;
    .aside {
      width: 150px;
      border-right: 1px solid #ccc;
      border-top: none;
      text-align: center;
      .on {
        background-color: rgb(185, 190, 185);
      }
      div {
        border-bottom: 1px solid #ccc;
        height: 60px;
        line-height: 60px;
        color: rgb(63, 63, 62);
        cursor: pointer;
        a {
          text-decoration: none;
          color: rgb(63, 63, 62);
        }
      }
    }
  }
  .center {
    flex: 1;
    padding: 10px 20px;
  }
}

.list-container {
  height: 30px;
  line-height: 30px;
  font-size: 14px;
}
</style>
