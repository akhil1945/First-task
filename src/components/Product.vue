<template>

  <div class="category-sec">
  <button  @click="closeSideNav" class="filter-btn"> <i class="fa-solid fa-filter"></i>Filter</button>

    <div class="sidebar-sec desktop">
      
      <div class="sidenav" v-for="(items, index) in getFiltersData" :key="items._id">
        <div>
          <h2  @click="closeList(index)" class="dropdown-btn">
            {{ items.filter_lable }}
            <i class="fa-solid fa-minus" v-if="currentIndex == index"></i>
            <!-- <i class="fa fa-caret-up" v-else></i> -->
            <i class="fa-regular fa-plus" v-else></i>
          </h2>
          <div
            class="dropdown-container"
            v-for="(filter, i) in items.options"
            :key="i"
            v-show="currentIndex == index"
          >
            <a>
              <input type="checkbox" :checked="checkbox_control(filter.value)" name="plain" @click="getFilters(filter, index)" />
              {{filter.value}}
            </a>
          </div>
        </div>
      </div>
    </div>
  
    <div class="sidebar-sec mobile" v-show="seen" id="hide">
      <div class="close-btn" @click="closeSideNav"><i class="fa-solid fa-circle-xmark"></i></div>
      <div class="sidenav" v-for="(items, index) in getFiltersData" :key="items._id">
        <div>
          <h2  @click="closeList(index)" class="dropdown-btn">
            {{ items.filter_lable }}
            <i class="fa-solid fa-minus" v-if="currentIndex == index"></i>
            <!-- <i class="fa fa-caret-up" v-else></i> -->
            <i class="fa-regular fa-plus" v-else></i>
          </h2>
          <div
            class="dropdown-container"
            v-for="(filter, i) in items.options"
            :key="i"
            v-show="currentIndex == index"
          >
            <a href="#">
              <input type="checkbox" :checked="checkbox_control(filter.value)" name="plain" @click="getFilters(filter, index)" />
              {{filter.value}}
            </a>
          </div>
        </div>
      </div>
    </div>
    <div class="main-product-sec">
      <div class="sorting-sec">
        <!-- <strong>Sort by :</strong> -->
        <select v-model="getSort" @change="getSorting(getSort)">
          <option selected value="">Sort by:</option>
          <option v-for="sort in getSortingData" :key="sort.id" :value="sort.code" >{{sort.label}}</option>
        </select>
      </div>
      <LoaderPage v-if="loader"/>
      <div class="cat-product-sec">
        <div class="cat-product" v-for="product in getImagesData" :key="product._id">
          <div class="product-cont">
            <img :src=" product.image" />
          </div>
          <div class="product-infos">
            <p class="product-name">{{product.name}}</p>
            <p class="product-price">
              <span class="original-price">Rs.{{product.price}}</span>
            </p>
          </div>
        </div>
      </div>
      
    </div>
    <div class="pagination-sec">
        <p>Page<span>{{count}}</span> of {{Math.ceil(getTotalData/20)}}</p>
      <div class="pagination">
        <ul class="pagination-box">
         
        <button  @click="onClickPageButton(index)" :class="{activeBackground: count == index + 1}"  v-for="(item, index) in new Array(10)" :key="index">{{ index + 1 }}</button>
         
         
         <button @click="increment">Next</button>
        <!-- <button>2</button>
        <button>3</button>
        <button>4</button>
        <button>5</button> -->
        </ul>
      </div>
  </div>
  </div>
</template>

