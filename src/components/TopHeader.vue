<template>
  <div class="top-header">
    <div class="top-header-cont">
         <div class="top-header-left">
        <p>COMPLIMENTARY GIFT BOX PACKING ON ALL PRE-PAID ORDERS</p>
         </div>
        <div class="top-header-right">
            <ul>
                <li>
                    <select id="country" name="country">
                        <option value="IN">IND</option>
                        <option value="AU">AUS</option>
                        <option value="US">USA</option>
                        <option value="EN">ENG</option>
                       
                    </select>
                </li>
                <li><a href="#">OUR STORES</a></li>
                <li><a href="#">MY ACCOUNT</a></li>
                <li><a href="#">BLOG</a></li>
            </ul>
        </div>
    </div>
  </div>
</template>

<script>
export default {
name:'TopHeaer'
}
</script>

<style>
.top-header-left {
    text-align: left;
    width: 50%;
    float: left;
}
body {
    margin: 0;
    padding: 0;
}
.top-header-left p {
    margin: 0;
    font-size: 12px;
    color: #fff;
    padding-left: 10px;
}
.top-header-right {
    float: right;
    width: 50%;
    text-align: right;
}
.top-header-right ul {
    padding: 0;
    margin: 0;
    list-style: none;
}
.top-header-right ul li {
    font-size: 14px;
}
.top-header-right ul li {
    display: inline-block;
    padding: 0px 10px;
}
.top-header-right ul li a {
    color: #fff;
    text-decoration: none;
    font-size: 12px;
}
.top-header-right select#country {
    border: 0;
}
</style>