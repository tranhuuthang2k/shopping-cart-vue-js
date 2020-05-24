<template>
 <div id="app">
   <nav class="nav">
     <h2 class="nav_header">Products</h2>
     <div class="nav_cart">
        <button  @click="showCart = !showCart">
          <img src="https://image.flaticon.com/icons/png/512/60/60992.png" alt="" style="width: 5%;">
        </button>
        <span class="total-quantity">{{ totalQuantity }}</span>
        <div class="cart_dropdown" v-if="showCart" >
          <ul class="cart-dropdown_list" v-for="product in cart" :key="product.id">
              <li>{{ product.name }} ({{ product.quantity }})</li>
          </ul>
        </div>
     </div>
   </nav>
   <section class="products">
     <div   v-for="product in products" :key="product.id" class="product">
       <h3 class="product_header"> {{ product.name }}</h3>
       <img src="https://via.placeholder.com/150" alt="" class="product_images">
       <p class="product_description" >{{ product.description }}</p>
       <div class="cart">
                <button class="cart_button"  @click="updateCart(product, 'subtract')">-</button>
                <span class="cart_quanlity"  >{{ product.quantity }}</span>
                 <button class="cart_button"  @click="updateCart(product, 'add')"> +</button>
       </div>
     </div>
   </section>
 </div>
</template>

<script >

export default {
  name: 'App',
  components: {
  },
 data() {
    return {
      products: [
        {
          id: 1,
          name: 'Product 1',
          description: 'This is an incredibly awesome product',
          quantity: 0,
        },
        {
          id: 2,
          name: 'Product 2',
          description: 'This is an incredibly awesome product',
          quantity: 0,
        },
        {
          id: 3,
          name: 'Product 3',
          description: 'This is an incredibly awesome product',
          quantity: 0,
        }
      ],
      showCart: false,
       totalCart:0
    };
    
  },



   computed: { 
     cart() {
      return this.products.filter(product => product.quantity > 0);
    },
    totalQuantity() {
      return this.products.reduce(
        (total, product) => total + product.quantity,
        0
      );
    }
  },
 methods: {
      updateCart(product, updateType) {      
        for (let i = 0; i < this.products.length; i++) {
          //window.console.log(product);
         // window.console.log(this.products[i]);
          if (this.products[i].id === product.id) {
            if (updateType === 'subtract') {
              if (this.products[i].quantity !== 0) {
                this.products[i].quantity--;
              }
            } else {
              this.products[i].quantity++;
            }
            
            break;
          }
        }
      },

 }  
  
  //    watch:
  // {
    
  //   products: {
  //        handler(){
  //          window.console.log('change');
  //        this.totalQuantity();
  //        },
  //       deep:true,
  //       immediate:true
  //   }
   
  // },
    
}


</script>

<style>
* {
  box-sizing: border-box;
  font-weight: normal;
  margin: 0;
  padding: 0;
}
nav {
  align-items: center;
  background: salmon;
  color: white;
  display: flex;
  justify-content: space-between;
}
 button {
      background: none;
      border: 0;
      color: white;
      cursor: pointer;
 
 }
   .total-quantity {
      align-items: center;
      border-radius: 50%;
      display: flex;
      font-weight: bold;
      height: 2rem;
      justify-content: center;
      padding: 0.5rem;
      position: absolute;
      right: 217px;
      top: -3px;
      width: 2rem;
      color: black;
    }
    .cart-dropdown {
      background: white;
      border: 1px solid lightgray;
      border-radius: 10px;
      box-shadow: 0 0 2px rgba(0, 0, 0, 0.2);
      color: #333;
      font-size: 1.3rem;
      overflow: auto;
      padding: 0 1rem;
      position: absolute;
      right: 0;
      width: 12rem;
    }
      .cart-dropdown__list {
        list-style: none;
     }
       li {
          margin: 1rem 0;
        }
        .products {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
        }
        .product {
    border: 1px solid lightgray;
    border-radius: 10px;
    margin: 2rem;
    padding: 1rem;
        }
        .cart {
  margin-top: 2rem;
  text-align: center;
  }
.cart_button{
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
</style>
