<template>
  <div id="app">
    <top-menu></top-menu>
    <div class="ui container">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import TopMenu from './components/TopMenu'

export default {
  components: {
    TopMenu
  },
  head: {
    title: { inner: 'twitty eiei' },
    meta: [
      { name: 'viewport', content: 'width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1' }
    ]
  }
}
</script>