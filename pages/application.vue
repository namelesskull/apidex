<template>
  <div>
    <input-request @request-sent="handleRequest" />
    <request-params @data-sent="handleData" />
    <v-divider class="my-4"></v-divider>
    <response-here
      v-if="errorMessage === null && responseData.status === null"
    />
    <response-json
      v-else-if="responseData.status !== null && errorMessage.message === null"
      :responseData="responseData"
    />
    <response-error
      v-else-if="errorMessage.message !== null"
      :errorMessage="errorMessage"
    />
  </div>
</template>

<script>
import InputRequest from '../components/InputRequest.vue'
import RequestParams from '../components/RequestParams.vue'
import ResponseError from '../components/ResponseError.vue'
import ResponseHere from '../components/ResponseHere.vue'
import ResponseJson from '../components/ResponseJson.vue'

export default {
  components: {
    InputRequest,
    RequestParams,
    ResponseJson,
    ResponseError,
    ResponseHere,
    ResponseError,
  },
  data() {
    return {
      requestData: {
        headers: [],
        selectedBodyType: '',
        requestBody: [],
        bodyJSON: '',
        method: '',
        url: '',
      },
      responseData: {
        // Inisialisasi responseData sebagai objek kosong
        data: null,
        status: null,
        method: null,
      },
      errorMessage: {
        message: null,
      },
    }
  },
  methods: {
    handleData(data) {
      this.requestData.headers = data.headers
      this.requestData.selectedBodyType = data.selectedBodyType
      this.requestData.requestBody = data.requestBody
      this.requestData.bodyJSON = data.bodyJSON
    },
    async handleRequest(data) {
      this.requestData.method = data.method
      this.requestData.url = data.url

      try {
        const headers = this.requestData.headers
        const body = this.requestData.requestBody

        const resultHeader = {}
        const resultBody = {}

        headers.forEach((item) => {
          for (const key in item) {
            resultHeader[key] = item[key]
          }
        })

        body.forEach((item) => {
          for (const key in item) {
            resultBody[key] = item[key]
          }
        })

        const response = await this.$axios.request({
          method: this.requestData.method,
          url: this.requestData.url,
          headers: resultHeader,
          data:
            this.requestData.selectedBodyType === 'JSON'
              ? this.requestData.bodyJSON
              : resultBody,
        })

        this.responseData.data = response.data
        this.responseData.status = response.status
        this.responseData.method = this.requestData.method
        this.errorMessage.message = null
      } catch (error) {
        console.log('Error', error)
        this.errorMessage.message = error
      }
    },
  },
}
</script>
