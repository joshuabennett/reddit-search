/* eslint-disable */
<template>
    <div class="container box is-primary">
        <div class="post-title">{{title}}</div>
        <div class="post-content">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Nobis inventore magni aspernatur natus expedita culpa qui, exercitationem doloremque nemo optio asperiores sapiente consectetur sunt commodi in delectus velit alias praesentium!</div>
        <div class="comment-container">
            <div class="upvotes has-text-centered">100</div>
            <div class="post-top-comment">Lorem ipsum dolor sit amet consectetur adipisicing elit. Suscipit aut unde blanditiis laudantium ullam facere, nulla reiciendis. Voluptatem recusandae facere consequuntur? Ad facilis iure doloribus in minima eius sit magni!</div>
        </div>
        <div class="comment-container" v-if='isExpanded' v-for='comment in moreComments'>
            <div class="upvotes has-text-centered">{{comment.upvotes}}</div>
            <div class="post-top-comment">{{comment.content}}</div>
        </div>
        <nav class="breadcrumb is-right" aria-label="breadcrumbs">
        <ul>
            <li><a @click='isExpanded = !isExpanded'>Expand Comments</a></li>
            <li ><a aria-current="page">View Thread</a></li>
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
            isExpanded: false,
            title: '',
            postContent: '',
            topComment: 'This is the top comment.',
            moreComments: []
        }
    },
    props: ['searchText'],
    methods: {},
            //     console.log(data);
            // });
            // r.getSubmission('4j8p6d').expandReplies({limit: 1, depth: 1}).then(data => {
            //     console.log(data);
            // });
    created() {
            console.log(this.title);
            //console.log(r.getSubmission(this.searchText));
            r.getSubmission(this.searchText).title.then(data => {
                this.title = data;
            });
            //   
            r.getSubmission(this.searchText).expandReplies({limit: 1, depth: 1}).then(data => {
                console.log(data);
            });
    }
}
</script>


<style>
.post-title {
    padding: 1em;
}
.post-content {
    background-color: rgba(0, 0, 255, 0.05);
    padding: 1em;
    font-size: calc(10px + 0.3vw);
}
.comment-container {
    display: flex;
    flex-direction: row;
    margin-top: 2vh;
    justify-content: center;
    align-items: center;
}
.upvotes {
    padding: 1em;
    color: green;
    background-color: rgba(0, 128, 0, 0.096);
    margin: 1em;
    width: 65px;

}
.breadcrumb {
    margin: 1em;
}
.container {
    min-height: 20vh;
    width: 90vw;
    border: 1px dotted rgba(0, 0, 0, 0.151);
    box-shadow: 0px 4px 8px rgba(128, 128, 128, 0.589);
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
</style>
