<template>
    <div class="title" :id="id">{{title}}</div>
</template>

<script>
    export default {
        name: "Header",
        props: {
            title: String,
            id: String,
        }
    }
</script>

<style scoped>
    .title{
        width: 100%;
        font-size: 1.2em;
        line-height: 0.6em;
        padding: 15px;
        text-transform: uppercase;
        color:#fff;
        border-bottom: 1px solid #d3d3d3;
        background: rgb(0,229,145);
        background: -moz-linear-gradient(left, rgba(0,229,145,1) 1%, rgba(47,239,188,1) 100%);
        background: -webkit-linear-gradient(left, rgba(0,229,145,1) 1%,rgba(47,239,188,1) 100%);
        background: linear-gradient(to right, rgba(0,229,145,1) 1%,rgba(47,239,188,1) 100%);
        filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#00e591', endColorstr='#2fefbc',GradientType=1 );
    }
    #header.title{
        font-size: 2em;
        line-height: 1em;
        text-transform: initial;
        border: none;
    }
</style>