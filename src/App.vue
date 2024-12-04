<template>
  <div class="app">
    <div class="user" v-if="user1">
      <img :src="user1.picture" alt="User 1" />
      <p>{{ user1.name }}</p>
      <message-form 
        :user="user1" 
        @sendMessage="addMessage"
      />
    </div>
    <ChatComponent :messages="messages" />
    <div class="user" v-if="user2">
      <img :src="user2.picture" alt="User 2" />
      <p>{{ user2.name }}</p>
      <message-form 
        :user="user2" 
        @sendMessage="addMessage"
      />
    </div>
  </div>
</template>

<script>
import ChatComponent from "./components/ChatComponent.vue";
import MessageForm from "./components/MessageForm.vue";

export default {
  components: {
    ChatComponent,
    MessageForm,
  },
  data() {
    return {
      user1: null,
      user2: null,
      messages: [],
    };
  },
  async created() {
    const res1 = await fetch("https://randomuser.me/api/");
    const res2 = await fetch("https://randomuser.me/api/");
    const data1 = await res1.json();
    const data2 = await res2.json();

    this.user1 = {
      name: `${data1.results[0].name.first} ${data1.results[0].name.last}`,
      picture: data1.results[0].picture.medium,
    };
    this.user2 = {
      name: `${data2.results[0].name.first} ${data2.results[0].name.last}`,
      picture: data2.results[0].picture.medium,
    };
  },
  methods: {
    addMessage(message) {
      this.messages.push(message);
    },
  },
};
</script>

<style>
.app {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}
.user {
  width: 25%;
  text-align: center;
}
</style>
