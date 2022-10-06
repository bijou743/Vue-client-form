<script setup>
import { defineProps, ref, defineEmits, watch } from 'vue';

const emits = defineEmits(['update:modelValue']);

const { modelValue } = defineProps({
	modelValue: [String, Array],
	label: String,
	items: Array,
	required: {
		type: Boolean,
		default: false,
	},
	multiple: {
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
	<div class="field select">
		<label :class="'field__label' + (required ? ' required' : '')">
			{{ label }}
		</label>
		<select v-model="value" :multiple="multiple" :required="required">
			<option v-if="!multiple" value="">не выбран</option>
			<option v-for="(item, index) of items" :key="index">
				{{ item }}
			</option>
		</select>
	</div>
</template>

<style lang="scss">
.field.select {
	select {
		border: 1px solid $gray;
		padding: 6px 9px;
		border-radius: 5px;
		width: 100%;
		outline: none;
		line-height: 1.5;
		font-family: $fontFamily;
		font-size: $fontSize;
		transition: box-shadow 0.15s ease, border-color 0.15s ease;
		appearance: none;
		background-position: right 10px center;
		background-size: 16px 27px;
		background-image: url('../../assets/images/select.svg');
		background-repeat: no-repeat;

		&[multiple] {
			background-image: none;
			padding: 0;

			option {
				padding: 3px 9px;
			}
		}

		&:focus {
			box-shadow: 0 0 0 0.25rem $lightBlue;
			border-color: $lightBlue;
		}
	}
}
</style>
