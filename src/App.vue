<template>
  <el-container id="app">
    <el-header id="topInfo" height=50px style="padding: 10px">
      COVID-19 Dashboard by the Center for Systems Science and Engineering (CSSE) at Johns Hopkins University (JHU)
    </el-header>
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div> -->
    <el-main style="padding: 10px">
      <router-view/>
    </el-main>
  </el-container>
</template>

<style>
#app {
  /* font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50; */
  height: 100%;
}

#topInfo {
  background-color: #e4f5ef;
  text-align: center;
  /* border: 2px solid black; */
  border-radius: 20px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
  margin-top: 10px;
  margin-left: 8px;
  margin-right: 8px;
}

.el-main {
  height: 100%
}
</style>
