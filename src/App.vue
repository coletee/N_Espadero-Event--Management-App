<template>
  <div class="flex items-center justify-center min-h-screen bg-blue-100">
    <div class="container mt-5">
      <h1 class="mb-4 text-center text-3xl font-bold">Event Management App</h1>

  
      <div v-if="!isLoggedIn" class="bg-white p-6 rounded-lg shadow-md">
        <h2 class="text-xl font-semibold mb-4 text-center">Login</h2>
        <form @submit.prevent="login">
          <div class="mb-4">
            <input
              v-model="username"
              type="text"
              placeholder="Username"
              class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              required
            />
          </div>
          <div class="mb-4">
            <input
              v-model="password"
              type="password"
              placeholder="Password"
              class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
              required
            />
          </div>
          <button
            type="submit"
            class="w-full bg-green-500 text-white py-2 px-4 rounded-md hover:bg-green-600 transition duration-200"
          >
            Login
          </button>
        </form>
      </div>
 
      <div v-else>
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-xl font-semibold">Welcome, {{ currentUser }}</h2>
          <button
            @click="logout"
            class="bg-red-500 text-white px-4 py-2 rounded-md hover:bg-red-600 transition"
          >
            Logout
          </button>
        </div>
        <AddEvent :events="events" />
        <EventList :events="events" />
      </div>
    </div>
  </div>
</template>

<script>
import AddEvent from './components/AddEvent.vue'
import EventList from './components/EventList.vue'
import eventsData from './data/events.json'

export default {
  components: {
    AddEvent,
    EventList
  },
  data() {
    return {
      events: eventsData.map(event => ({
        ...event,
        likes: 0
      })),
      isLoggedIn: false,
      username: '',
      password: '',
      currentUser: '',
      credentials: {
        username: 'colete_dev_pcd',
        password: 'cbms2025'
      }
    }
  },
  methods: {
    login() {
      if (
        this.username === this.credentials.username &&
        this.password === this.credentials.password
      ) {
        this.isLoggedIn = true
        this.currentUser = this.username
        this.username = ''
        this.password = ''
      } else {
        alert('Invalid username or password')
      }
    },
    logout() {
      this.isLoggedIn = false
      this.currentUser = ''
    }
  }
}
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
