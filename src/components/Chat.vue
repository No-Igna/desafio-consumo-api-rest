<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-md-3 border">
        <RandomUser userName="Usuario_1" @message-sent="handleMessage" @color-changed="updateUserColor('Usuario_1', $event)" />
      </div>
      <div class="col-md-6 border chat">
        <div v-for="(msg, index) in messages" :key="index" :class="getUserClass(msg.sender)"
          :style="{ backgroundColor: colorUser[msg.sender] }">
          <strong>{{ msg.user }}:</strong> {{ msg.content }}
        </div>
      </div>
      <div class="col-md-3 border">
        <RandomUser userName="Usuario_2" @message-sent="handleMessage" @color-changed="updateUserColor('Usuario_2', $event)" />
      </div>
    </div>
  </div>
</template>

<script>
import RandomUser from './RandomUser.vue';

export default {
  name: 'Chat',
  components: {
    RandomUser,
  },
  data() {
    return {
      messages: [],
      colorUser: {
        usuario_1:'',
        usuario_2:''
      }
    };
  },
  methods: {
    handleMessage(message) {
      this.messages.push(message)
      console.log(this.colorUser);
      
    },
    getUserClass(sender) {
      return sender === "Usuario_1" ? "user1-message" : "user2-message";
    },
    updateUserColor(userId, color) {
      this.colorUser[userId] = color;
    }
  }
};
</script>

<style scoped>
.chat{
  background-color: #f0f0f0;
  border-radius: 5px;
}
.user1-message {
  
  color: #333;
  padding: 8px;
  border-radius: 5px;
  margin: 5px 0;
  text-align: left;
  overflow: auto;      /* Agrega scroll si el contenido se desborda */
  word-wrap: break-word;
}

.user2-message {
  color: #333;
  padding: 8px;
  border-radius: 5px;
  margin: 5px 0;
  text-align: right;
  overflow: auto;      /* Agrega scroll si el contenido se desborda */
  word-wrap: break-word;
}
</style>