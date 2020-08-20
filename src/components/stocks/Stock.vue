<template>
    <div class="col-sm-6 col-md-4 mt-4">
        <div class="card">
            <div class="card-header bg-success">
               <h5 class="card-title">
                   {{ stock.name }}
                   <small>(Price: {{ stock.price }})</small>
                   </h5>
            </div>
            <div class="card-body">
                <div class="row">
                    <div class="col-sm-7">
                        <input class="form-control" placeholder="Quantity" 
                        v-model.number="quantity" type="number" 
                        :class="{danger: insufficientFunds}"
                        >
                    </div>
                    <div class="col-sm-5 pr-0">  
                        <button class="btn btn-success float-right" 
                            @click="buyStock"
                            :disabled=" insufficientFunds || quantity <= 0 || !Number.isInteger(quantity)"
                            >{{ insufficientFunds ? 'insufficientFunds' : 'Buy' }}
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .danger{
         border: 3px solid red;
    }
</style>

<script>

    export default {
        props:['stock'],
        data(){
            return {
                quantity: 0,
            }
        },
        computed:{
            funds(){
                return this.$store.getters.funds;
            },
            insufficientFunds(){
                return this.quantity * this.stock.price > this.funds;
            }
        },
        methods:{
            buyStock(){
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity,
                };
                this.$store.dispatch('buyStock', order);
                this.quantity = 0;
            }
        }
    }
</script>