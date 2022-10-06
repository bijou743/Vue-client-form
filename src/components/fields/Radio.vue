<script setup>
import { defineProps, ref, defineEmits, watch } from 'vue';

const emits = defineEmits(['update:modelValue']);

const { modelValue } = defineProps({
	modelValue: String,
	label: String,
	items: Array,
	name: String,
	required: {
		type: Boolean,
		default: false,
	},
});

const value = ref(modelValue);

watch(value, () => {
	emits('update:modelValue', value);
});
</script>

<template>
	<div class="field radio">
		<label :class="'field__label' + (required ? ' required' : '')">
			{{ label }}
		</label>
		<div v-for="(item, index) of items" :key="index" class="radio__wrapper">
			<input
				type="radio"
				:id="item + index"
				:name="name"
				v-model="value"
				:value="item"
			/>
			<label :for="item + index">{{ item }}</label>
		</div>
	</div>
</template>

<style lang="scss">
.field.radio {
	display: flex;

	.radio__wrapper {
		display: flex;
		align-items: center;
		gap: 5px;

		input {
			appearance: none;
			width: 18px;
			height: 18px;
			background-repeat: no-repeat;
			background-position: center;
			background-size: 8px;
			border: 1px solid rgba(0, 0, 0, 0.25);
			border-radius: 50%;
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
				background-image: url('../../assets/images/radio-btn-circle.svg');
			}
		}
	}
}
</style>
