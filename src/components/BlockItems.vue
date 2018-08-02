<template>
    <div class="content">
        <div class="block_items">
            <keep-alive>
                <app-header :title="titleHeader" ></app-header>
            </keep-alive>
            <div v-if="items.length">
                <app-item v-for="(item,  index) in items"
                          :item="item"
                          :index="index"
                          :key="index"
                          @removeItem="removeFromList(index)"
                ></app-item>
            </div>
            <div v-else>
                <p >Nothing left in the list. Add a new item in the input above.</p>
            </div>
            <app-btn @additem="editItem"></app-btn>
        </div>
        <div class="block_details" v-for="(item,  index) in items" :key="index">
            <keep-alive>
                <app-header :title="items[index].name+' details'" ></app-header>
            </keep-alive>
            {{item.details}}

            <div class="form-group" v-for="(detail, key, i) in item.details" :key="i">
                <label :for="'form'+(key)+'Input'">{{key}}</label>
                <template v-if="key=='description'">
                    <textarea class="form-control" :value="detail" :id="'form'+(key)+'Input'"  rows="2"></textarea>
                </template>
                <template v-else>
                    <input type="text" class="form-control" :value="detail" :id="'form'+(key)+'Input'"  >
                </template>
            </div>
        </div>
    </div>
</template>

<script>
    const url = 'data.json';
    import axios from 'axios';

    import AppHeader from './Header.vue';
    import AppItem from './Item.vue';
    import AppBtn from './AddBtn.vue';
    import AppItemDetails from './ItemDetails';
    export default {
        name: "Blockitems",
        data() {
            return{
                items: {},
                titleHeader:'ShoppingList',
                showId: 0,
            }
        },
        components: {
            AppHeader,
            AppItem,
            AppBtn,
            AppItemDetails,
        },
        created() {
            this.fetchData();
        },
        mounted(){
            this.$on('removeItem', this.removeFromList);
        },
        methods:{
            fetchData() {
                axios.get(url)
                    .then(response => {
                        this.items = response.data;
                    })
                    .catch(e => {
                        this.errors.push(e);
                    })
                ;
            },
            editItem(){
                this.items.push({
                    name:'',
                    details:{quantity:'',price:'',description:''}
                });
            },
            removeFromList(index){
                this.items.splice(index,1);
            },
        },
    }
</script>

<style scoped>
    .block_items{
        width: 100%;
        max-width: 300px;
    }
    .block_items p{
        padding: 5px 10px;
        border-bottom: 1px solid #d3d3d3;
        margin-bottom: 0;
    }
</style>