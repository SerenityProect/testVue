<template>
    <div class="item-detail">
        <div v-for="(item, key, i) of details" :id="newId">
            <label :for="'form'+(key)+'Input'">{{key}}</label>
            <app-base-text-area v-if="key=='description'" class="form-control" :value="details[key]"  v-model.trim="details[key]" :id="'form'+(key)+'Input'"  rows="2"></app-base-text-area>
            <app-base-input v-else :value="details[key]" :index="index" :readonly="readonly"  v-model.trim="details[key]"></app-base-input>
        </div>
    </div>
</template>

<script>
    import AppBaseInput from './BaseInput';
    import AppBaseTextArea from './BaseTextArea';
    export default {
        name: "ItemDetails",
        props:{
            index: Number,
            id:Number,
            details:Object,
        },
        data() {
            return{
                readonly:false,
            }
        },
        components: {
            AppBaseInput,
            AppBaseTextArea
        },
        computed:{
            newId(){
                return  'details-'+this.id;
            }
        },
    }
</script>

<style scoped>
    .item-detail{
        padding:5px 10px;
    }
</style>