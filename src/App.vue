<template>
  <header>
    <router-link to="/">
      <h1><span>Vue</span>Movies</h1>
    </router-link>
  </header>
  <main>
    <router-view/>
  </main>
</template>

<style lang="scss">
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans',sans-serif;
  ::selection{
    background: transparentize(#42B883, 0.5);
  }
}
body{
  background-color: #35495E;
}
a{
  text-decoration: none;
}
header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px 16px;
  background-color: #2C3D4E;
  box-shadow: 0 0 6px rgba(0,0,0, 0.2);
}
h1{
  color: #fff;
  font-size: 28px;
  span{
    color: #42B883;
  }
}
</style>
