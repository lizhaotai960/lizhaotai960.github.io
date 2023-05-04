<template>
  <div class="common-layout">
    <el-container>
      <el-header class="header">Header</el-header>
      <el-container>
        <el-aside class="aside">Aside
          <p><router-link to="/carousel">Carousel</router-link></p>
          <p><router-link to="/calendar">Calendar</router-link></p>
        </el-aside>
        <el-main class="main">Main</el-main>
      </el-container>
    </el-container>
  </div>
</template>


<style lang="less" scoped>
.header {
  background-color: rgb(127, 9, 133);
}

.aside {
  width: 20%;
  height: autos;
  background-color: pink;
}

.main {
  background-color: blue;
}
</style>
