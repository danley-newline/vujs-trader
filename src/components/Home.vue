<template>
    <div class="mt-5 text-center">
        <h1>Trader ou verifier votre porte monnaie</h1>
        <h6>Sauvegarder et charger vos donnees</h6>
        <h6>Click sur 'End Day' pour debuter une nouvelle Day</h6>
        <hr>
        <p>Your Funds: {{ funds | currency}}</p>
    </div>
</template>

<script>
    export default {
        computed:{
            funds(){
                return this.$store.getters.funds;
            }
        }
    }
</script>