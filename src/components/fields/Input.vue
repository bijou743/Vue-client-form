<script setup>
import { defineProps, ref, defineEmits, watch } from 'vue';

const emits = defineEmits(['update:modelValue']);

const { modelValue } = defineProps({
	modelValue: String,
	placeholder: String,
	label: String,
	pattern: {
		type: String,
		default: null,
	},
	size: {
		type: Number,
		default: null,
	},
	required: {
		type: Boolean,
		default: false,
	},
	type: {
		type: String,
		default: 'text',
		validator: (val) => {
			return [
				'text',
				'textarea',
				'password',
				'tel',
				'email',
				'search',
				'date',
			].includes(val);
		},
	},
});

const value = ref(modelValue);

watch(value, () => {
	emits('update:modelValue', value);
});
</script>

<template>
	<div class="input field">
		<label :class="'field__label' + (required ? ' required' : '')">
			{{ label }}
		</label>

		<input
			v-if="type !== 'textarea'"
			:type="type"
			:placeholder="placeholder"
			v-model="value"
			:required="required"
			:pattern="pattern"
			:size="size"
		/>

		<textarea
			v-else
			:placeholder="placeholder"
			v-model="value"
			:required="required"
		></textarea>
	</div>
</template>

<style lang="scss">
.field.input {
	input,
	textarea {
		border: 1px solid $gray;
		padding: 6px 12px;
		border-radius: 5px;
		line-height: 1.5;
		outline: none;
		width: 100%;
		font-family: $fontFamily;
		font-size: $fontSize;
		transition: box-shadow 0.15s ease, border-color 0.15s ease;

		&:focus {
			box-shadow: 0 0 0 0.25rem $lightBlue;
			border-color: $lightBlue;
		}
	}
}
</style>
