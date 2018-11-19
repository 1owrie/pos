<template>
  <div class="left-nav">
      <ul>
          <li>
               <i class="icon iconfont icon-shouyintai"></i>
               <p>收银</p>
          </li>
          <li>
               <i class="icon iconfont icon-dianpu1"></i>
               <p>店铺</p>
          </li>
          <li>
               <i class="icon iconfont icon-shangpin"></i>
               <p>商品</p>
          </li>
          <li>
               <i class="icon iconfont icon-huiyuan"></i>
               <p>会员</p>
          </li>
          <li>
               <i class="icon iconfont icon-guanli"></i>
               <p>统计</p>
          </li>
      </ul>
  </div>
</template>
<script>
export default {
  name: "leftNav"
};
</script>
<style>
* {
  padding: 0px;
  margin: 0px;
}
.left-nav {
  float: left;
  height: 100%;
  width: 5%;
  background-color: #1d8ce0;
  color: aliceblue;
  font-size: 14px;
}
li {
  list-style: none;
  padding: 15px;
  border-bottom: 1px solid #20a0ff;
}
.iconfont {
  font-size: 28px;
}
p {
  margin-top: 5px;
  cursor: pointer;
}
</style>
