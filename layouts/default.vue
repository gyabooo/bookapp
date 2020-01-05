<template>
  <div id="wrap" class="columns is-mobile">

    <header id="header" class="section column has-background-primary has-text-centered">
      <a href="/">
        <h1 class="title">本検索アプリ</h1>
        <h2 class="subtitle">国立国会図書館サーチAPI</h2>
      </a>
    </header>
    
    <div id="contents" class="section column">
      <nuxt />
    </div>

    <footer id="footer" class="section column footer has-background-grey-lighter">
    </footer>

  </div>
</template>

<style lang="scss" scoped>
#wrap {
  flex-direction: column;
  height: 100vh;
  width: 100vw;
}

#contents {
  flex-grow: 5;
}

</style>
