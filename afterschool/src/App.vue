<template>
    <div id="app">
      <header>
        <h3>{{sitename}}</h3>
        <button @click="showCheckout">{{this.cart.length}} Checkout</button>
      </header>
      <product-list :products ="products" @addProduct='addToCart'></product-list>
      <checkout :cart="cart" @removeProduct='removeFromCart'></checkout>
    </div>
</template>

<script>
import Checkout from './components/Form.vue'
import productList from './components/Products.vue'

export default {
  
        components: {
            productList,
            Checkout
        },
        name: "App",
        data() {
            return {
              sitename:"Afterschool Application",
                cart: [],
                products: [{
                        subject: "Architecture",
                        location: "Latvia",
                        price: 3220,
                        description: "Learn to design structures with us",
                        image: 'product-geo.jpg',
                        inventory: 10,
                        inCart: 0
                    },
                    
                ]
            }
        },
        methods: {
            showCheckout: function(){
                    this.showProduct = this.showProduct ? false : true;
                },
            addToCart(product){
                let added = false;
                this.cart.forEach((product2) => {
                    if(product2.id === product.id){
                         product.inCart++
                         added = true
                    }
                });
                    if(!added){
                        this.cart.push(product)
                        product.inCart = 1
                    }    
                        product.inventory--; 
             
            },
            removeFromCart(product){
                this.cart.forEach((product2) => {
                    if(product2.id === product.id) {
                        product.inventory++;
                        product.inCart--
                    }
                })
            }    
        }
    }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style