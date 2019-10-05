
<template>
  <div class='home'>
    <div class="title is-size-3 has-text-centered">Reddit Search</div>
    <div class="field searchbar has-addons">
      <div class="control is-expanded">
        <input class="input" type="text" placeholder="Search Reddit" v-model='searchText'>
      </div>
      <div class="control">
        <a class="button" @click='searchViaGoogle'>
          Search
        </a>
      </div>
    </div>
    <p> {{redditLinks}} </p>
    <search-result v-if='submitted' v-for='link in redditLinks' :searchText='link'></search-result>
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
      msg: 'Welcome to Your Vue.js App',
      searchText: '',
      submitted: false,
      redditLinks: []
    }
  },
  components: {
    'search-result': searchResult
  },
  methods: {
    searchViaGoogle() {
        for (let i = 0; i < this.searchText.length; i++ ) {
          if(this.searchText[i] == ' ') {
            this.searchText[i] == '+';
          }
        }
        this.searchText += '+reddit';
        var links = fetch(`https://www.googleapis.com/customsearch/v1?q=${this.searchText}&cx=017754768390139241406%3Aed9z5ovbxg1&num=5&key=AIzaSyDQKt9pelyhU5L24ijX2pL3WLIbk1HwCrs`)
            .then( response => response.json().then( data => {
                var urls = [];
                for(let i = 0; i < data.items.length; i++) {
                    let container = data.items[i].link;
                    urls[i] = container.slice(container.indexOf('comments') + 9, container.indexOf('comments') + 15);
                }
                this.redditLinks = urls;
                this.submitted = true;
                return urls;
            }))
            .catch(function(err) {
                console.log('Fetch Error :-S', err);
            });
          this.searchText='';
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.searchbar {
  width: 600px;
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
