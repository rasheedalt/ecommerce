<template>
    <div >
        <HeaderComponent :cart="cart" />

        <div class="row container">
            <div class="col-md-8">
                <div class="jumbotron">
                    <h1 class="display-4">Hello, world!</h1>
                    <p class="lead">This is a simple hero unit, a simple jumbotron-style component for calling extra attention to featured content or information.</p>
                    <hr class="my-4">
                    <p>It uses utility classes for typography and spacing to space content out within the larger container.</p>
                    <p class="lead">
                        <a class="btn btn-primary btn-lg" href="#" role="button">Learn more</a>
                    </p>
                </div>
            </div>
        </div>
        
        <h1 class="text-center py-3">POPULAR PRODUCTS</h1>

        <div class="row mt-3 justify-content-center">
            <div class="col-md-3 m-1" v-for="product in products" :key="product.id">
                <CardComponent  :product="product" :cart="cart" />
            </div>
        </div>

        <FooterComponent />
    </div>
</template>

<script>

    import HeaderComponent from './components/HeaderComponent';
    import CardComponent from './components/CardComponent';
    import FooterComponent from './components/FooterComponent';
    export default {
        components:{
         HeaderComponent,
         CardComponent,
         FooterComponent,
    },
        mounted() {
            this.getProducts();
            console.log(this.products)
        },
        data(){
            return{
                cart: [],
                user: '',
                products: '',
                items: ''
            }
        },
        computed:{
            authenticated(){
                if(localStorage.getItem('user')){
                    return true;
                }
                return false;
            },
            isAdmin(){
                var user;
                if(this.authenticated){
                   user = JSON.parse(localStorage.getItem('user'))
                   if(user.role == 'admin'){
                    return true;
                   }
                   return false
                }
                return false;
            },
            cartItems(){
                var items;
                
                if(this.authenticated){
                    axios.get(`/cart/add`)
                    .then((res)=>{
                        items = res.data.data
                    }) 
                   return items
                }
                return '';
            }
        },
        methods:{
            getProducts(){
                axios.get(`/products`)
                    .then((res)=>{
                        this.products = res.data.data
                    })
            },
            addToCart(product){
                console.log(product)
                axios.post(`cart/add/${id}`)
            },
            removeFromCart(id){
                axios.delete(`cart/remove/${id}`)
            },
        }
    }
</script>
