<template>
   <div class="card">
       <div class="card-body">
           <img class="card-img-top" :src="product.image_url" alt="Card image cap" />
            <div class="card-body">
                <h4 class="card-text">{{product.title}} </h4>
                <p class="card-text text-center">{{product.price}} </p>
                <button class="btn btn-primary text-center" @click="addToCart(product)"><i class="fa fa-shopping-cart"></i> Add To Cart</button>
            </div>
       </div>
    </div>
</template>

<script>
    export default {
               props:['product', 'cart'],
        mounted() {
            console.log('Component mounted.')
        },
        methods:{
             addToCart(product){
                 this.cart.push(product)
                console.log(this.cart)
               // axios.post(`cart/add/${id}`)
            }
        }
    }
</script>

<style >

</style>


