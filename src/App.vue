<template>
  <div>
    <div class="ui menu">
      <router-link to="/" class="item">Home</router-link>
      <router-link to="/about" class="item">About</router-link>
      <div class="right menu">
        <router-link to="/signin" class="item">Sign In</router-link>
      </div>
    </div>
    <br>
    <router-view></router-view>
  </div>
</template>

<script>
export default{

}
</script>