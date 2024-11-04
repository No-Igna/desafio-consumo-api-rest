<template>
  <div class="container-fluid p-2">
    <img v-if="user.results && user.results[0]" :src="user.results[0].picture.large" :alt="name">
    <h3 class="mt-3"> {{ name }} </h3>
    <div class="d-flex flex-column">
      <input class="form-control form-control-color mt-3" type="color" v-model="selectedColor" @input="colorChanged">
      <textarea class="form-control mt-3" v-model="message" placeholder="Escribe tu mensaje..."></textarea>
      <button class="btn mt-3 border" @click="sendMessage">Enviar</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'RandomUser',
  props: {
    userName: String
  },
  data() {
    return {
      message: '',
      name: '',
      user: {},
      selectedColor: '#fff',
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get('https://randomuser.me/api/');
        this.user = response.data;
        this.name = this.user.results[0].name.first + ' ' + this.user.results[0].name.last;
      } catch (error) {
        console.error('vaya... algo ha pasao: ', error)
      }
    },
    sendMessage() {
      if (this.message.trim()) {
        this.$emit('message-sent', { sender: this.userName, user: this.name, content: this.message });
        this.message = '';
      }
    },
    colorChanged() {
      this.$emit('color-changed', this.selectedColor);
    }
  }
};
</script>

<style scoped>
</style>