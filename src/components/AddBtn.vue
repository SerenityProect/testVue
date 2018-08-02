<template>
    <button type="button" class="btnAddItem"  @click="addNewItem">Add item</button>
</template>
<script>
    export default {
        name: "AddBtn",
        methods:{
            addNewItem(){
                this.$emit('additem');
            }
        }
    }
</script>

<style scoped>
    button, html [type=button] {
        -webkit-appearance: none;
        background: #fff;
        border: none;
    }
    button:focus {
        outline: none;
    }
    [type=button].btnAddItem {
        padding: 5px 10px 5px 28px;
        border-bottom: 1px solid #d3d3d3;
        width: 100%;
        text-align: left;
    }
</style>