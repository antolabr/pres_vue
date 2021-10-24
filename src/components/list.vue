<template>
  <li>
    {{id}} : {{msg}} <button @click="remove()">X</button>
  </li>
</template>

<script>

export default {
  name: 'list',
  props: {
    msg: String,
    id: Number
  },
  methods: {
    remove() {
      //dans cette méthode, on émet un évènement remove vers le module parent
      this.$emit('remove')
    }
  }
}
</script>