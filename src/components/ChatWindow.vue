<script setup>
import { ref, computed } from 'vue';

const messages = ref([]);
const messageUser1 = ref('');
const messageUser2 = ref('');

const user = 'user1';

// Вычисляемое свойство для обработки ввода в зависимости от пользователя
const message = computed({
  get() {
    return user === 'user1' ? messageUser1.value : messageUser2.value;
  },
  set(value) {
    if (user === 'user1') {
      messageUser1.value = value;
    } else {
      messageUser2.value = value;
    }
  }
});

// Отправка сообщения от user1
const sendMessageFromUser1 = () => {
  if (messageUser1.value.trim()) {
    messages.value.push({ from: 'user1', text: messageUser1.value });
    messageUser1.value = '';
  }
};

// Отправка сообщения от user2
const sendMessageFromUser2 = () => {
  if (messageUser2.value.trim()) {
    messages.value.push({ from: 'user2', text: messageUser2.value });
    messageUser2.value = '';
  }
};
</script>


<template>
  <div class="chat-window">
    <h3>{{ user }}</h3>
    <div class="message-feed">
      <div v-for="message in messages" :key="message.text" class="message" :class="message.from">
        <p>{{ message.text }}</p>
      </div>
    </div>
    <div class="input-area">
      <input v-model="message" placeholder="Введите сообщение" />
      <button @click="user === 'user1' ? sendMessageFromUser1() : sendMessageFromUser2()">Отправить</button>
    </div>
  </div>
</template>

<style>
.chat-window {
  border: 1px solid #ccc;
  padding: 10px;
  width: 300px;
  height: 400px;
  overflow-y: auto;
}

.message-feed {
  height: 300px;
  overflow-y: auto;
}

.message {
  margin-bottom: 10px;
  padding: 5px;
  border-radius: 5px;
}

.user1 {
  background-color: lightblue;
  text-align: left;
}

.user2 {
  background-color: lightgreen;
  text-align: right;
}

.input-area {
  display: flex;
  justify-content: space-between;
}
</style>