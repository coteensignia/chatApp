<script>
import axios from 'axios'
import ChatBoard from '@/components/ChatBoard.vue'
import UserCard from '@/components/UserCard.vue'

export default {
  name: 'ChatApp',
  components: {
    ChatBoard,
    UserCard
  },
  data() {
    return {
      userLeft: {},
      userRight: {},
      messages: []
    }
  },
  async created() {
    try {
      const url = 'https://randomuser.me/api/?results=2'
      const { data } = await axios.get(url)

      this.userLeft = { ...data.results[0], side: 'left' }
      this.userRight = { ...data.results[1], side: 'right' }
    } catch (error) {
      console.error(error)
    }
  },
  methods: {
    enviarMensaje(message, color, name, side) {
      this.messages.push({ message, color, name, side })
    }
  }
}
</script>
<template>
  <h1 style="text-align: center; color: #28a745;">Chat App</h1>

  <div class="chat-app-container container">
    <div class="row">
      <UserCard
        :user="userLeft"
        @enviar-mensaje="enviarMensaje"
        class="col-4"
        v-if="Object.keys(userLeft).length > 0"
      />
      <ChatBoard class="chat col-4" :messages="messages" />
      <UserCard
        :user="userRight"
        class="col-4"
        @enviar-mensaje="enviarMensaje"
        v-if="Object.keys(userRight).length > 0"
      />
    </div>
  </div>
</template>
<style scoped>
.chat-app-container {
  background-color: #f0f4f8;
  padding: 20px;
  border-radius: 10px;
  display: flex;
  justify-content: center; 
  align-items: center; 
  text-align: center;
  margin-top:50px;
  max-width: 950px;
}



.chat{
  background-color: white;
  width: 300px;
  overflow: auto;
  max-height: 570px;
  gap:30px;
  margin-top: 40px;
  border:solid 1px #71b2f3;
  border-radius: 10px;
  
}

.row {
  display: flex;
  justify-content: center;
}
</style>