<script>
import LoaderPage from '../components/LoaderPage.vue'
// import Vue from "vue";
import axios from "axios";
export default {
  name: "product-page",
  components: {
    LoaderPage

  },
  
  

  data() {
    return {
      getFiltersData: [],
      currentIndex: null,
      filterCheck: '',
      selectedIndex: null,
      //  isShow: false,
      getImagesData: [],
      getSortingData:[],
      appliedFilters:[],
      // getTotalData:[],
      check: '',
      getSort:'',
      count: 1,
      loader: false,
       isHidden: true,
        seen: false

      // selectedSort: ""
    };
    
  },
  mounted() {
    this.getProducts();
  },
  methods: {
    onClickPageButton(index){
      console.log('index', index)
      this.count = index + 1;
      console.log('this.count', this.count)
      this.getProducts();
    },
    closeSideNav(){
      this.seen = !this.seen
      
    },
    checkbox_control(item){
      let a=this.appliedFilters.findIndex((x)=> x.filter_value==item)>=0
      ? true
      :false
      return a;
    },
    closeList(loopIndex) {
      if (this.currentIndex == loopIndex) {
        this.currentIndex = null;
      } else {
        this.currentIndex = loopIndex;
      }
    },
     rmByIndex(index){
      this.appliedFilters.splice(index, 1);
     },
     indexFilter(arr, value, code){
      let index =arr.findIndex(
        (x) => x.filter_code == value && x.filter_value == code
      );
     return index
     },
    getFilters(filter, index){
      this.selectedIndex = index
      let isvalue = this.indexFilter(this.appliedFilters, filter.code, filter.value)
      if(isvalue >=0){
        this.rmByIndex(isvalue)
      }
      else{
     let filter_key_code= filter.code + '-' + filter.value;
     filter_key_code= filter_key_code.split(" ").join("%2B")
     filter_key_code= filter_key_code.split("&").join("%26")
     let obj ={};
     obj["filter_key_code"] =filter_key_code; 
     obj["filter_value"] =filter.value; 
     obj["filter_code"] =filter.code; 
     this.appliedFilters.push(obj);
      }
     console.log('a',this.appliedFilters);
     for (let a in this.appliedFilters){
      console.log('b',a );
      console.log('c', this.appliedFilters[a])
      console.log('d', this.appliedFilters);
      if(this.appliedFilters[this.appliedFilters.length-1]==this.appliedFilters[a]){
        console.log('this.appliedFilters[this.appliedFilters.length-1]', this.appliedFilters[this.appliedFilters.length-1]);
        this.filterCheck= this.filterCheck.concat("",this.appliedFilters[a].filter_key_code)
      }
      else{
        this.filterCheck=this.filterCheck.concat(",",this.appliedFilters[a].filter_key_code)
      }
      console.log(this.filterCheck);
     }
      this.getProducts()
    },

    getSorting(getSort){
      this.check = getSort;
      console.log('getSort', this.check)
      
      this.getProducts()
    },
     increment() {
      console.log('+')
      this.count = this.count+1;
      this.getProducts();
    },
    


    async  getProducts() {
     try {
       this.loader = true;
      if(this.filterCheck==''&&this.getSort==''&&this.count==1){
        await axios
        .get(
          `https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter=`
        )
        .then(res => {
          this.getFiltersData = res.data.result.filters;
          this.getImagesData = res.data.result.products;
          this.getSortingData = res.data.result.sort;
          this.getTotalData = res.data.result.count;

          console.log(res);
          this.loader = false;
        });
      } else{
        this.loader = true
        axios
        .get(
          `https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=${this.count}&count=20&sort_by=${this.check}&sort_dir=desc&filter=${this.filterCheck}`
        )
        .then(res => {
          this.getImagesData = res.data.result.products;
          console.log(res);
          this.loader = false;
        });
      }
    } catch (error) {
        console.log(error);
      }
    },
    
  },
    
};



</script>


<style>

@media screen and (max-width: 767px){

  .category-sec i.fa-solid.fa-filter {
    padding-right: 5px;
}

    .footer-social-icon {
    padding-bottom: 60px !important;
   }
  .category-sec .cat-product {
    float: left;
    width: calc(50% - 10px) !important;
    margin: 0px 5px;
        padding: 0 !important;
}
.main-product-sec {
    float: left !important;
    width: 100% !important;
    margin-bottom: 20px;
}
.footer-menu {
    float: left;
    width: 100%;
}

  .close-btn i.fa-solid.fa-circle-xmark {
    font-size: 22px;
    color: #a28a61;
}
.category-sec button {
    position: fixed;
    bottom: 0;
    left: 0;
    z-index: 9999;
    width: 50%;
    height: 35px;
    background-color: #fff;
    border: none;
    border-right: 1px solid #ccc;
    
    box-shadow: 0px 1px 3px #000;
}
.sorting-sec {
    position: fixed;
    width: 50%;
    right: 0;
    bottom: 0;
    background-color: #ccc !important;
       margin-right: 0 !important;
}
.sorting-sec select {
    width: 100%;
    height: 35px;
    background-color: #fff;
    text-align: center;
    box-shadow: 0px 1px 3px #000;
    border: 0;
}
.sidebar-sec {
   display: block;
    position: fixed;
    background-color: #FFF !important;
    TOP: 0;
    LEFT: 0;
    RIGHT: 130px;
    MARGIN-TOP: 0 !important;
    OPACITY: 1;
    overflow: auto;
    bottom: 0;
        width: auto !important;
        height: 100%;
            box-shadow: 0px 4px 3px #000;
}
.sidenav {
    height: auto !important;
}
.sidenav:first-child {
    padding-top: 40px;
}

.close-btn {
    text-align: right;
    margin-top: 12px;
    margin-right: 10px;
}
.pagination button {
  position: static;
    width: auto;
    padding: 0px 10px !important;
}
.sidebar-sec.desktop {
    display: none;
}
sidebar-sec.mobile {
    display: block !important;
}
button.filter-btn {
    display: none;
}
button.filter-btn {
    display: block !important;
}

}
button.filter-btn {
    display: none;
}

