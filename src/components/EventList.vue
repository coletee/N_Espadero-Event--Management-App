<template>
    <div>
        <h2 class="text-2xl font-semibold mb-4 text-center">List of All Events</h2>

        <div v-for="(event, index) in events" :key="event.id" class="bg-white shadow-md rounded-lg p-4 mb-4">

            <div v-if="editIndex !== index">
                <h5 class="text-lg font-medium">{{ event.name }}</h5>
                <p class="text-gray-600">{{ event.date }}</p>

                <div class="flex items-center space-x-2 mt-2">
                    <button @click="likeEvent(index)"
                        class="flex items-center bg-red-100 text-red-500 px-3 py-1 rounded-md hover:bg-red-200 transition">
                        ❤️ {{ event.likes }}
                    </button>

                    <button @click="startEdit(index)"
                        class="bg-blue-500 text-white px-3 py-1 rounded-md hover:bg-blue-600 transition">
                        Edit
                    </button>
                    <button @click="confirmRemoveEvent(index)"
                        class="bg-red-500 text-white px-3 py-1 rounded-md hover:bg-red-600 transition">
                        Remove
                    </button>
                </div>
            </div>


            <div v-else>
                <input v-model="editName"
                    class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 mb-2"
                    placeholder="Event Name" />
                <input v-model="editDate" type="date"
                    class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 mb-2" />
                <div class="flex space-x-2">
                    <button @click="confirmSaveEdit(index)"
                        class="bg-green-500 text-white px-3 py-1 rounded-md hover:bg-green-600 transition">
                        Save
                    </button>
                    <button @click="cancelEdit"
                        class="bg-gray-500 text-white px-3 py-1 rounded-md hover:bg-gray-600 transition">
                        Cancel
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Swal from 'sweetalert2'

export default {
    props: {
        events: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            editIndex: null,
            editName: '',
            editDate: ''
        }
    },
    methods: {
        likeEvent(index) {
            this.events[index].likes++
        },
        startEdit(index) {
            this.editIndex = index
            this.editName = this.events[index].name
            this.editDate = this.events[index].date
        },
        cancelEdit() {
            this.editIndex = null
        },
        confirmSaveEdit(index) {
            Swal.fire({
                title: 'Save Changes?',
                text: "Do you want to save the changes to this event?",
                icon: 'question',
                showCancelButton: true,
                confirmButtonColor: '#28a745',
                cancelButtonColor: '#6c757d',
                confirmButtonText: 'Yes, save it!'
            }).then((result) => {
                if (result.isConfirmed) {
                    this.saveEdit(index)
                }
            })
        },
        saveEdit(index) {
            this.events[index].name = this.editName
            this.events[index].date = this.editDate
            this.editIndex = null
            Swal.fire({
                icon: 'success',
                title: 'Event Updated',
                text: 'The event has been successfully updated.',
                timer: 2000,
                showConfirmButton: false
            })
        },
        confirmRemoveEvent(index) {
            Swal.fire({
                title: 'Are you sure?',
                text: "You won't be able to revert this!",
                icon: 'warning',
                showCancelButton: true,
                confirmButtonColor: '#d33',
                cancelButtonColor: '#3085d6',
                confirmButtonText: 'Yes, remove it!'
            }).then((result) => {
                if (result.isConfirmed) {
                    this.removeEvent(index)
                }
            })
        },
        removeEvent(index) {
            this.events.splice(index, 1)
            Swal.fire({
                icon: 'success',
                title: 'Event Removed',
                text: 'The event has been successfully removed.',
                timer: 2000,
                showConfirmButton: false
            })
        }
    }
}
</script>