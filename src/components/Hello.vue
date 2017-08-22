<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="button" value="post请求" @click="post">
    <input type="button" value="get请求" @click="get">
    <input type="button" value="post/get同时请求" @click="all">
  </div>
</template>

<script>
// import axios from 'axios'

export default {
  name: 'hello',
  data () {
    return {
      msg: '学习axios'
    }
  },
  created () {},
  methods: {
    post () {
      this.$http.post('http://easy-mock.com/mock/599a9e44059b9c566dc9c62d/axios-test/post/list')
      .then((res) => {
        console.log(res)
        this.msg = res.data
      })
      .catch((res) => {
        console.log(res)
      })
    },
    get () {
      this.$http.get('http://easy-mock.com/mock/599a9e44059b9c566dc9c62d/axios-test/getList')
      .then((res) => {
        console.log(res)
        this.msg = res.data
      })
      .catch((res) => {
        console.log(res)
      })
    },
    all () {
      let nihao = this.$http
      function http1 () {
        return nihao.get('http://easy-mock.com/mock/599a9e44059b9c566dc9c62d/axios-test/getList')
      }

      function http2 () {
        return nihao.post('http://easy-mock.com/mock/599a9e44059b9c566dc9c62d/axios-test/post/list')
      }
      nihao.all([http1(), http2()]).then(nihao.spread((res1, res2) => {
        this.msg = res1.data + res2.data
      }))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
