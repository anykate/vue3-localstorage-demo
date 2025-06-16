<script setup>
import { reactive } from 'vue'

const form = reactive({
	name: '',
	email: '',
	message: '',
})

const emit = defineEmits(['submit-form'])

const handleSubmit = () => {
	if (form.name && form.email && form.message) {
		emit('submit-form', { ...form })
		form.name = ''
		form.email = ''
		form.message = ''
	} else {
		alert('Please fill in all fields.')
	}
}
</script>

<template>
	<form
		class="w-full p-8 bg-white shadow-xl rounded-2xl space-y-6 transition-all duration-300 h-fit"
		@submit.prevent="handleSubmit"
	>
		<h2 class="text-2xl font-semibold text-gray-800 text-center">Contact Form</h2>
		<div>
			<label
				for="name"
				class="block text-sm font-medium text-gray-700 mb-1"
				>Full Name</label
			>
			<input
				id="name"
				v-model="form.name"
				type="text"
				placeholder="John Doe"
				class="w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500"
				required
			/>
		</div>
		<div>
			<label
				for="email"
				class="block text-sm font-medium text-gray-700 mb-1"
				>Email Address</label
			>
			<input
				id="email"
				v-model="form.email"
				type="email"
				placeholder="john@example.com"
				class="w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500"
				required
			/>
		</div>
		<div>
			<label
				for="message"
				class="block text-sm font-medium text-gray-700 mb-1"
				>Message</label
			>
			<textarea
				id="message"
				v-model="form.message"
				placeholder="Your message here..."
				class="w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500"
				rows="4"
				required
			>
			</textarea>
		</div>
		<button
			type="submit"
			class="w-full bg-blue-600 text-white py-2 rounded-lg font-semibold hover:bg-blue-700 transition duration-300"
		>
			Submit
		</button>
	</form>
</template>
