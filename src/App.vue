<template>
  <div id="app">
    <div class="ui container grid">
      <div class="column">
        <h1 class="ui dividing header">
          <i class="cart icon"></i>
          <div class="content">
              Simple Vue Cart
            <div class="sub header">By Damien Castro</div>
          </div>
        </h1>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
