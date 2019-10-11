/* eslint-disable */
<template>
    <div class="container full-container box is-primary" >
        <!-- <a :name='firstCommentData.created'></a> -->
        <div class="post-title">{{title}}</div>
        <div class="image-container" v-if='hasImg'>
            <img class='img-thumb' :src='image'>
            <button @click="expandImg()" class="button expand-img">Expand Image</button>
        </div>
        <div class="post-content" v-html='postContent' v-if='postContent'></div>
        <div class="comment-container">
            <div class="upvotes has-text-centered">{{upvotes}}</div>
            <div class="post-top-comment" v-html='topComment'></div>
        </div>
        <div class="reply" v-for='reply in moreComments[0].replies'>
            <div class="reply-score has-text-centered" :class='getColor(reply.score)'>{{reply.score}}</div>
            <div class="reply-text">
                <p>{{reply.body}}</p>
                <p style='text-align: right; font-size: 12px;'>{{'/u/'+reply.author.name}}</p>
            </div>
        </div>
            <transition name='expand'>
                <div class="expand-wrapper" v-if='isExpanded'>
                    <div class="individual-comment" v-for='(comment,index) in moreComments' v-if='index > 0'>
                        <div class="comment-container">
                            <div class="upvotes has-text-centered">{{comment.score}}</div>
                            <div class="post-top-comment">{{comment.body}}
                                <p style='text-align: right; font-size: 12px;'>{{'/u/'+comment.author.name}}</p>
                            </div>
                        </div>
                        <div class="reply" v-for='reply in comment.replies'>
                            <div class="reply-score has-text-centered" :class='getColor(reply.score)'>{{reply.score}}</div>
                            <div class="reply-text">
                                <p>{{reply.body}}</p>
                                <p style='text-align: right; font-size: 12px;'>{{'/u/'+reply.author.name}}</p>
                            </div>
                        </div>
                    </div>
                </div>
            </transition>
        <nav class="breadcrumb is-right" aria-label="breadcrumbs">
        <ul>
            <li><a v-if='moreComments.length > 0' @click='toggleComments()' :href='backToComment()'>{{expandText}}</a></li>
            <li ><a :href='link' aria-current="page">View Thread</a></li>
        </ul>
        </nav>
    </div>
</template>

<script>
//import snoowrap from '../../node_modules/snoowrap'
var snoowrap = require('snoowrap');

const r = new snoowrap({
  userAgent: 'RedditSearch by /u/EarthsVisitor',
  clientId: 'tkeURvFf2gpnwQ',
  clientSecret: 'RugvbmBgfWtolavy1CZTqi02fJY',
  refreshToken: '370426875071-LSGyKySnbjacfzSIjWYkvk-M_Vk'
});

export default {
    data () {
        return {
            hasImg: false,
            image: '',
            isExpanded: false,
            title: '',
            postContent: '',
            firstCommentData: {},
            topComment: 'Unable to load Top Comment',
            moreComments: [],
            upvotes: '',
            expandText: 'More Comments'
        }
    },
    props: ['searchText', 'link'],
    methods: {
        getColor(score) {
            return score >= 0 ? 'upvotes' : 'downvotes';
        },
        backToComment(comment) {
            // if (!this.isExpanded) {
            //     return `#${this.firstCommentData.created}`;
            // } else {
            //     return false;
            // }
        },
        toggleComments() {
            this.isExpanded = !this.isExpanded;
            this.expandText == 'More Comments' ? 'Less Comments' : 'More Comments';
        },
        expandImg() {
            var imageClass = document.querySelector('img');
            imageClass.classList.contains('img-thumb') ? imageClass.className = 'img-full' : imageClass.className = 'img-thumb';
        }
    },
    created() {
            //console.log(r.getSubmission(this.searchText));
            r.getSubmission(this.searchText).preview.images[0].source.url.then(data => {
                if (data) {
                    this.hasImg = true;
                    this.image = data;
                }
            });
            r.getSubmission(this.searchText).title.then(data => {
                this.title = data;
            });
            r.getSubmission(this.searchText).selftext_html.then(data => {
                this.postContent = data;
            });
            r.getSubmission(this.searchText).score.then(data => {
                this.upvotes = data;
            });
            //   
            r.getSubmission(this.searchText).comments.then(data => {
                console.log(data);
                //this.firstCommentData = data[0];
                if (data) {
                    this.topComment = data[0].body_html; 
                    this.moreComments = data.slice(0, 6);
                }
            }).catch(error => {
                console.log(error);
            });
    }
}
</script>



<style>
.image-container {
    position: relative;
}
.expand-img {
    position: absolute;
    top: 0;
    left: 0;
    opacity: 0;
    transition: .5s ease;
}
.image-container:hover .expand-img {
    opacity: 1;
}

.img-full {
    max-height: 80vh;
}
.img-thumb {
    max-height: 25vh;
    max-width: 25vh;
}
.post-title {
    padding: 1em;
}
.post-content {
    background-color: rgba(182, 182, 184, 0.651);
    padding: 1em;
    font-size: calc(10px + 0.3vw);
    border-radius: 10px;
}
.comment-container {
    display: flex;
    flex-direction: row;
    margin-top: 2vh;
    justify-content: center;
    align-items: center;
    margin-bottom: 1vh;
}
.upvotes {
    padding: 1em;
    color: green;
    background-color: rgba(0, 128, 0, 0.096);
    margin: 1em;
    width: 60px;

}
.downvotes {
    padding: 1em;
    color: red;
    background-color: rgba(192, 6, 6, 0.096);
    margin: 1em;
    width: 60px;
}
.reply-score {
    width: 45px;
    padding: 0.5em;
    margin: 0.5em;
}
.breadcrumb {
    margin: 1em;
}
.full-container {
    min-height: 20vh;
    width: 90vw;
    border: 1px dotted rgba(0, 0, 0, 0.151);
    box-shadow: 0px 4px 8px rgba(128, 128, 128, 0.589);
    transition: height 1.0s linear;
}
hr {
    margin: 0;
    padding: 0;
    background-color: rgba(0, 0, 0, 0.205);
    border: none;
    height: 1px;
    margin-top: 10px;
    margin-bottom: 10px;
}
.post-title {
    font-weight: bold;
    font-size: calc(10px + 0.5vw);
}
.post-top-comment {
    padding: 1em;
    background-color: rgba(211, 211, 211, 0.507);
    font-size: calc(10px + 0.3vw);
    width: 100%;

}
.individual-comment {
    display: flex;
    flex-direction: column;
}
.reply {
    display: flex;
    flex-direction: row;
    margin-left: 12%;
    align-items: center;
}
.reply-text {
    background-color: rgba(0, 0, 255, 0.05);
    padding: 1em;
    margin: 0.3em;
    font-size: calc(10px + 0.3vw);
    width: 100%;
}
.expand-enter-active {
  transition: all .3s ease;
  max-height: 5000px;
}
.expand-leave-active {
  transition: all .3s ease;
  max-height: 5000px;
}
.expand-enter, .expand-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
  max-height: 0;
}
</style>
