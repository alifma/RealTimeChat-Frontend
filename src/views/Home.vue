<template>
<div class="container pt-5">
  <div class="card">
    <div class="card-header text-center">
      <h1>Aplikasi Chatting</h1>
    </div>
    <div class="card-body">
      <p v-for="(item, index) in content " :key="index"> <b>{{item.username}}:</b> {{item.text}}</p>
    </div>
    <div class="card-footer">
        <form action="" @submit.prevent="setPesan()" class="form-inline text-center">
          <div class="text-center w-100">
            <h5>Logged in as {{username}}</h5>
            <input v-model="text" type="text" class="form-control mr-2" placeholder="Write Something">
            <button class="btn btn-warning font-weight-bold">Send</button>
          </div>
        </form>
    </div>
  </div>
</div>
</template>

<script>
// @ is an alias to /src
import io from 'socket.io-client'
export default {
  name: 'Home',
  data () {
    return {
      socket: io('http://localhost:4000'),
      text: '',
      username: this.$route.query.username,
      content: []
    }
  },
  methods: {
    test () {
      this.socket.emit('test', 'hello World')
    },
    setPesan () {
      const data = {
        text: this.text,
        username: this.username
      }
      this.socket.emit('pesan', data)
      this.text = ''
    },
    getPesan () {
      this.socket.on('response-pesan', (data) => {
        console.log(data)
        this.content = [...this.content, data]
      })
    }
  },
  mounted () {
    this.test()
    this.getPesan()
  }
}
</script>
