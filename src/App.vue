<script setup>
	import { ref } from 'vue';
	import ListItem from './components/ListItem.vue';
	import ButtonModel from './components/ButtonModel.vue';
	const todoDataList = ref([]);
	const newList = ref('');
	const editListItem = ref('');
	function addList() {
		if (newList.value.length === 0) {
			return alert('新增待辦事項不可空白');
		}
		todoDataList.value.push({
			text: newList.value,
			editStatus: false,
		});
		newList.value = '';
	}
	function handlerEdit(key) {
		todoDataList.value[key].editStatus = true;
		editListItem.value = todoDataList.value[key].text;
	}
	function handlerEditCheck(param) {
		if (param.editValue.length === 0) {
			return alert('修改待辦事項不可空白');
		}
		todoDataList.value[param.index].editStatus = false;
		todoDataList.value[param.index].text = param.editValue;
	}
	function handlerDelete(key) {
		todoDataList.value.splice(key, 1);
	}
	function handlerCancel(key) {
		todoDataList.value[key].editStatus = false;
	}
</script>

<template>
	<div class="w-3/4 h-full mx-auto mt-5">
		<div class="flex flex-row w-full items-center justify-center">
			<label
				for="addList"
				class="text-2xl">
				新增待辦事項
			</label>
			<input
				v-model="newList"
				type="text"
				id="addList"
				class="ml-7 border-2 mr-5" />
			<ButtonModel
				:buttonText="'新增'"
				:buttonStyle="'btn-primary'"
				@click="addList"
				@keyup.enter="addList" />
		</div>
		<ListItem
			:dataList="todoDataList"
			:editValue="editListItem"
			@edit="handlerEdit"
			@checkEdit="handlerEditCheck"
			@delete="handlerDelete"
			@cancel="handlerCancel"
			class="mx-auto" />
	</div>
</template>
