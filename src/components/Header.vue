<template>
    <div class="navbar">
      <div class="navbar_inner clearfix">
           <router-link :to="{name:'root'}"  class="navbar_brand">
               <img src="../assets/cnodejs_light.svg">
           </router-link>
          <ul class="clearfix">
            <li><a href="#">首页</a></li>
            <li><a href="#">新手入门</a></li>
            <li><a href="#">API</a></li>
            <li><a href="#">关于</a></li>
            <li><a href="#">注册</a></li>
            <li><a href="#">登陆</a></li>
          </ul>
      </div>
    </div>
</template>

<script>
    export default {
        name: "Header"
    }
</script>

<style scoped>
.clearfix::after{
  display: block;
  content: '';
  clear:both;
}
.navbar{
  width: 100%;
  background-color: #444;
}
.navbar_inner{
  width: 90%;
  margin: auto;
  padding: 8px 5px;
}
.navbar_brand{
  width: 120px;
  height: 34px;
  display: block;
  float: left;
}
.navbar_brand>img{
  width: 100%;
}
.navbar_inner>ul{
  list-style: none;
  float: right;
}
.navbar_inner>ul>li{
  float:left;
  color:#fff;

}
.navbar_inner>ul>li>a{
  float:left;
  color:#ccc;
  text-decoration: none;
  font-size:13px;
  padding: 8px 16px;
}
.navbar_inner>ul>li>a:hover{
  color:#fff;
}
</style>
