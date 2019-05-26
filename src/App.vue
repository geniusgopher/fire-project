<template>
  <div id="app">
    <div class="wrap">
      <div class="container">
        <fire-component v-for="fire in flames" :fireObj="fire" :key="fire.id"/>
      </div>
      <p v-show="errorMessage" class="error">{{ errorMessage }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import FireComponent from "./components/FireComponent.vue";
import mock from './mock.json'

export default {
  name: "app",
  components: {
    FireComponent
  },
  data() {
    return {
      flames: [],
      errorMessage: '',
      url: ''
    };
  },
  async beforeMount() {
    try {
      if (this.url) {
        const { data } = await axios.get(this.url);
        this.flames = data;
      } else {
        this.flames = mock;
      }
    } catch (error) {
      switch(error.response.status) {
        case 404:
          this.errorMessage = 'Данные не найдены'
          break;
        case 500:
          this.errorMessage = 'Серверная ошибка'
          break;
        default :
          this.errorMessage = error.message
          break;
      }
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.wrap {
  max-width: calc(1200px - 40px);
  margin: 0 auto;
}
.container {
  display: flex;
  flex-wrap: wrap;
}
.error {
  color: red;
  text-align: center;
}
</style>
