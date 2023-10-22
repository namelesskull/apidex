<template>
  <div>
    <v-alert type="error" outlined>
      <strong>Error:</strong> {{ errorMessage.message }}
    </v-alert>
  </div>
</template>

<script>
export default {
  props: {
    errorMessage: {
      type: Object,
      required: true,
    },
  },
  mounted() {
    const message = this.errorMessage
    console.log(message)
  },
}
</script>
