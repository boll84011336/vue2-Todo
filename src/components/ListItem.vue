<script setup>
	import { ref, watch } from 'vue';
	import ButtonModel from './ButtonModel.vue';

	const props = defineProps({
		dataList: {
			typeof: [],
			default: () => [],
		},
		editValue: {
			typeof: 'string',
			default: '',
		},
	});
	const emits = defineEmits(['edit', 'delete', 'checkEdit', 'cancel']);
	const editValue = ref();
	watch(
		() => props.editValue,
		(newVal) => {
			editValue.value = newVal;
		},
	);
</script>

<template>
	<ul class="flex flex-col w-full justify-center items-center mt-5">
		<li
			v-for="(item, index) in props.dataList"
			:key="item"
			class="flex flex-row items-center justify-between w-4/5 mb-3">
			<div class="w-2/4">
				<input
					v-if="item.editStatus"
					v-model="editValue"
					class="w-full" />
				<p
					v-else
					class="w-full">
					{{ item.text }}
				</p>
			</div>
			<div
				v-if="item.editStatus"
				class="flex flex-row">
				<ButtonModel
					:buttonText="'確認修改'"
					:buttonStyle="'btn-primary'"
					@click="emits('checkEdit', { index, editValue })"
					class="mx-5" />
				<ButtonModel
					:buttonText="'取消'"
					:buttonStyle="'btn-cancel'"
					@click="emits('cancel', index)" />
			</div>
			<div
				v-else
				class="flex flex-row">
				<ButtonModel
					:buttonText="'編輯'"
					:buttonStyle="'btn-edit'"
					@click="emits('edit', index)"
					class="mx-5" />
				<ButtonModel
					:buttonText="'刪除'"
					:buttonStyle="'btn-delete'"
					@click="emits('delete', index)" />
			</div>
		</li>
	</ul>
</template>
