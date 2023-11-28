<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'


</script>
<style>
#hotelsys-nav {
  position: fixed;
  left: 0;
  top: 0;
  width: 8vw;
  height: 100vh;
  background-color: rgba(220, 245, 240, 0.523);
  display: flex;
  /* 添加 Flex 布局 */
  flex-direction: column;
  /* 设置为纵向排列 */
}

.nav-item-div {
  text-align: center;
  width: 100%;
  flex: 1;
  /* 让每个 div 占据相同的大小 */
}

.nav-item-div a {
  display: flex;
  align-items: center;
  height: 5vh;
  width: 100%;
  text-decoration: none;
  color:  rgb(114, 154, 118);
}
</style>
<template>
  <div id="hotelsys-nav" class="bg-info">
    <nav class="navbar navbar-expand-lg navbar-light">
      <div class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav"
        aria-expanded="false" aria-label="Toggle navigation">
        <router-link class="navbar-brand" to="/">Home</router-link>
      </div>
      <div class="collapse navbar-collapse" id="navbarNav">
        <div class="nav-item-div">
          <router-link to="/register">登记</router-link>
        </div>
        <div class="nav-item-div">
          <router-link to="/room">房间</router-link>
        </div>

        <div class="nav-item-div">
          <router-link to="/customer">住客</router-link>
        </div>

      </div>
    </nav>
  </div>
  <div class="container mt-4">
    <router-view></router-view>
  </div>
</template>

