<template>
  <div class='home'>
    <div class="title is-size-3 has-text-centered">Reddit Search</div>
    <div class="control searchbar has-icons-right">
      <input class="input is-small" type="email" placeholder="Search Reddit">
      <span class="icon is-small is-right">
        <i class="fas fa-search"></i>
      </span>
    </div>
    <search-result></search-result>
    <search-result></search-result>
    <search-result></search-result>
    <footer class="footer">
      <div class="content has-text-centered">
        <p>
          <strong>Reddit Search</strong> by <a href="https://jgthms.com">Joshua Bennett</a>. The source code is licensed
          <a href="http://opensource.org/licenses/mit-license.php">MIT</a>. The website content
          is licensed <a href="http://creativecommons.org/licenses/by-nc-sa/4.0/">CC BY NC SA 4.0</a>.
        </p>
      </div>
  </footer>
  </div>
</template>

<script>
import searchResult from './searchResult.vue'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components: {
    'search-result': searchResult
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.searchbar {
  width: calc(200px + 25vw);
  margin: 0 auto;
  margin-bottom: 2em;
}
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
.footer {
  margin-top: 10vh;
}
</style>
