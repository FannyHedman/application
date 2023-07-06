<template>
  <div>
    <div v-for="employee in paginatedData" :key="employee.id">
      <img :src="employee.avatar" alt="Avatar"/>
      <p>{{ employee.first_name }} {{ employee.last_name }}</p>
      <p>
        <a :href="'mailto:' + employee.email">{{ employee.email }}</a>
      </p>
    </div>

    <button
      v-for="pageNumber in totalPages"
      :key="pageNumber"
      @click="fetchEmployees(pageNumber)"
      :disabled="currentPage === pageNumber"
    >
      {{ pageNumber }}
    </button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      jsonData: [],
      currentPage: 1,
      totalPages: 0
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get('https://reqres.in/api/users')
        this.jsonData = response.data.data
        this.totalPages = response.data.total_pages
      } catch (error) {
        console.error(error)
      }
    },
    async fetchEmployees(page) {
      try {
        const response = await axios.get(`https://reqres.in/api/users?page=${page}`)
        this.jsonData = response.data.data
        this.currentPage = page
      } catch (error) {
        console.error(error)
      }
    }
  },
  computed: {
    paginatedData() {
      return this.jsonData
    }
  }
}
</script>
