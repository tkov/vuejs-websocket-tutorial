<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <button v-on:click="sendMessage('Hello World!')">Send Message</button>
</template>

<script>

export default {
  name: 'App',

  data: function() {
    return {
      connection: null
    }
  },
  methods: {
    sendMessage: function(message) {
      console.log(this.connection);
      this.connection.send(message);
    }
  },
  created: function() {
    console.log("Starting Connection to Web Server")
    this.connection = new WebSocket("wss://echo.websocket.org")
  
    // callback function event handler for WebSocket.open
    // (when a connection is opened...)
    this.connection.onopen = function(event) {
      console.log(event)
      console.log("Successfully connected to the echo WebSocket Server")
    }
    // callback function event handler for WebSocket.message 
    // (when a message is received from the server...)
    this.connection.onmessage = function(event) {
      console.log(event)
    }
  },

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
