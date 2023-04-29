<script>
  export default {
    props: ['event'],
      methods: {
        register() {
            this.$router.replace({
                name: 'EventDetails',
                params: { id: 3 }
            })
        }
      }
  }
</script>

<template>
    <p>Register for the event here</p>
    <button @click="register">Register</button>
</template>
