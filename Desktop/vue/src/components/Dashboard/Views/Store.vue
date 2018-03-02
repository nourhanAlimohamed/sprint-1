<template>
<div>

  <input v-model="name" placeholder="ex: channel bag">
  <p>{{ message }}</p>
  <input v-model="price" placeholder="ex: 1000">
<p>{{ message }}</p>
<button type="button" v-on:click="addproducts">add product</button>
    <table id="firstTable">

  <thead>
    <tr>
      <th>ID</th>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>

      <th>Name</th>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>

      <th>price</th>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>

      <th>created at</th>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>
      <th>updated at</th>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>
      <th>Action</th>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>
      <th> sellerName </th>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>

    </tr>
  </thead>
  <tbody>
    <tr v-for="row in products.data">
      <td>{{row._id}}</td>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>

      <td>{{row.name}}</td>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>

      <td>{{row.price}}</td>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>


      <td>{{row.createdAt}}</td>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>


      <td>{{row.updatedAt}}</td>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>

      <td>{{row.Action}}</td>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>

      <td>nourhan ali</td>
      <div style="width: 100px; " v-bind:style="{ 'background-color': color }"></div>

    </tr>
  </tbody>
</table>
<input v-model="del" placeholder="ex: 5a986d92db523d0554cc4c0d">
<p>{{ message }}</p>
<button type="button" v-on:click="deleteprod">delete product</button>
<p>{{ message }}</p>
<p>{{ message }}</p>
<input  v-model="name2" placeholder="ex: nourhan">name </input>
<p>{{ message }}</p>
<input v-model="price2" placeholder="ex: 199">price </input>
<p>{{ message }}</p>
<input v-model="del2" placeholder="ex: 5a986d92db523d0554cc4c0d">ID </input>
<p>{{ message }}</p>
<button type="button"v-on:click="updateProd">update product</button>
<p>{{ message }}</p>

</div>
</template>
<script>

import axios from 'axios'
import PaperTable from 'components/UIComponents/PaperTable.vue'
const tableColumns = ['_Id', 'Name', 'Price', 'createdAt', 'updatedAt', 'sellerName', 'Action', '']
const tableData = [{
  id: 1,
  name: 'Dakota Rice',
  price: '$36.738',
  createdat: '15/2/2018',
  updatedat: '16/2/2018',
  sellername: 'Mo'
},
{
  id: 2,
  name: 'Minerva Hooper',
  price: '$36.738',
  createdat: '15/2/2018',
  updatedat: '16/2/2018',
  sellername: 'Mo'
}]
export default {
  components: {
    PaperTable
  },
  data () {
    return {
      table1: {
        title: 'Stripped Table',
        subTitle: 'Here is a subtitle for this table',
        columns: [...tableColumns],
        data: [...tableData]
      },
      table2: {
        title: 'Table on Plain Background',
        subTitle: 'Here is a subtitle for this table',
        columns: [...tableColumns],
        data: [...tableData]
      },
      products: [],
      name: '',
      price: '',
      sellername: '',
      del2: '',
      name2: '',
      price2: ''
    }
  },
  created () {
    this.getproducts()
  },
  methods: {
    AddToApi () {
      let newtable = {
        tablecolumns: this.table1.tableColumns,
        tabledata: this.table1.tableData
      }
      axios.post('http://localhost:3000/User')
    .then((response) => {
      console.log(response)
    })
    .catch((error) => {
      console.log(error)
    })
    },
    getproducts () {
      axios.get('http://localhost:3000/api/product/getProducts')
      .then((response) => {
        this.products = response.data
        console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    addproducts () {
      axios.post('http://localhost:3000/api/product/createProduct', {
        name: this.name,
        price: this.price,
        sellername: this.sellername
      })
      .then((response) => {
        console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    deleteprod () {
      axios.delete('http://localhost:3000/api/product/deleteProduct/' + this.del)
      .then((response) => {
        console.log(response)
      })
    },
    updateProd () {
      axios.patch('http://localhost:3000/api/product/updateProduct/' + this.del2, {
        name: this.name2,
        price: this.price2
      })
      .then((response) => {
        console.log(response)
      })
    }
  }
}
  </script>
<style>

</style>
