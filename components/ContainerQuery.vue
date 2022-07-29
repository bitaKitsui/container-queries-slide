<template>
  <div class="wrapper">
    <aside class="sidebar"></aside>
    <main class="container">
      <div class="card" />
      <div class="card" />
      <div class="card" />
      <div class="card" />
      <div class="card" />
      <div class="card" />
      <div class="card" />
      <div class="card" />
      <div class="card" />
    </main>
  </div>
</template>

<style>
.wrapper {
  display: flex;
  flex-wrap: wrap;
  height: 85%;
}

.sidebar {
  width: 150px;
  background-color: gray;
}

.container {
  width: calc(100% - 150px);
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  contain: layout inline-size;
}

.card {
  background-color: darkgray;
  width: calc(100% / 4);
  height: 100px;
  margin: 10px;
}

@container (max-width: 1000px) {
  .card {
    width: calc(100% / 5);
  }
}

/* slidevのスタイル上書き */

@media (min-width: 768px) {
  .container {
    max-width: 100%;
  }
}

@media (min-width: 640px) {
  .container {
    max-width: 100%;
  }
}
</style>