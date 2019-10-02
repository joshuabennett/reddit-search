<template>
    <div class="container box is-primary">
        <div class="post-title">Reddit Post Title</div>
        <hr>
        <div class="post-content">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Nobis inventore magni aspernatur natus expedita culpa qui, exercitationem doloremque nemo optio asperiores sapiente consectetur sunt commodi in delectus velit alias praesentium!</div>
    </div>
</template>

<script>
export default {

}
</script>

<style>
.container {
    min-height: 20vh;
    width: 90vw;
    border: 1px dotted black;
    box-shadow: 0px 4px 8px gray;
}
hr {
    margin: 0;
    padding: 0;
    background-color: black;
    border: none;
    height: 1px;
    margin-top: 10px;
    margin-bottom: 10px;
}
.post-title {
    font-weight: bold;
    font-size: 18px;
}
</style>
