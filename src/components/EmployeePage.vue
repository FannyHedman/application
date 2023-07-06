<template>
  <div class="staff-container">
    <h2>MEET OUR PEOPLE</h2>
    <div class="grid-container">
      <div class="grid-content" v-for="employee in paginatedData" :key="employee.id">
        <img class="img" :src="employee.avatar" alt="Avatar" />
        <h4>{{ employee.first_name }} {{ employee.last_name }}</h4>
        <!-- <p> -->
        <a :href="'mailto:' + employee.email">{{ employee.email }}</a>
        <!-- </p> -->
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

<style scoped>
.staff-container h2 {
  text-align: center;
  margin-top: 50px;
  margin-bottom: 50px;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial,
    sans-serif;
}
.grid-container {
  margin: 0;
  position: relative;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  grid-gap: 10px;

  background-color: rgba(157, 217, 217, 0.3);
  border-top-left-radius: 800px;
  border-top-right-radius: 800px;
  border-bottom-right-radius: 800px;
  border-bottom-left-radius: 800px;
  padding: 100px;
}

.grid-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.grid-content a {
  text-decoration: none;
  color: black;
  background-color: rgba(255, 255, 255, 0.58);
  margin-bottom: 30px;
  border-radius: 8px;
  padding: 8px;
}

.grid-content h4 {
  font-weight: normal;
  font-size: 1.2rem;
  margin-bottom: 10px;
}

.button-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.button {
  margin: 5px;
  padding: 10px;
  padding-left: 20px;
  padding-right: 20px;
  border-radius: 10px;
  border-color: rgb(157, 217, 217);
  background-color: rgb(157, 217, 217);
  color: black;
  text-decoration: none;
}

.button:disabled {
  background-color: rgb(200, 210, 210);
  border-color: rgb(200, 210, 210);
}

.img {
  border-radius: 50%;
}
</style>
