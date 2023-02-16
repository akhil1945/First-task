<template>
  <div class="pagination-sec">
   <label>{{step}}</label>
    <button class="btn btn-red btn-next" @click="increment"
         >
         nwxt
</button>
  
  </div>
  
</template>

<script>
export default {
name:'Pagination-page',

data() { 
    return { 
      count: 0 
    } 
  },
  // computed: {
  //   stepLabel({ count }) {
  //     return count === 3 ? 'Kirim' : 'Selanjutnya';
  //   },
  //   shouldStopIncrement({ count }) {
  //     return count >= 3;
  //   }
  // },
  methods: {
    increment() {
      this.count++;
    }
  }
}




</script>

<style>
.pagination {
  display: inline-block;
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
.pagination button:focus {
    background-color: rebeccapurple;
    color: #fff;
    font-size: 14px;
    border-color: rebeccapurple;
}
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

}
</style>
