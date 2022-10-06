<script setup>
import { defineProps, ref, defineEmits, watch } from 'vue';

const emits = defineEmits(['update:modelValue']);

const { modelValue } = defineProps({
	modelValue: Boolean,
	label: String,
	id: String,
});

const value = ref(modelValue);

watch(value, () => {
	emits('update:modelValue', value);
});
</script>

<template>
	<div class="field checkbox">
		<input type="checkbox" v-model="value" :id="id" />
		<label :for="id">{{ label }}</label>
	</div>
</template>

<style lang="scss">
.field.checkbox {
	display: flex;
	flex-direction: row;
	align-items: center;

	input {
		appearance: none;
		width: 18px;
		height: 18px;
		background-repeat: no-repeat;
		background-position: center;
		border: 1px solid rgba(0, 0, 0, 0.25);
		border-radius: 3px;
		background-color: #fff;
		outline: none;
		transition: box-shadow 0.15s ease, border-color 0.15s ease;

		&:focus {
			box-shadow: 0 0 0 0.25rem $lightBlue;
			border-color: $lightBlue;
		}

		&:checked {
			background-color: #0d6efd;
			border-color: #0d6efd;
			background-image: url('../../assets/images/checkbox-checked.svg');
		}
	}
}
</style>
