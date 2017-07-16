<template>
  <div>
    <header>
      <mu-appbar title="garage">
      </mu-appbar>
    </header>
    <section v-for="article in articleList" :key="article.id">
      <h1>{{article.title.rendered}}</h1>
      <article v-html="article.content.rendered"></article>
    </section>
  </div>
</template>

<script>
import logo from 'assets/img/logo.png'
export default {
  data () {
    return {
      msg: 'Use Vue 2.0 Today!',
      logoImg: logo,
      articleList: [{
        title: {
          rendered: ''
        },
        content: {
          rendered: ''
        }
      }]
    }
  },

  methods: {
    startHacking () {
      this.$notify({
        title: 'It Works',
        message: 'We have laid the groundwork for you. Now it\'s your time to build something epic!',
        duration: 6000
      })
    }
  },
  mounted:function(){
    let _this = this
    fetch('http://www.garage.net.cn/blog//wp-json/wp/v2/posts', {method: 'get'})
      .then(function(response){
        console.log(response)
        if(response.status >= 400){
          throw new Error('Bad Network!')
        }
        return response.json()
      })
      .then(function(response){
        _this.articleList = response
        console.log(response)
      })
  }
}
</script>

<style lang="postcss" scope>
  body {
    background-color: #f5f5f5;
  }
  :root h1 {
   --color: red;
   display: flex;
   color: var(--color);
  }

</style>
