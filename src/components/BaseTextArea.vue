<template>
    <textarea class="form-control"  :value="value" rows="2"  v-on="listeners"></textarea>
</template>

<script>
    export default {
        name: "BaseInput",
        props:{
            index:Number,
            value: {
                type: String,
                default: '',
            }
        },
        data(){
            return{
                readonly: true,
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
    .form-control{
        line-height: initial;
        box-shadow:none;
    }
    .form-control:focus {
        border-color: rgba(0,229,145,1);
        outline: 0;
        box-shadow:none;
    }
</style>