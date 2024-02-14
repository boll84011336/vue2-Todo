<script setup>
	defineProps({
		buttonText: {
			typeof: 'string',
			default: '編輯',
		},
		buttonStyle: {
			typeof: 'string',
			default: 'btn-primary' | 'btn-cancel' | 'btn-delete' | 'btn-edit',
		},
	});
</script>

<template>
	<button
		:class="buttonStyle"
		class="btn">
		{{ buttonText }}
	</button>
</template>
