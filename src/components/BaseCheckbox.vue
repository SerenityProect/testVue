<template>
    <input class="form-check-input" type="checkbox" :checked="checked"   @change="$emit('change', $event.target.checked)">
</template>
<script>
    export default {
        name: "CheckInput",
        model: {
            prop: 'checked',
            event: 'change'
        },
        props:{
            index:Number,
            checked:{
                type:Boolean,
                default:false,
            }
        },
    }
</script>
<style scoped>
    [type="checkbox"] {
        position: relative;
        margin-top: .3rem;
        margin-left: 0;
    }
</style>