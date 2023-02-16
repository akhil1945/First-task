<template>
  <section class="header-main-sec">
    <div class="navbar-sec desk-header" id="head-sec" :class="{sticky:active}">
      <div class="navbar left">
        <div class="dropdown">
          <button class="dropbtn">
            WOMEN
            <i class="fas fa-angle-down"></i>
          </button>
          <div class="dropdown-content">
            <a href="#">Link 1</a>
            <a href="#">Link 2</a>
            <a href="#">Link 3</a>
          </div>
        </div>
        <div class="dropdown">
          <button class="dropbtn">
            MEN
            <i class="fas fa-angle-down"></i>
          </button>
          <div class="dropdown-content">
            <a href="#">Link 1</a>
            <a href="#">Link 2</a>
            <a href="#">Link 3</a>
          </div>
        </div>
        <a href="#news" class="single-menu">SALE</a>
        <div class="dropdown">
          <button class="dropbtn">
            COLLECTION
            <i class="fas fa-angle-down"></i>
          </button>
          <div class="dropdown-content">
            <a href="#">Link 1</a>
            <a href="#">Link 2</a>
            <a href="#">Link 3</a>
          </div>
        </div>
        <a href="#">
          <img alt="Vue logo1" src="../assets/logo1.png" />
        </a>
        <div class="dropdown">
          <button class="dropbtn">
            OUR STORY
            <i class="fas fa-angle-down"></i>
          </button>
          <div class="dropdown-content">
            <a href="#">Link 1</a>
            <a href="#">Link 2</a>
            <a href="#">Link 3</a>
          </div>
        </div>
        <a href="#" class="single-menu">CRAFTSMANSHIP</a>
      </div>
      <div class="header-menu-right">
        <ul>
          <li>
            <a href="#">
              <img alt="Vue search-icon" src="../assets/search-icon.png" />
            </a>
          </li>
          <li>
            <a href="#">
              <img alt="Vue heart-icon" src="../assets/heart-icon.png" />
            </a>
          </li>
          <li>
            <a href="#">
              <img alt="Vue cart-icon" src="../assets/cart-icon.png" />
            </a>
          </li>
        </ul>
      </div>

  
    </div>
   
     <div class="navbar-sec mobile-header" id="head-sec" :class="{sticky:active}">
      <div class="mobile-header-content">
       <a href="#" class="menu-toggle" v-on:click="toggleSidenav">
            <img alt="Vue logo1" src="../assets/menu-cion.svg" />
          </a>
      
      <div class="mob-head-cont" v-show="seen" id="hide">
         
        <div class="navbar left" v-if="isHidden">
           <div class="close-btn" @click="toggleSidenav"><i class="fa-solid fa-circle-xmark"></i></div>
          <div class="dropdown">
            <button class="dropbtn" v-on:click="isHide = !isHide">
              WOMEN
              <i class="fas fa-angle-down"></i>
            </button>
            <div class="dropdown-content" v-if="!isHide">
              <a href="#">Link 1</a>
              <a href="#">Link 2</a>
              <a href="#">Link 3</a>
            </div>
          </div>
          <div class="dropdown">
            <button class="dropbtn" v-on:click="isHide = !isHide">
              MEN
              <i class="fas fa-angle-down"></i>
            </button>
            <div class="dropdown-content" v-if="!isHide">
              <a href="#">Link 1</a>
              <a href="#">Link 2</a>
              <a href="#">Link 3</a>
            </div>
          </div>
          <a href="#news" class="single-menu">SALE</a>
          <div class="dropdown">
            <button class="dropbtn" v-on:click="isHide = !isHide">
              COLLECTION
              <i class="fas fa-angle-down"></i>
            </button>
            <div class="dropdown-content" v-if="!isHide">
              <a href="#">Link 1</a>
              <a href="#">Link 2</a>
              <a href="#">Link 3</a>
            </div>
          </div>
        
          <div class="dropdown">
            <button class="dropbtn" v-on:click="isHide = !isHide"> 
              OUR STORY
              <i class="fas fa-angle-down"></i>
            </button>
            <div class="dropdown-content" v-if="!isHide">
              <a href="#">Link 1</a>
              <a href="#">Link 2</a>
              <a href="#">Link 3</a>
            </div>
          </div>
          <a href="#" class="single-menu">CRAFTSMANSHIP</a>
        </div>
        </div>
          <a href="#" class="mob-logo">
            <img alt="Vue logo1" src="../assets/mobile-logo.svg" />
          </a>
        <div class="header-menu-right">
          <ul>
            <li>
              <a href="#">
                <img alt="Vue search-icon" src="../assets/search-icon.png" />
              </a>
            </li>
            <li>
              <a href="#">
                <img alt="Vue heart-icon" src="../assets/heart-icon.png" />
              </a>
            </li>
            <li>
              <a href="#">
                <img alt="Vue cart-icon" src="../assets/cart-icon.png" />
              </a>
            </li>
          </ul>
        </div>
      </div>
      </div>
  </section>
