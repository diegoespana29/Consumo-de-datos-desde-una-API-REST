<template>
    <div class="chat">
      <div 
        class="message" 
        v-for="(msg, index) in messages" 
        :key="index" 
        :style="{ backgroundColor: msg.color }"
      >
        <strong>{{ msg.user }}</strong>: {{ msg.text }}
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ["messages"],
  };
  </script>
  
  <style>
  .chat {
    width: 50%;
    background-color: #f0f0f0;
    padding: 10px;
    border-radius: 5px;
    height: 400px;
    overflow-y: auto;
  }
  .message {
    margin-bottom: 10px;
    padding: 5px;
    border-radius: 5px;
    color: white;
  }
  </style>
  