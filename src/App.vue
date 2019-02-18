<template>
  <div id="app">
    <div class="logo_area">
      <img alt="Vue logo" src="./assets/logo.png" style="width: 100px;">
    </div>
    <div class="input_area">
      <input type="text" placeholder="Find your favorite conference ..." class="input_text">
    </div>
    <div class="card_area">
      <Card v-for="d in data" :data="d" :key="d.id" />
    </div>
  </div>
</template>

<script>
import Card from './components/Card.vue'
import data from './data/items.json'

export default {
  name: 'app',
  components: {
    Card
  },
  data() {
    return {
      data: data
    }
  }
}
</script>

<style>
* {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  font-size: 16px;
  box-sizing: border-box;
  outline: none;
}

html, body {
  background: #fdfdfd;
}

.logo_area {
  text-align: center;
  margin-top: 20px;
  margin-bottom: 20px;
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
  border: 1px solid #ffbb87;
}

.input_text:focus {
  border: 1px solid #f57868;
}

.card_area {
  margin: 0 auto;
  margin-bottom: 50px;
  padding: 5px;
  width: 95%;
  column-count: 5;
  column-gap: 10px;
  margin-top: 30px;
}
</style>
