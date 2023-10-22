<template>
  <v-container fluid>
    <v-row justify="center">
      <!-- HTTP Method Dropdown -->
      <v-col cols="auto">
        <v-combobox
          v-model="selectedMethod"
          :items="httpMethods"
          label="HTTP Method"
          outlined
          autocomplete
        ></v-combobox>
      </v-col>

      <!-- URL Input -->
      <v-col cols="6">
        <v-text-field v-model="url" label="URL" outlined></v-text-field>
      </v-col>

      <!-- Send Button -->
      <v-col>
        <v-btn
          class="my-2"
          @click="sendRequest"
          prepend-icon="$vuetify"
          variant="tonal"
        >
          <v-icon icon="$send"></v-icon>Send</v-btn
        >
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      selectedMethod: 'get',
      url: '',
      httpMethods: ['get', 'post', 'put', 'delete'],
    }
  },
  methods: {
    sendRequest() {
      this.$emit('request-sent', {
        method: this.selectedMethod,
        url: this.url,
      })
    },
  },
}
</script>
