<template>
  <section class="section">
    <div class="field">
      <div class="control">
        <input class="input" type="text" v-model="msg" @keypress.enter.exact="sendMessage">
      </div>
    </div>
    <article class="media" v-for="(msg, index) in msgs" :key="index">
      <div class="media-content">
        <div class="content">
          <p>
            <strong>{{ msg.name }}</strong>
            <br>
            {{ msg.text }}
          </p>
        </div>
      </div>
    </article>
  </section>
</template>

<script>
import io from 'socket.io-client'

export default {
  data() {
    return {
      msg: '',
      msgs: [],
      socket: ''
    }
  },
  mounted() {
    this.socket = io('http://localhost:3001')
    this.socket.emit('join', this.$route.params.id)
    this.socket.on('new-msg', msg => {
      this.msgs.push(msg)
    })
  },
  methods: {
    sendMessage() {
      this.msg = this.msg.trim()
      if (this.msg) {
        const message = {
          name: this.socket.id,
          text: this.msg,
        }
        this.msgs.push(message)
        // send-msgイベントでmessageをサーバーサイドに投げる
        this.socket.emit('send-msg', message, this.$route.params.id)
        this.msg = ''
      }
    }
  }
}
</script>
