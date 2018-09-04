<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/384ba7ef0c7f5c8b83121cecd8f26809.jpg">
    <h1>Be nice to the duck</h1>
    ><input v-model="message.text" @keyup.enter="submit">
    <p>{{duck_reply}}</p>
  </div>
</template>

<script>
const axios = require('axios')
const qs = require('qs')
export default {
  name: 'Game',
  data () {
    return {
      message: {
        text: this.message,
        language: 'english'
      },
      response: null,
      duck_reply: ''
    }
  },
  methods: {
    submit () {
      this.duck_reply = ''
      const options = {
        headers: {
          'X-Mashape-Key': 'GtzH0B8PzkmshTizmQTqGadyOUHHp1euquSjsn7gAZY47UCfLi',
          'Content-Type': 'application/x-www-form-urlencoded',
          'Accept': 'application/json'
        }
      }
      axios.post('https://japerk-text-processing.p.mashape.com/sentiment/', qs.stringify(this.message), options).then(r => {
        this.response = r.data.label
      })
    }
  },
  watch: {
    'response': function (newVal) {
      this.duck_reply = ''
      if (newVal === 'pos') {
        this.duck_reply = 'You are being nice to the duck and he is happy'
      }
      if (newVal === 'neg') {
        this.duck_reply = 'That wasn\'t very nice'
      }
      if (newVal === 'neutral') {
        this.duck_reply = 'You said something to the duck. He\'s unsure how to take it'
      }
    }
  }
}
</script>