</template>

<script>
export default {
  name: "MainHeader",

  data(){
      return{
      isHidden: false,
        seen: true,
        active: false,
         isHide: false
      }
  },
   methods: {
    toggleSidenav(){
      this.isHidden = !this.isHidden
    },
    closeSideNav(){
      this.seen = !this.seen 
    },
    toggleNavClass(){
        if(this.active == false){
          return 'desk-header'
        } else {
          return 'sticky-nav'
        }

    }
    
    
  },
   mounted(){
  window.document.onscroll = () => {
      let navBar = document.getElementById('head-sec');
      if(window.scrollY > navBar.offsetTop){
        console.log('navbar', window.scrollY)
        this.active = true;
        } else {
        this.active = false;
      }
    }
  }
}
</script>


<style>

@media screen and (min-width: 768px) and (max-width: 991px) {
.navbar.left .dropdown .dropbtn {
    
    font-size: 12px !important;
        padding: 14px 10px;

}
.navbar.left img {
    width: 100px;
}
.navbar.left a {
    font-size: 12px !important;
    padding: 14px 10px;
}
.footer-desk {
    float: left;
    width: 20%;
}
.footer-menu h2 {
    font-size: 13px;
}
.category-sec {
    float: left;
    width: calc( 100% - 20px);
    padding: 0px 10px;
}
.sidebar-sec {
    float: left;
    width: calc(20% - 10px);
    padding: 0px 5px;
    margin-top: 40px;
}

}
@media screen and (max-width: 767px){

 /* .mob-head-cont {
    position: fixed;
    height: 100%;
    width: 100%;
    display: block;
    top: 0;
    z-index: 1;
    background: rgba(0,0,0,.6) !important;
    left: 0;
    transition: all .5s;
    border: 0;
    bottom: 0;
}  */
.mobile-header a.single-menu {
    display: block;
    width: 100%;
    text-align: left;
}
.mobile-header .navbar.left {
    width: 100%;
    display: block;

}
.navbar-sec.desk-header {
    display: none;
}
.mobile-header .navbar.left {
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
    z-index: 9999999;
}
.mobile-header .navbar.left .dropdown {
    width: 100%;
    text-align: left;
}
.navbar-sec.mobile-header .menu-toggle img {
    width: 21px;
}
.mobile-header a.mob-logo img {
    width: 65px;
    margin-left: 25px;
}
.mobile-header-content {
    text-align: center;
    float: left;
    width: 100%;
    display: flex;
    align-items: center;
    margin-bottom: 0px;
    justify-content: unset;
        margin-left: 10px;
        margin-top: 15px;
            width: calc( 100% - 10px);
}
.mobile-header .header-menu-right {
    width: 100%;
    text-align: right;
}

.navbar-sec.desk-header {
    display: none !important;
}
.navbar-sec.mobile-header {
    display: block !important;
    padding-bottom: 10px;
}
.cat-product-sec {
    margin-top: 0 !important;
}
.navbar.left i.fas.fa-angle-down {
    float: right;
}
.mobile-header .navbar .dropdown .dropbtn {
    width: 100%;
    text-align: left;
}
.navbar .dropdown-content{
position: static;
}

}



.navbar a {
  float: left;
  font-size: 16px;
  color: #000;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}
.navbar-sec.mobile-header {
    display: none;
}

.dropdown {
  float: left;
  overflow: hidden;
}

.dropdown .dropbtn {
  font-size: 14px;
  border: none;
  outline: none;
  color: #303030;
  padding: 14px 16px;
  background-color: inherit;
  font-family: inherit;
  margin: 0;
}
.sticky{
  position: fixed;
  background: #FFF;
}

.navbar a:hover,
.dropdown:hover .dropbtn {
  background-color: transparent;
}

.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 1;
}

.dropdown-content a {
  float: none;
  color: #303030;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
  text-align: left;
}

.dropdown-content a:hover {
  background-color: #ddd;
}

.dropdown:hover .dropdown-content {
  display: block;
}
.header-menu-right ul li {
  list-style: none;
  display: inline-block;
  margin: 0px 15px;
}
.top-header {
  float: left;
  width: 100%;
  border-bottom: 1px solid #ccc;
     padding: 14px 0px;
    background-color: #9d8b61;
}
.navbar.left {
  width: 80%;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
/* .header-menu-right {
    float: left;
    width: 20%;
} */

.header-menu-right ul {
  padding: 0;
  margin: 0;
}
.header-menu-right ul li img {
  width: 20px;
}
.navbar.left a.single-menu {
  font-size: 14px;
  color: #303030;
}

.navbar-sec {
  text-align: center;
  float: left;
  width: 100%;
  display: flex;
  align-items: center;
  margin-bottom: 40px;
  justify-content: center;
  box-shadow: 0 4px 12px 0 rgb(0 0 0 / 5%);
}

</style>