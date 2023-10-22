<template>
  <v-container fluid>
    <!-- Recent API Requests -->
    <v-divider class="my-4"></v-divider>
    <h2>Recent API Requests</h2>
    <br />
    <v-list>
      <v-list-item v-for="request in recentRequests" :key="request.id">
        <v-list-item-title>{{ request.name }}</v-list-item-title>
        <v-list-item-subtitle>{{ request.date }}</v-list-item-subtitle>
      </v-list-item>
    </v-list>
    <!-- Getting Started and Tips & Tricks -->
    <v-divider class="my-4"></v-divider>
    <br />
    <h2>Getting Started</h2>
    <p>
      Learn how to get started with Apidex and simplify your API management.
    </p>
    <h2>Tips & Tricks</h2>
    <p>
      Discover tips for using Apidex and enhancing your API testing workflow.
    </p>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      quickLinks: [
        {
          title: 'apidex Quick Start Guide',
          description: 'Start your experience with creating an account',
          url: '#',
        },
        {
          title: 'apidex Documentation',
          description: 'Comprehensive documentation for Vuetify.',
          url: 'https://vuetifyjs.com/',
        },
      ],
      recentRequests: [
        {
          id: 1,
          name: 'GET /api/users',
          date: '2 days ago',
        },
        {
          id: 2,
          name: 'POST /api/products',
          date: '3 days ago',
        },
        {
          id: 3,
          name: 'PUT /api/settings',
          date: '4 days ago',
        },
      ],
    }
  },
}
</script>
