
<template>
  <div class='home'>
    <div class="title is-size-3 has-text-centered">Reddit Search</div>
    <div class="field searchbar has-addons">
      <div class="control is-expanded">
        <input class="input" type="text" placeholder="Search Reddit" v-model='searchText' @keyup.enter='searchViaGoogle'>
      </div>
      <div class="control">
        <a class="button" @click='searchViaGoogle'>
          Search
        </a>
      </div>
    </div>
    <div class="cur-search container box" v-if='finalText'><p><span style='font-weight: bold;'>Current Search: </span><i>{{finalText}}</i></p></div>
    <transition-group name='fade'>
      <search-result v-if='submitted' v-for='(link, index) in redditLinks' :searchText='link' :link='fullUrls[index]' :key='index'></search-result>
    </transition-group>
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
      finalText: '',
      submitted: false,
      redditLinks: [],
      fullUrls: []
    }
  },
  components: {
    'search-result': searchResult
  },
  methods: {
    searchViaGoogle() {
        if (this.submitted) {
          this.submitted = false;
        }
        for (let i = 0; i < this.searchText.length; i++ ) {
          if(this.searchText[i] == ' ') {
            this.searchText[i] == '+';
          }
        }
        this.finalText = this.searchText;
        this.searchText += '+reddit';
        var links = fetch(`https://www.googleapis.com/customsearch/v1?q=${this.searchText}&cx=017754768390139241406%3Aed9z5ovbxg1&num=5&key=AIzaSyDQKt9pelyhU5L24ijX2pL3WLIbk1HwCrs`)
            .then( response => response.json().then( data => {
                var urls = [];
                this.fullUrls = [];
                for(let i = 0; i < data.items.length; i++) {
                    let container = data.items[i].link;
                    //this.fullUrls[i] = container;
                    if (container.indexOf('comments') >= 0) {
                      urls.push(container.slice(container.indexOf('comments') + 9, container.indexOf('comments') + 15));
                      this.fullUrls.push(container);
                    }
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
.cur-search {
  padding: 0.6em;
  background: transparent;
  box-shadow: none;
  margin-bottom: 0px;
}
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
.fade-leave-active, .fade-enter-active{
  transition: all 1s ease;
}
.fade-enter, .fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
</style>
