<template>
    <div class="form-check" :id="'item-'+id">
        <app-base-checkbox :index="index" v-model="checkItem" @change="checkBoxItem(index)" ></app-base-checkbox>
        <app-base-input  :value="item.name" :readonly="readonlyItem"  :index="index"  v-model.trim="item.name" @click="clickEditItem(index)" ></app-base-input>
        <app-remove-btn :index="id"  v-if="showBtn"></app-remove-btn>
    </div>
</template>

<script>
    import AppBaseCheckbox from './BaseCheckbox';
    import AppBaseInput from './BaseInput';
    import AppRemoveBtn from './RemoveBtn';
    export default {
        name: "Item",
        props:{
            index: Number,
            id: Number,
            item: Object,
            readonly: Boolean,
        },
        data() {
            return{
                checkItem:false,
            }
        },
        components: {
            AppBaseCheckbox,
            AppBaseInput,
            AppRemoveBtn,
        },
        computed:{
            showBtn(){
                return  this.checkItem || !this.readonly;
            },
            readonlyItem(){
                return   this.readonly || this.checkItem? true: false;
            }
        },
        methods:{
            clickEditItem(i) {
                this.checkItem=false;
                this.$emit('editItem', i);
            },
            checkBoxItem(i){
                this.$emit('changeBox',i, this.checkItem);
            }

        }
    }
</script>

<style scoped>
    .form-check{
        padding: 5px 10px;
        border-bottom: 1px solid #d3d3d3;
    }
    button, html [type=button] {
        -webkit-appearance: none;
        background: #fff;
        border: none;
    }
    button:focus {
        outline: none;
    }
</style>