<template>
  <div>
    <div class="grid-container">
      <div class="grid-content" v-for="employee in paginatedData" :key="employee.id">
        <img class="img" :src="employee.avatar" alt="Avatar" />
        <p>{{ employee.first_name }} {{ employee.last_name }}</p>
        <p>
          <a class="link" :href="'mailto:' + employee.email">{{ employee.email }}</a>
        </p>
      </div>
    </div>
    <div class="button-container">
      <button
        class="button"
        v-for="pageNumber in totalPages"
        :key="pageNumber"
        @click="fetchEmployees(pageNumber)"
        :disabled="currentPage === pageNumber"
      >
        {{ pageNumber }}
      </button>
    </div>
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

<style>
.grid-container {
  margin-top: 10vh;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  grid-gap: 10px;
}

.grid-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.button-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.button {
  margin: 5px;
}

.img {
  border-radius: 50%;
}

.link {
  color: black;
}
</style>
