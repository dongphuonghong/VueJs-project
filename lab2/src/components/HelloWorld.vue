<template>
  <div id="app">
    <h1>Danh sách sản phẩm</h1>
    <label for="">Enter your search terms</label>
    <input type="text" v-model="search">
    <ul>
      <li v-for="product in filteredProducts" :key="product">{{ product }}</li>
    </ul>
  </div>
  <h2>BÁN HÀNG</h2>
  <div class="sp">
  <label for="From">from</label>
  <input type="text" v-model="from">
  <label for="To">to</label>
  <input type="text" v-model="to">
  </div>
<table>
  <tr>
    <th>Hàng hóa</th>
    <th>đơn giá</th>
    <th>Số lượng</th>
    <th>Thành tiền</th>
  </tr>
  <tr v-for="product in filteredProducts" :key="product">
    <td>{{ product.name }}</td>
    <td>{{ product.price }}</td>
    <td>              
      <input               type="checkbox"               :checked="product.checked"
              @change="toggleCheck(product)"
            >

            <input type="number"
              v-model="product.quantity"
              :disabled="!product.checked"
              @input="calculateSubtotal(product)"
            >
              </td>
              <td>{{ product.subtotal }}</td>
  </tr>
  <tr>
    <td>Tổng tiền</td>
    <td>{{ total }}</td>
  </tr>
</table>  
</template>
<script>
export default {
  name: 'App',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      from:0,
      to:0,
      total:0,
      products: [
                { name: "iPhone 9", price: 700, quantity: 0, subtotal: 0, checked: false },
        {
          name: "Samsung",
          price: 400,
          quantity: 1,
          subtotal: 400,
          checked: true,
        },
        { name: "Nokia", price: 100, quantity: 0, subtotal: 0, checked: false },
        {
          name: "Sony Xperia",
          price: 450,
          quantity: 0,
          subtotal: 0,
          checked: false,
        },
        {
          name: "Motorola",
          price: 180,
          quantity: 0,
          subtotal: 0,
          checked: false,
        },
        { name: "Oppo", price: 600, quantity: 0, subtotal: 0, checked: false },
        { name: "bPhone", price: 90, quantity: 2, subtotal: 180, checked: true },
    ],
    computed:{
      filteredProducts(){
              return this.products.filter(        (product) => product.price >= this.from && product.price <= this.to);      
},
    total(){
            return this.products.reduce((sum, product) => sum + product.subtotal, 0);
    }, 
        methods: {
    toggleCheck(product) {
      product.checked = !product.checked;
      if (!product.checked) {
        product.quantity = 0;
        product.subtotal = 0;
      }
      this.calculateTotal();
    },
    calculateSubtotal(product) {
      product.subtotal = product.price * product.quantity;
      this.calculateTotal();
    },
    }
    },
      search: "",
      product1s: [
        "Taya Bánh Mì den",
        "Bánh mì nướng",
        "Hạnh Nhân nướng",
        "Bready cuộn nhân dừa",
      ],
    };
  },
  computed: {
    filteredProducts() {
      return this.products.filter(product =>
        product.toLowerCase().includes(this.search.toLowerCase())
      );
    },
  },
  watch: {
    search() {    
      console.log("abf");
    },
  },
  from:0,
  to:0,
        products: [
        { name: "iPhone 9", price: 700, quantity: 0, subtotal: 0, checked: false },
        {
          name: "Samsung",
          price: 400,
          quantity: 1,
          subtotal: 400,
          checked: true,
        },
        { name: "Nokia", price: 100, quantity: 0, subtotal: 0, checked: false },
        {
          name: "Sony Xperia",
          price: 450,
          quantity: 0,
          subtotal: 0,
          checked: false,
        },
        {
          name: "Motorola",
          price: 180,
          quantity: 0,
          subtotal: 0,
          checked: false,
        },
        { name: "Oppo", price: 600, quantity: 0, subtotal: 0, checked: false },
        { name: "bPhone", price: 90, quantity: 2, subtotal: 180, checked: true },
      ],
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>