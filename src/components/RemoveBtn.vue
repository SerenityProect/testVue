<template>
    <button type="button"  class="close" aria-label="Close" :index="index" @click="clickRemoveItem"><span aria-hidden="true" >&times;</span></button>
</template>

<script>
    export default {
        name: "RemoveBtn",
        model: {
            prop: 'checked',
            event: 'click'
        },
        props:{
            index:Number,
            id:null,
        },
        methods:{
            clickRemoveItem: function(e) {
                this.$parent.$emit('removeItem', e.currentTarget.index);
            }
        },
    }
</script>

<style scoped>
    .close{
        color: #ff0000;
    }
    .close:hover, .close:focus{
        color:#dc3545;
    }


</style>