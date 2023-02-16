<template>
  <div class="footer-sec desktop">
    <div class="footer-menu">

      <div v-for="(ulItem, index) in listArray" :key="index" class="footer-desk">
        <h2 @click="closeList(index)">{{ulItem.headingText}}  <i class="fas" :class=" currentIndex != index ? 'fa-plus' :  'fa-minus' "></i></h2>
        <ul>
        <li v-for="(listItem, index2) in ulItem.linkNames" :key="index2">
          <a href>{{ listItem }}</a>
        </li>
        <div class="Subscribe-box" v-if="ulItem.lastItme">
            <input type="text" />
            <button>{{ ulItem.btnText }}</button>
        </div>
        <div class="footer-social-icon" v-if="ulItem.lastItme">
            <span>{{ ulItem.spanText }}</span>
            <ul class="icon-list">
              <li>
                <a href="#">
                  <img alt="Vue" :src="require(`../assets/${ulItem.socialIcons}.png`)" />
                </a>
              </li>
            </ul>
        </div>
        </ul>      
      </div>

       <div v-for="(ulItem, index) in listArray" :key="index" class="footer-mobile">
        <h2 @click="closeList(index)">{{ulItem.headingText}}  <i class="fas" :class=" currentIndex != index ? 'fa-plus' :  'fa-minus' "></i></h2>
        <ul  v-if="currentIndex == index">
        <li v-for="(listItem, index2) in ulItem.linkNames" :key="index2">
          <a href>{{ listItem }}</a>
        </li>
        <div class="Subscribe-box" v-if="ulItem.lastItme">
            <input type="text" />
            <button>{{ ulItem.btnText }}</button>
        </div>
        <div class="footer-social-icon" v-if="ulItem.lastItme">
            <span>{{ ulItem.spanText }}</span>
            <ul class="icon-list" v-if="currentIndex == index" >
              <li>
                <a href="#">
                  <img alt="Vue" :src="require(`../assets/${ulItem.socialIcons}.png`)" />
                </a>
              </li>
            </ul>
        </div>
        </ul>      
      </div>
    </div>
  </div>

  

  
  
</template>

<script>
export default {
  name: "Footer-page",
data(){
  return{
   isHidden: false,
   isFooterLink: false,
   currentIndex: null,
   listArray:[
    {
      headingText: 'Shop',
      linkNames: ['Men', 'Women', 'Home','Sale','Collection'],
      isActive: false,
    },
    {
      headingText: 'Quick Links',
      linkNames: ['Ahujasons Export', 'Ahujasons Wholesale', 'Our Story','Legacy','Craftsman Ship','Our Store','Blogs'],
       isActive: false,
    },
     {
      headingText: 'Customer Service',
      linkNames: ['Terms and Condition', 'Shipping & Delivery', 'Return & Cancellation','Contact Us','Store Appointment'],
       isActive: false,
    },
     {
      headingText: 'My Profile',
      linkNames: ['My Account', 'Track Order', 'My Cart','Wishlist','Order History'],
       isActive: false,
    },
     {
      headingText: 'Sign Up and Save',
      linkNames: ['Subscribe to our newsletter and get 10% off your first purchase'],
      lastItme: true,
      btnText: 'Subscribe',
      spanText: 'GIVE US A FOLLOW',
      socialIcons: ['icon01'],
       isActive: false,
    },
  
   ]
  }
  

  },
  methods:{
     closeList(loopIndex) {
      // console.log('a' ,loopIndex );
      // this.listArray.map(key =>{
      //   console.log('key',key);
      //   if(key.isActive) key.isActive = false;
      // })
      // loopIndex.isActive = true;
      // console.log('b' ,this.currentIndex )
      if (this.currentIndex == loopIndex) {
        this.currentIndex = null;
      } else {
        this.currentIndex = loopIndex;
      }
    },

  }
  
 
};
 
</script>

<style>
@media screen and (max-width: 767px){
.top-header-left {
    text-align: left;
    width: 100%;
    float: left;
}
.top-header-left p {
 
    font-size: 10px;
   
}
 .top-header-right {
    display: none;
}
.footer-menu h2 i {
    float: right;
}
.footer-menu h2 i {
display: block !important;
}
.footer-menu {
    float: left !important;
    width: 100% !important;
    display: block !important;
    margin-bottom: 50px;
}
.footer-mobile {
    display: block !important;
}
.footer-desk {
    display: none;
}
.footer-sec {
       float: left !important;
    width: calc(100% - 20px) !important;
    width: -moz-calc(100% - 20px);
    padding: 0px 10px !important;
}
.footer-mobile {
    border-bottom: 1px solid #ccc;
    padding: 10px 0px;
}


}

.footer-menu h2 i {
display: none;
}
.footer-sec {
    float: left;
    width: calc(100% - 60px);
    width: -webkit-calc(100% - 60px);
    width: -moz-calc(100% - 60px);
    padding: 0px 30px;
}
.footer-menu {
    float: left;
    width: 100%;
    display: flex;
    justify-content: space-between;
}
.footer-menu h2 {
    font-size: 15px;
    text-transform: uppercase;
    text-align:left;
}
.footer-menu ul {
    padding: 0;
    margin: 0;
}
.footer-menu ul li {
    list-style: none;
    text-align: left;
    padding: 8px 0px;
}
.footer-menu ul li a {
    text-decoration: none;
    color: #222;
    font-size: 14px;
}
.footer-menu p {
    text-align: left;
    font-size: 14px;
    line-height: 18px;
    color: #303030;
}
.Subscribe-box input {
    border-left: 0;
    border-top: 0;
    border-right: 0;
    border-color: #303031;
    border-width: thin;
    border: 0;
}
.Subscribe-box button {
    background-color: transparent;
    border: 0;
    padding: 0;
}
.Subscribe-box {
    border-bottom: 1px solid #ccc;
    text-align: right;
    margin-bottom: 25px;
}
.footer-social-icon span {
   display: block;
    text-align: left;
    font-size: 14px;
    color: #303030;
    font-weight: 600;
        margin-bottom: 15px;
}
.footer-mobile {
    display: none;
}

</style>