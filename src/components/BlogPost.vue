<script setup>
	// const props = defineProps(['title', 'description'])
	defineProps({
		title: String,
		id: Number,
		body: {
			type: String,
			default: 'Void',
		}
	})
	const emit = defineEmits(['changeFavorite'])
</script>

<template>
	<div class="card mt-4 mb-4">
		<div class="card-body">
			<h5 class="cart-title">{{ id }} - {{ title }}</h5>
			<p>{{ body }}</p>
			<button 
			  @click="emit('changeFavorite', title)"
			  class="btn btn-outline-primary border-0"
			>
			  ♥️
			</button>
		</div>
	</div>
</template>

<style scoped lang="css">
  .card-body {
		position: relative;
	}
	.card-title {
		max-width: 90%;
	}
	.card-body .btn {
		position: absolute;
		top: .5rem;
		right: .5rem;
	}
</style>