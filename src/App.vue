 <template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  background-color: #ddfff6;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
  background-color: rgb(232, 255, 249);
}

#nav a.router-link-exact-active {
  color: #42b983;
  background-color: rgb(232, 255, 249);
}
</style>
