<template>
    <div class="bg-white shadow-md rounded-lg p-6 mb-6">
        <h2 class="text-xl font-semibold mb-4">Create New Event</h2>
        <form @submit.prevent="addNewEvent">
            <div class="mb-4">
                <input v-model="name"
                    class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                    placeholder="Event Name" required />
            </div>
            <div class="mb-4">
                <input v-model="date" type="date"
                    class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                    required />
            </div>
            <button type="submit"
                class="w-full bg-green-500 text-white py-2 px-4 rounded-md hover:bg-green-600 transition duration-200">
                Add Event
            </button>
        </form>
    </div>
</template>

<script>
export default {
    props: ['events'],
    data() {
        return {
            name: '',
            date: ''
        }
    },
    methods: {
        addNewEvent() {
            const newEvent = {
                id: Date.now(),
                name: this.name,
                date: this.date,
                likes: 0
            }
            this.events.push(newEvent)
            this.name = ''
            this.date = ''
        }
    }
}
</script>