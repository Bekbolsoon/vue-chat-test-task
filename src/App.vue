<script setup>
import { ref } from 'vue';

// Лента общих сообщений для обоих пользователей
const messages = ref([]);

// Сообщения пользователей
const messageUser1 = ref('');
const messageUser2 = ref('');

// Отправка сообщения от user1
const sendMessageFromUser1 = () => {
  if (messageUser1.value.trim()) {
    messages.value.push({ from: 'user1', text: messageUser1.value });
    messageUser1.value = ''; // Очищаем поле ввода
  }
};

// Отправка сообщения от user2
const sendMessageFromUser2 = () => {
  if (messageUser2.value.trim()) {
    messages.value.push({ from: 'user2', text: messageUser2.value });
    messageUser2.value = ''; // Очищаем поле ввода
  }
};
</script>

<template>
  <div class="chat-container">
    <!-- Окно чата для user1 -->
    <div class="chat-window">
      <h3>Chat User 1</h3>
      <div class="message-feed">
        <div v-for="message in messages" :key="message.text" class="message" :class="{ 
          'me': message.from === 'user1',
          'companion': message.from === 'user2' }">
          <p>{{ message.from === 'user1' ? 'You: ' : 'User2: ' }} {{ message.text }}</p>
        </div>
      </div>
      <div class="input-area">
        <input v-model="messageUser1" class="form-control" placeholder="Enter a message" />
        <button class="btn btn-primary" @click="sendMessageFromUser1">Send</button>
      </div>
    </div>

    <!-- Окно чата для user2 -->
    <div class="chat-window">
      <h3>Chat User 2</h3>
      <div class="message-feed">
        <div v-for="message in messages" :key="message.text" class="message" :class="{ 
          'me': message.from === 'user2',
          'companion': message.from === 'user1' }">
          <p>{{ message.from === 'user2' ? 'You: ' : 'User1: ' }} {{ message.text }}</p>
        </div>
      </div>
      <div class="input-area">
        <input v-model="messageUser2" class="form-control" placeholder="Enter a message" />
        <butto class="btn btn-primary" @click="sendMessageFromUser2">Send</butto>
      </div>
    </div>
  </div>
</template>

<style>
.chat-container {
  display: flex;
  gap: 20px;
}

.chat-window {
  border: 1px solid white;
  border-radius: 10px;
  padding: 10px;
  height: 400px;
  overflow-y: auto;
  width: calc(50% - 10px);
}

@media (max-width: 768px) {
  .chat-container {
    flex-direction: column;
  }

  .chat-window {
    width: 100%;
  }
}

.message-feed {
  height: 300px;
  overflow-y: auto;
}

.message {
  margin-bottom: 10px;
  padding: 5px;
  border-radius: 5px;
  color: #000;
  width: 50%;
}
.message.me {
  background-color: lightblue;
  text-align: right;
  margin-left: auto;
}
.message.companion {
  background-color: lightgreen;
  text-align: left;
  margin-right: auto;
}

.input-area {
  display: flex;
  justify-content: space-between;
}
</style>
