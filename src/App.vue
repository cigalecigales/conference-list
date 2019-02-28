<template>
  <div id="app">
    <div class="logo_area">
      <!-- <img alt="Vue logo" src="./assets/logo.png" style="width: 100px;"> -->
      Conference List
    </div>
    <div class="sub_area">日本国内で開催されるカンファレンス等のIT系大型イベントのみを集めたリスト</div>
    <div class="input_area">
      <input
        type="text"
        placeholder="Find your favorite conference ..."
        v-model="filterText"
        @input="filterList"
        class="input_text"
      >
    </div>
    <div class="card_area">
      <Card v-for="d in data" :data="d" :key="d.id"/>
    </div>
    <div class="github" @click="openGithub">
      <i class="fab fa-github"></i>
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import items from "./data/items.json";

export default {
  name: "app",
  components: {
    Card
  },
  data() {
    return {
      data: [],
      filterText: ""
    };
  },
  created() {
    this.filterList();
  },
  methods: {
    filterList() {
      // 今日
      const today = new Date()
      // 開催中 or 開催前イベントリスト
      let beforeList = [];
      // 過去のイベントリスト
      let afterList = [];

      items.forEach(d => {
        // 追加済みフラグ
        let addedFlg = false;

        // 入力欄が空でない場合
        if (this.filterText) {
          if (
            !d.name.includes(this.filterText) ||
            !d.description.includes(this.filterText)
          ) {
            return;
          }
        }

        d.eventDate.forEach(ed => {
          const eventDate = new Date(ed);
          // イベント開催当日 or イベント開催前の場合
          if (today.toString() === eventDate.toString()) {
            if (!addedFlg) {
              // イベント当日
              d.status = 1;
              addedFlg = true;
              beforeList.push(d)
            }
          } else if (today.getTime() < eventDate.getTime()) {
            if (!addedFlg) {
              // イベント開催前
              d.status = 2;
              addedFlg = true;
              beforeList.push(d)
            }
          }
        });
        // イベント開催後の場合
        if (!addedFlg) {
          d.status = 3;
          afterList.push(d)
        }
      });

      let result = beforeList.concat(afterList)
      this.data = result.concat()
    },
    openGithub() {
      window.open('https://github.com/cigalecigales/conference-list')
    }
  }
};
</script>

<style>
* {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 16px;
  box-sizing: border-box;
  outline: none;
}

html,
body {
  background: #fdfdfd;
}

.logo_area {
  text-align: center;
  margin-top: 20px;
  margin-bottom: 20px;
  font-size: 1.5rem;
  font-weight: bold;
}

.sub_area {
  text-align: center;
  font-size: 0.8rem;
  margin-bottom: 10px;
}

.input_area {
  width: 95%;
  max-width: 500px;
  margin: 0 auto;
}

.input_text {
  width: 100%;
  padding: 5px 8px;
  border-radius: 3px;
  border: 1px solid #ffa500;
}

.input_text:focus {
  border: 1px solid #f57868;
}

.card_area {
  margin: 0 auto;
  margin-bottom: 50px;
  padding: 5px;
  width: 95%;
  /* column-count: 3;
  column-gap: 10px; */
  margin-top: 30px;
  display: grid;
  grid-gap: 10px;
  grid-template-columns: repeat(auto-fill, minmax(250px,1fr));
  grid-auto-rows: auto;
  
}

.github {
  background: linear-gradient(
      to top right,
      rgba(255, 255, 255, 0) 50%,
      #ffa500 50.5%
    )
    no-repeat top left/100% 100%;
  width: 60px;
  height: 60px;
  text-align: right;
  position: fixed;
  right: 0;
  top: 0;
}

.github:hover {
  cursor: pointer;
  background: linear-gradient(
      to top right,
      rgba(255, 255, 255, 0) 50%,
      #f57868 50.5%
    )
    no-repeat top left/100% 100%;
}

.github > i {
  font-size: 1.5rem;
  padding: 6px;
  color: #ffffff;
}
</style>
