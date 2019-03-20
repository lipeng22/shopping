<template>
  <div id="app">
    <div id="nav">
      <router-link to="/" v-show="false">Home</router-link>
      <router-link to="/about" v-show="false">About</router-link>
      <router-link to="/counter" v-show="false">Counter</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
</style>
