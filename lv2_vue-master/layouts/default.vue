<template>
  <div class="container">
    <div class="header row">
        <header-index></header-index>
          <div class="content1">
            <menu-index/>
            <Nuxt />
        </div>
    </div>
  </div>
</template>
<script>
import Header from "../components/AppHeader/header.vue"
import Menu from "../components/AppMenu/menu.vue"
export default {
  components : {
    "header-index": Header,
    "menu-index": Menu,
  }
}
</script>
<style>
.content{
  width: 100%;
  height: auto;
  margin-top: 100px;
}
.header{
  display: flex;
  width: 100%;
  height: 100px;
}
.menua{
  width: 30%;
  margin-top: 20px;
  margin-left: -10px;
  height: 100px;
}
.content1{
  width: 100%;
  height: auto;
}
</style>
