<template>
    <div class="container box is-primary">
        <div class="post-title">Reddit Post Title</div>
        <hr>
        <div class="post-content">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Nobis inventore magni aspernatur natus expedita culpa qui, exercitationem doloremque nemo optio asperiores sapiente consectetur sunt commodi in delectus velit alias praesentium!</div>
        <hr>
        <div class="comment-container">
            <div class="upvotes">100</div>
            <div class="post-top-comment">Lorem ipsum dolor sit amet consectetur adipisicing elit. Suscipit aut unde blanditiis laudantium ullam facere, nulla reiciendis. Voluptatem recusandae facere consequuntur? Ad facilis iure doloribus in minima eius sit magni!</div>
        </div>
        <div class="comment-container">
            <div class="upvotes">100</div>
            <div class="post-top-comment">Lorem ipsum dolor sit amet consectetur adipisicing elit. Suscipit aut unde blanditiis laudantium ullam facere, nulla reiciendis. Voluptatem recusandae facere consequuntur? Ad facilis iure doloribus in minima eius sit magni!</div>
        </div>
    
        <nav class="breadcrumb is-right" aria-label="breadcrumbs">
        <ul>
            <li><a href="#">Expand Comments</a></li>
            <li class="is-active"><a href="#" aria-current="page">View Thread</a></li>
        </ul>
        </nav>
    </div>
</template>

<script>
export default {

}
</script>

<style>
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
    font-size: 18px;
}
.post-top-comment {
    padding: 1em;
    background-color: rgba(211, 211, 211, 0.507);

}
</style>