sidebar-sec.mobile {
    display: none;
}
.sidenav {
  height: 100%;
  width: 100%;
  position: static;
  z-index: 1;
  top: 0;
  left: 0;
  background-color: transparent;
  overflow-x: hidden;
  border-bottom: 1px solid #ccc;
  padding-bottom: 15px;
  padding-top: 14px;
}

.sidenav a,
.dropdown-btn {
  padding: 6px 8px 6px 0px;
  text-decoration: none;
  font-size: 14px;
  color: #303030;
  display: block;
  border: none;
  background: none;
  width: 100%;
  text-align: left;
  cursor: pointer;
  outline: none;
  margin-top: 0;
}

.main {
  margin-left: 200px; /* Same as the width of the sidenav */
  font-size: 20px; /* Increased text to enable scrolling */
  padding: 0px 10px;
}
.activeBackground{
 background: rebeccapurple !important;
    color: #fff !important;
}
.active {
  background-color: green;
  color: white;
}

.fa-caret-down {
  float: right;
  padding-right: 8px;
}
h2.dropdown-btn {
  font-weight: 600;
}
.product-infos span.compare-price {
  text-decoration: line-through;
  display: inline-block;
  color: #303030;
  font-size: 14px;
}
.product-infos span.original-price {
  display: inline-block;
  color: #501337 !important;
  font-size: 17px;
}
.cat-product {
  float: left;
  width: 80%;
}
.sidebar-sec {
  float: left;
  width: calc(20% - 20px);
  padding: 0px 10px;
  margin-top: 40px;
}
.category-sec {
  text-align: left;
}
.category-sec .cat-product {
  float: left;
  width: calc(25% - 20px);
  padding: 0px 10px;
}
.product-infos {
  height: 95px;
}
.cat-product .product-cont img {
  width: 100%;
  max-height: 336px;
}
.sidenav h2.dropdown-btn i {
  float: right;
}
.main-product-sec {
  float: left;
  width: 80%;
      margin-bottom: 20px;
}
.product-infos p {
  font-size: 14px;
  color: #303030;
  line-height: 20px;
}
.product-infos p.product-price span {
  font-size: 14px;
}
.sorting-sec select {
  width: 100%;
  height: 35px;
}

.sorting-sec {
  float: right;
  max-width: 250px;
  width: 200px;
  margin-right: 15px;
}
.sorting-sec select {
  width: 100%;
  height: 35px;
}
.cat-product-sec {
  margin-top: 60px;
}
.sorting-sec select:focus {
    outline: 0;
}
.pagination {
  display: inline-block;
}
ul.pagination-box {
    padding: 0;
    margin: 0;
}

.pagination button {
  color: black;
    float: left;
    padding: 8px 11px;
    text-decoration: none;
    font-size: 14px;
    background: transparent;
    margin: 0px 4px;
    box-shadow: none;
    border: 1px solid #ccc;
    cursor: pointer;
}
/* .pagination button:focus {
    background-color: rebeccapurple;
    color: #fff;
    font-size: 14px;
    border-color: rebeccapurple;
} */
.pagination button.next-page {
    border: 1px solid #ccc;
    padding: 5px 11px;
    font-size: 14px;
    letter-spacing: 0.8px;
}
.pagination-sec p {
    
         float: left;
    padding-left: 10px;
    font-size: 14px;
}
.pagination-sec {
       margin-bottom: 50px;
    border-top: 1px solid #f1f1f1;
    float: left;
    width: 100%;
    padding-top: 20px;
    text-align: center;

}

</style>