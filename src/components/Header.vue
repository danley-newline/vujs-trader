<template>
    <div>
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
                <router-link to="/" class="navbar-brand">Stock Trader</router-link>
           
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav mr-auto">
                    <router-link to="/portfolio" class="mr-2" activeClass="active" tag="li"><a>Portfolio</a></router-link>
                    <router-link to="/stocks" activeClass="active" tag="li"><a>Stocks</a></router-link>
                </ul>
                
                <ul class="navbar-nav ml-auto">
                    <li class="ml-2"><a href="#" @click="endDay">End Day</a></li>
                        <li><a href="#" @click="saveData">Save Data</a></li>
                        <li><a href="#" @click="loadData">Load Data</a></li>
                </ul>
                <strong class="navbar-text navbar-right ml-3">Argent: {{ funds | currency}}</strong>

            </div>
        </nav>
    </div>
</template>

<script>
import {mapActions} from 'vuex';
    export default {
        data(){
            return{
               
            }
        },
        computed: {
            funds(){
                return this.$store.getters.funds;
            }
        },
        methods:{
            ...mapActions({
                randomizeStocks: 'randomizeStocks',
                fetchData: 'loadData'
            }),
            endDay(){
                this.randomizeStocks();
            },
            saveData(){
                const data = {
                    funds: this.$store.getters.funds,
                    stockPortfolio: this.$store.getters.stockPortfolio,
                    stocks: this.$store.getters.stocks
                };
                this.$http.put('data.json', data);
            },
            loadData(){
                this.fetchData();
            }
        }
    }
</script>