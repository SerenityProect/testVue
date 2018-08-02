<template>
    <div class="container" role="main">
        <div class="content">
            <div class="block_items">
                <keep-alive>
                    <app-header :title="titleHeader" ></app-header>
                </keep-alive>
                <div v-if="items.length">
                    <app-item v-for="(item,  index) in items"
                              :item="item"
                              :index="index"
                              :id="item.id"
                              :key="item.id"
                              :readonly="!showItem[index]"
                              @removeItem="removeFromList(index)"
                              @editItem="editItem(index)"
                              @changeBox="changeBox"
                    ></app-item>
                </div>
                <div v-else>
                    <p >Nothing left in the list. Add a new item in the input above.</p>
                </div>
                <app-btn @additem="addNewItem"></app-btn>
            </div>
            <div class="block_details" :id="'item-'+showInd" v-if="showDetailsItem">
                <keep-alive>
                    <app-header  :title="titleItem" ></app-header>
                </keep-alive>
                <app-item-details :index="showInd" :id="items[showInd].id" :details="items[showInd].details"></app-item-details>
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
        name: "Content",
        data() {
            return{
                items: {},
                titleHeader:'ShoppingList',
                showInd: 0,
                showItem:[],
                newItem:false,
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
            this.showItem = new Array(this.items.length).fill(false);
        },
        mounted(){
            this.$on('removeItem', this.removeFromList);
            this.$on('check', this.editItem);
        },
        computed:{
            titleItem(){
                return this.items[this.showInd].name + ' details'
            },
            showDetailsItem(){
                return this.showItem[this.showInd] || this.newItem;
            }
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
            addNewItem(){
                this.showInd = this.items.length;
                this.newItem = true;
                   this.items.push({
                       id: Math.max.apply(Math, this.items.map(function (o) {
                           return o.id;
                       })) + 1,
                       name: '',
                       details: {quantity: '', price: '', description: ''}
                   });
            },
            editItem(i){
                this.newItem = false;
                const show=this.showItem[i];
                this.showItem = new Array(this.items.length).fill(false);
                this.showInd=i;
                this.showItem[this.showInd] = !show;
            },
            changeBox(i,s){
                this.newItem = false;
                this.showItem = new Array(this.items.length).fill(false);
            },
            removeFromList(index){
                this.showItem=false;
                this.showInd=0;
                this.items.splice(index,1);
            },
        },
    }
</script>

<style scoped>
    .container{
        margin: 120px auto 20px;
        display: -webkit-flex;
        display: flex;
        -webkit-justify-content: center;
        justify-content: center;
    }
    .content{
        width: 100%;
        max-width: 800px;
        display: -webkit-flex;
        display: flex;
        -webkit-align-items: flex-start;
        align-items: flex-start;
        -webkit-justify-content: space-between;
        justify-content: space-between;
        -webkit-flex-wrap: wrap;
        flex-wrap: wrap;
    }
    .content>div{
        border:1px solid #d3d3d3;
        min-height: 330px;
    }
    .block_details{
        width: 100%;
        max-width: calc(100% - 320px);
    }
    .block_items{
        width: 100%;
        max-width: 300px;
    }
    .block_items p{
        padding: 5px 10px;
        border-bottom: 1px solid #d3d3d3;
        margin-bottom: 0;
    }

    @media only screen  and (max-width:800px) {
        .container {
            margin-top: 20px;
        }

        .content {
            margin: auto;
            width: 300px;
        }

        .content > div {
            min-width: 300px;
            margin: 0 auto 20px;
            min-height: 30px;
            height: auto;
        }

    }
</style>