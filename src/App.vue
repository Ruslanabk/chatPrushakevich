<template>
  <div id="app">
    <input type="text" placeholder="Автор" v-model="author">
    <textarea placeholder="Сообщение" v-model="text"></textarea>
    <button v-on:click="sendMessage()">Отправить</button>
    <hr>
    <br><br>

    <div v-for="(item, i) in messages" :key="i">
      <strong>{{item.name}}</strong>
      <p>{{item.text}}</p>
      <hr>
    </div>

  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      messages: [],
      author: '',
      text: ''
    }
  },
  methods: {
    getMessages(){
      this.axios({
        method: "GET",
        url: "http://37.77.104.246/api/jsonstorage/?id=db97868f606182092b61089701130650"
      }).then( response => {
        this.messages = response.data;
      } )
    },
    sendMessage(){
      this.getMessages();
      let newMessage = {
        name: this.author,
        text: this.text
      }
      this.messages.push(newMessage);
      this.axios({
        method: "PUT",
        url: "http://37.77.104.246/api/jsonstorage/?id=db97868f606182092b61089701130650",
        data: this.messages
      });
    }
  },
  mounted(){
    setInterval(this.getMessages, 1000);
    this.getMessages();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
