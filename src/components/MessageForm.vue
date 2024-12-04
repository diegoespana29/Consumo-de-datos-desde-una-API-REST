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
    <!-- Aquí se utiliza ChatComponent correctamente -->
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
  export default {
    props: ["user"],
    data() {
      return {
        text: "",
        color: "#007bff",
      };
    },
    methods: {
      sendMessage() {
        if (this.text.trim() === "") return;
        this.$emit("sendMessage", {
          user: this.user.name,
          text: this.text,
          color: this.color,
        });
        this.text = "";
      },
    },
  };
  </script>
  
  <style>
  .message-form {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  textarea {
    width: 100%;
    height: 80px;
  }
  button {
    align-self: center;
    background-color: #007bff;
    color: white;
    padding: 5px 10px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  </style>
  