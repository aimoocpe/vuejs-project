<template>
  <div>
    <input v-model="name">
    <br>
    <li><input type="checkbox" value="6" v-model="list"> 7 </li>
    <li><input type="checkbox" value="7" v-model="list"> 8 </li>
    <li><input type="checkbox" value="8" v-model="list"> 9 </li>
    <br>
    <hello :name="name" :list="list"></hello>
    <br>
    <button v-on:click="sayHello()">Say</button>
    
  </div>
</template>

<script>
import Hello from './components/Hello.vue'

export default {
  data () {
    return {
      name: '',
      list: [
        1, 2, 3, 4, 5
      ]
    }
  },
  components: {
    Hello
  },
  methods: {
    sayHello () {
      window.alert('Hi, ' + this.name)
    }
  }
}
</script>

