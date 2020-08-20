<template>
    <div class="col-sm-6 col-md-4 mt-4">
        <div class="card">
            <div class="card-header bg-info">
               <h5 class="card-title">
                   {{ stock.name }}
                   <small>(Price: {{ stock.price }} | Quantity: {{ stock.quantity }})</small>
                   </h5>
            </div>
            <div class="card-body">
                <div class="row">
                    <div class="col-sm-7">
                        <input class="form-control" placeholder="Quantity" 
                        v-model.number="quantity" type="number"
                        :class="{danger: insufficientQuantity}">
                    </div>
                    <div class="col-sm-5 pr-0">  
                        <button class="btn btn-success float-right" 
                            @click="sellStock"
                            :disabled="quantity <= 0 || !Number.isInteger(quantity) || insufficientQuantity"
                            >{{ insufficientQuantity ? 'too much this' : 'Sell' }}
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .danger{
        border: 1px solid red;
    }
</style>

<script>
    import {mapActions} from 'vuex';

    export default {
        props:['stock'],
        data(){
            return {
                quantity: 0,
            }
        },
        computed:{
            insufficientQuantity(){
                return this.quantity > this.stock.quantity;
            }
        },
        methods:{
            ...mapActions({
                placeSellOrder: 'sellStock'
        }),
            sellStock(){
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity
                };
                this.placeSellOrder(order);
                this.quantity = 0;
            }
            
        }
    }
</script>