<template>
    <input class="form-control" type="text"  :value="value" :index="index"  v-on="listeners">
</template>

<script>
    export default {
        name: "BaseInput",
        props:{
            index:Number,
            value: {
                type: String,
                default: '',
                readonly: Boolean,
            }
        },
        computed: {
            listeners () {
                return {
                    ...this.$listeners,
                    input: event => this.$emit('input', event.target.value)
                }
            }
        },
    }
</script>

<style scoped>
    [readonly] {
        color: #999;
    }
    .block_items .form-control {
        background-color: transparent;
        opacity: 1;
        border: none;
        width: calc(100% - 34px);
        display: inline-block;
        padding: 0 0 0 5px;
    }
    .block_items .form-control:focus{
        border: none;
    }
    .form-control{
        line-height: initial;
        box-shadow:none;
    }
    .form-control:focus {
        border-color: rgba(0,229,145,1);
        outline: 0;
        box-shadow:none;
    }
    [type="checkbox"]:checked + input{text-decoration: line-through;}
</style>