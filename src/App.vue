<template>
  <br>
  <h3 class="font-weight-bold text-h4 ">
    Название веб-приложения
  </h3>
  <nav>
    <router-link to="/">Главная</router-link> |
    <router-link to="/model1">Модель 1</router-link> |
    <router-link to="/model2">Модель 2</router-link> |
    <router-link to="/model3">Модель 3</router-link> 
  </nav>
  <router-view></router-view>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
