<template>
  <div id="app">
    <b-container class="container-space" fluid>
      <header>
        <h1>Which products would you like to add?</h1>
        <div class="row">
          <div class="brief">
            <div class="icon">
              <b-icon icon="exclamation-circle"></b-icon>
            </div>
            <p> Here you can fill an importsheet with the products you want to add to your shop. Just follow the steps below.</p>
          </div>
        </div>
      </header>
      
      <DataSelector :sheets="sheets" :brands="brands" @change:select="onChangeBrand" :products="selectedProducts" @reset:form="onResetProducts" />
      <ProductList :visible_comp="visible" :products="selectedProducts" />
    </b-container>    
  </div>
</template>

<script>
import DataSelector from './components/DataSelector.vue'
import ProductList from './components/ProductList.vue'
import { BIcon, BIconExclamationCircle } from 'bootstrap-vue'

export default {
  

  name: 'App',
  data () {
    return {
      // sheetId: '',
      sheets: [{ text: 'Select one', value: '' }],
      brands: [{ text: 'Select a Brand', value: ''}],
      selectedProducts: [],
      visible: 'invisible'
    }
  },
  components: {
    DataSelector, 
    ProductList,
    BIcon,
    BIconExclamationCircle
  },
  methods: {
    async fetchImportSheetData() {

      try {
        const response = await fetch('https://s3.eu-west-1.amazonaws.com/hungarian.phrasebook/decodata-frontend-assignment/importsheets.json')

        const data = await response.json();
              
        const sheetList = data.map(sheet => ({id: sheet.id,  value: sheet.id, text: sheet.name}))
              
        return sheetList
      } catch (err) {
        console.log(err)
      }
    },
    async fetchBrandData() {

      try {
        const response = await fetch('https://s3.eu-west-1.amazonaws.com/hungarian.phrasebook/decodata-frontend-assignment/product_data.json')

        const data = await response.json()
              
        let brandData = [];
        for (let elem in data) {
            brandData = [...brandData, {id: data[elem].brand_name,  value: data[elem].brand_name, text: data[elem].name, images: [...data[elem].images]}]
        }
        
        return brandData
      } catch (err) {
        console.log(err)
      }
    },
    onChangeBrand(selected) {
        const filteredProducts = this.brands.filter(brand => brand.value === selected)
        const product = {
            brand: filteredProducts[0].id,
            product_name: filteredProducts[0].text,
            images: [...filteredProducts[0].images]
        }
        this.visible = ''
        this.selectedProducts = [...this.selectedProducts, product]
        
    },
    onResetProducts() {
      this.visible = 'invisible'
      this.selectedProducts = [];
    }
  },
  async created() { 
    const importSheets = await this.fetchImportSheetData()
    this.sheets = [...this.sheets, ...importSheets]

    const importBrand = await this.fetchBrandData()
    this.brands = [...this.brands, ...importBrand]
    
  }
  
}
</script>

<style>
#app {
  font-family: Poppins, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  color: #070b60;
  background-color: #fff;
}
.row {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  margin-bottom: 20px;
}
.brief {
  display: flex;
  width: 90%;
  text-align: left;
}
.icon {
  display: flex;
  align-items: center;
  margin-right: 20px;
  font-size: 30px;
}
.brief p {
  margin: 0;
  font-size: 14px;
}
h1 {
  font-size: 30px;
  margin-bottom: 20px;
}
.container-space {
  width: 90%;
  background-color: #fbebf6;
}
</style>
