<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <h2>Response</h2>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-alert :type="alertType" outlined>
          <strong>Status Code:</strong> {{ responseData.status }}
        </v-alert>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-alert :type="alertType" outlined>
          <strong>Request Method:</strong> {{ responseData.method }}
        </v-alert>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-alert :type="alertType" outlined>
          <strong>Response Body:</strong>
          <pre style="white-space: pre-wrap">{{ responseData.data }}</pre>
        </v-alert>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-btn @click="copyToClipboard" color="primary">Copy</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  props: {
    responseData: {
      type: Object,
      required: true,
    },
  },
  computed: {
    alertType() {
      return this.responseData.status >= 200 && this.responseData.status < 300
        ? 'success'
        : 'error'
    },
  },
  methods: {
    copyToClipboard() {
      // Implement logic to copy responseData.data to clipboard here
      // You can use the Clipboard API or a third-party library for clipboard functionality
    },
  },
}
</script>
