<template>
    <form class="ui form" @submit.prevent="save">
        <div class="field">
            <label>Name</lable>
            <input v-model="name">
        </div>
        <div class="field">
            <label>Description</lable>
            <input v-model="description">
        </div>
        <button class="ui submit blue button">Save</button>
        <div class="ui red button" @click="$emit('cancel')">Cancel</button>
    </form>
</template>

<script>
export default {
  props: ['value'],
  data: () => ({
    name: '',
    description: ''
  }),
  created () {
    this.name = this.value.name
    this.description = this.value.description
  },
  watch: {
    value () {
      console.log(this.value)
      this.name = this.value.name
      this.description = this.value.description
    }
  },
  methods: {
    save () {
      this.$emit('input', {
        name: this.name,
        description: this.description
      })
      this.$emit('save')
    }
  }
}
</script>