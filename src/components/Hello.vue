<template>
  <div>
    <p v-if="name && name !== 'aimoocpe'">Hi , {{name}}</p>
    <p v-else-if="name == 'aimoocpe'">XD</p>
    <p v-else>No Data</p>
    <li v-for="x in list">{{ x }}</li>
  </div>
</template>

<script>
export default {
  props: {
    name: {
      required: true
    },
    list: {
      type: Array
    }
  }
}
</script>

