<template>
  <v-container fluid>
    <v-row>
      <!-- Headers Form -->
      <v-col cols="6">
        <h2>Headers</h2>
        <br />
        <v-form>
          <table>
            <thead></thead>
            <tbody>
              <tr v-for="(header, index) in headers" :key="index">
                <td>
                  <v-combobox
                    v-model="header.key"
                    clearable
                    label="key"
                    :items="headerKeys"
                  ></v-combobox>
                </td>
                <td>
                  <v-text-field
                    v-model="header.value"
                    label="value"
                  ></v-text-field>
                </td>
                <td>
                  <v-icon @click="removeHeader(index)" color="error"
                    >mdi-close</v-icon
                  >
                </td>
              </tr>
            </tbody>
          </table>
          <v-icon @click="addHeader" color="primary">mdi-plus</v-icon>
        </v-form>
      </v-col>

      <!-- Body Form (Table) -->
      <v-col cols="6">
        <h2>Body</h2>
        <v-form>
          <v-radio-group v-model="selectedBodyType" row>
            <v-radio
              v-for="(type, index) in bodyTypes"
              :key="index"
              :label="type"
              :value="type"
            ></v-radio>
          </v-radio-group>

          <table v-if="selectedBodyType === 'Table'">
            <thead></thead>
            <tbody>
              <tr v-for="(body, index) in requestBody" :key="index">
                <td>
                  <v-text-field
                    v-model="body.key"
                    :label="'key'"
                  ></v-text-field>
                </td>
                <td>
                  <v-text-field
                    v-model="body.value"
                    :label="'value'"
                  ></v-text-field>
                </td>
                <td>
                  <v-icon @click="removeRequestBody(index)" color="error"
                    >mdi-close</v-icon
                  >
                </td>
              </tr>
            </tbody>
          </table>
          <v-icon
            v-if="selectedBodyType === 'Table'"
            @click="addBody"
            color="primary"
            >mdi-plus</v-icon
          >
          <v-textarea
            v-if="selectedBodyType === 'JSON'"
            v-model="bodyJSON"
            label="JSON Body"
          ></v-textarea>
        </v-form>
      </v-col>
      <v-col>
        <v-btn @click="sendData" color="primary">save params</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      headers: [{ key: '', value: '' }],
      bodyTypes: ['Table', 'JSON'], // Menambahkan pilihan Table
      selectedBodyType: 'Table', // Mengatur nilai default ke Table
      requestBody: [{ key: '', value: '' }],
      bodyJSON: '',
      headerKeys: [
        'Accept',
        'Accept-Charset',
        'Accept-Encoding',
        'Accept-Language',
        'apikey',
        'Authorization',
        'Cache-Control',
        'Content-Type',
        'User-Agent',
        'DNT',
        'From',
        'Host',
        'If-Match',
        'If-None-Match',
        'If-Modified-Since',
        'If-Unmodified-Since',
        'Max-Forwards',
        'Origin',
        'Pragma',
        'Prefer',
        'Proxy-Authorization',
        'Range',
        'Referer',
        'TE',
        'Upgrade',
        'Via',
        'Warning',
        'X-Requested-With',
        'X-HTTP-Method-Override',
        'X-Forwarded-For',
        'X-Forwarded-Host',
        'X-Forwarded-Proto',
      ],
    }
  },
  methods: {
    addHeader() {
      this.headers.push({ key: '', value: '' })
    },
    removeHeader(index) {
      this.headers.splice(index, 1)
    },
    sendData() {
      // Mengubah format headers
      const formattedHeaders = this.headers.map((header) => ({
        [header.key]: header.value,
      }))
      // Mengubah format requestBody
      const formattedRequestBody = this.requestBody.map((body) => ({
        [body.key]: body.value,
      }))
      this.$emit('data-sent', {
        headers: formattedHeaders,
        selectedBodyType: this.selectedBodyType,
        requestBody: formattedRequestBody, // Mengirim requestBody dalam format yang diinginkan
        bodyJSON: this.bodyJSON, // Menambahkan JSON Body
      })
    },
    addBody() {
      this.requestBody.push({ key: '', value: '' })
    },
    removeRequestBody(index) {
      this.requestBody.splice(index, 1)
    },
  },
}
</script>
