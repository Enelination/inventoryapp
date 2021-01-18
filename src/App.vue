<template>
<nav class="navbar navbar-dark  bg-success">
  <span class="navbar navbar-brand mb-0 h1"> Inventory</span>
</nav>
<br>
<br>

<div class="container">
  <div class="row">
    <div class="col-md-12">
      <label for=""> Sort By:</label>
      <select v-model="filterValue">
        <option value="">Show All</option>
        <option value="availability">Availability</option>
        <option value="search">Search</option>
      </select>
    </div>
  </div>
  <br>
  <div class="row">
    <div class="col-md-12">
      <span v-show="availabilitySelected()">
        Availability
        <label>Availabile: <input v-bind:value="true " type="radio" name="available" v-model="radioValue"></label>
        <label>Not Availabile: <input v-bind:value="false" type="radio" name="available"  v-model="radioValue"></label>
      </span>
    </div>
  </div>

  <br>


  <div  v-show="!searchSelected()" class="row">
    <div class="col-md-12">
      <h3>Product Inventory</h3>
      <table class="table">
        <thead>
          <th>Name</th>
          <th>Price</th>
          <th>Rating</th>
          <th>Availability</th>
          <th>Seller</th>
          <th>Product ID</th>
          <th>Discount %</th>
          <th>Actual Price</th>
        </thead>
        <tbody>
          <tr v-show="filterByAvailability(product)" v-bind:class="highlight(product)" v-for="product in products" v-bind:key="product">
            <td>{{product.name}}</td>
            <td>{{product.price}}</td>
            <td>{{product.rating}}</td>
            <td>{{product.available}}</td>
            <td>{{product.seller}}</td>
            <td>{{product.productid}}</td>
            <td>{{product.discount}}</td>
            <td>{{priceAfterDiscount(product)}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

  <div v-show="searchSelected()" class="row">
    <div class="col-md-12">
      <label for="">Search By:</label>
      <select v-model="searchFilterValue">
        <option value="name">Name</option>
        <option value="seller">Seller</option>
      </select>
    </div>
  </div>
  <br>

  <div  v-show="searchSelected()" class="row">
    <div class="col-md-12">
      <label for="">Search: <input type="text" v-model="searchTerm" placeholder="Search Here"></label>
    </div>
  </div>
  <br>

   <div  v-show="searchSelected()" class="row">
    <div class="col-md-12">
      <h3>Search result</h3>
      <table class="table">
        <thead>
          <th>Name</th>
          <th>Price</th>
          <th>Rating</th>
          <th>Availability</th>
          <th>Seller</th>
          <th>Product ID</th>
          <th>Discount %</th>
          <th>Actual Price</th>
        </thead>
        <tbody>
          <tr v-show="search(product)" v-bind:class="highlight(product)" v-for="product in products" v-bind:key="product">
            <td>{{product.name}}</td>
            <td>{{product.price}}</td>
            <td>{{product.rating}}</td>
            <td>{{product.available}}</td>
            <td>{{product.seller}}</td>
            <td>{{product.productid}}</td>
            <td>{{product.discount}}</td>
            <td>{{priceAfterDiscount(product)}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>
</template>





<script>

export default {

  methods:{
    searchSelected(){
      if(this.filterValue === 'search'){
        return true
      }else{
        return false
      }
    },
    search(product){
      let result = false
      if(this.searchTerm !== ''){
        let term = this.searchTerm.toLowerCase()
        let searchFeild = product[this.searchFilterValue].toString().toLowerCase()
         result = searchFeild.includes(term)
      }
      return result
    },
    priceAfterDiscount(product){
      return product.price - (product.price * product.discount/100)

    },


    highlight(product){
      if (product.available === "Yes"){
        return 'table-success'
      }else{
        return 'table-danger'
      }

    },


    availabilitySelected(){
      return this.filterValue === 'availability'
    },



    filterByAvailability(product){
      if(product.available === "Yes" && this.radioValue === true){
         return true
      }
      else if(product.available === "No" && this.radioValue === false){
        return true

      }else if(this.filterValue === ""){
        return true
      }
      else{
      return false
      }
    }

  },


  data(){
    return{
      searchFilterValue:'',
      filterValue:'',
      radioValue:"",
      searchTerm:'',
     products:[
       {
    "name": "iPhone",
    "price": 10000,
    "rating": 4.5,
    "available": "Yes",
    "seller": "Apple",
    "productid": 1,
    "discount": 20
  },
  {
    "name": "iLaptop",
    "price": 2345,
    "rating": 4.8,
    "available": "No",
    "seller": "ABC Corp",
    "productid": 2,
    "discount": 10
  },
  {
    "name": "Microwave",
    "price": 378,
    "rating": 4.3,
    "available": "Yes",
    "seller": "XYZ inc",
    "productid": 3,
    "discount": 15
  },
  {
    "name": "Heater",
    "price": 34,
    "rating": 4.7,
    "available": "Yes",
    "seller": "Marine labs",
    "productid": 4,
    "discount": 5
  },
  {
    "name": "Book",
    "price": 12,
    "rating": 3.4,
    "available": "Yes",
    "seller": "boookish",
    "productid": 5,
    "discount": 5
  },
  {
    "name": "Telescope",
    "price": 456,
    "rating": 5,
    "available": "Yes",
    "seller": "Space tech",
    "productid": 6,
    "discount": 8
  },
  {
    "name": "Charger",
    "price": 10,
    "rating": 3.9,
    "available": "No",
    "seller": "XYZ Electronics",
    "productid": 7,
    "discount": 23
  },
  {
    "name": "Matress",
    "price": 120,
    "rating": 4.1,
    "available": "Yes",
    "seller": "Sleep Inc",
    "productid": 8,
    "discount": 5
  },
  {
    "name": "Neon bulb",
    "price": 7,
    "rating": 4.3,
    "available": "Yes",
    "seller": "Sleep Inc",
    "productid": 9,
    "discount": 2
  },
  {
    "name": "Coffee mug",
    "price": 23,
    "rating": 4.3,
    "available": "No",
    "seller": "The Cafe company",
    "productid": 10,
    "discount": 0
  }
     ]
    }
  },
  
  
 
}

</script>
