<script setup>
import ContactForm from '@/components/ContactForm.vue'
import { TrashIcon } from '@heroicons/vue/24/solid'
import { ref, onMounted } from 'vue'

const contacts = ref([])

const handleSubmit = (formData) => {
	contacts.value.push(formData)
	updateLocalStorage()
}

const deleteContact = (index) => {
	contacts.value.splice(index, 1)
	updateLocalStorage()
}

const updateLocalStorage = () => {
	localStorage.setItem('contacts', JSON.stringify(contacts.value))
}

onMounted(() => {
	const savedContacts = localStorage.getItem('contacts')
	if (savedContacts) {
		contacts.value = JSON.parse(savedContacts)
	}
})
</script>

<template>
	<div class="min-h-screen bg-gray-50 py-12 px-4 sm:px-6 lg:px-8">
		<div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-2 gap-10">
			<!-- Left: Contact Form-->
			<ContactForm @submit-form="handleSubmit" />
			<!-- Right: Contacts List -->
			<div class="bg-white p-8 rounded-2xl shadow-xl transition-all duration-300">
				<h2 class="text-2xl font-semibold text-gray-800 mb-6">Contacts List</h2>
				<div
					v-if="contacts.length"
					class="space-y-4"
				>
					<div
						v-for="(contact, index) in contacts"
						:key="index"
						class="relative p-5 bg-gray-100 rounded-xl shadow hover:shadow-md transition duration-300 group"
					>
						<div class="space-y-1">
							<p class="text-base text-gray-800"><strong>Name:</strong> {{ contact.name }}</p>
							<p class="text-base text-gray-800"><strong>Email:</strong> {{ contact.email }}</p>
							<p class="text-base text-gray-800"><strong>Message:</strong> {{ contact.message }}</p>
						</div>

						<button
							class="absolute top-3 right-3 text-red-500 hover:text-red-600 transition duration-200"
							title="Delete Contact"
							@click="deleteContact(index)"
						>
							<TrashIcon class="w-5 h-5" />
						</button>
					</div>
				</div>

				<p
					v-else
					class="text-gray-700 text-md mt-4"
				>
					No contacts yet. Please submit the form to add a contact.
				</p>
			</div>
		</div>
	</div>
</template>

<style></style>
