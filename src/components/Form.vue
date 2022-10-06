<script>
import { defineComponent, reactive, ref } from 'vue';
import Input from './fields/Input.vue';
import Radio from './fields/Radio.vue';
import Select from './fields/Select.vue';
import Checkbox from './fields/Checkbox.vue';

export default defineComponent({
	name: 'Form',

	components: {
		Input,
		Radio,
		Select,
		Checkbox,
	},

	setup() {
		const data = {
			sex: ['мужской', 'женский'],
			groups: ['VIP', 'Проблемные', 'ОМС'],
			doctors: ['Иванов', 'Захаров', 'Чернашева'],
			documentType: [
				'Паспорт',
				'Свидетельство о рождении',
				'Вод. удостоверение',
			],
		};

		const document = {
			type: data.documentType[0],
			series: '',
			number: '',
			issuedBy: '',
			issueDate: null,
		};

		const address = {
			index: '',
			country: '',
			region: '',
			city: '',
			street: '',
			house: '',
		};

		const client = reactive({
			lastName: '',
			name: '',
			middleName: '',
			birthday: null,
			phone: '',
			sex: data.sex[0],
			group: [],
			doctor: '',
			sms: false,
			document: document,
			address: address,
		});

		let success = ref(false);

		const submit = () => {
			console.log('test');
			success.value = true;
		};

		return { client, data, submit, success };
	},
});
</script>

<template>
	<div class="form">
		<form @submit.prevent.stop="submit">
			<h2>Клиент</h2>
			<Input
				v-model="client.lastName"
				type="text"
				placeholder="Фамилия"
				label="Фамилия"
				:required="true"
			/>

			<Input
				v-model="client.name"
				type="text"
				placeholder="Имя"
				label="Имя"
				:required="true"
			/>

			<Input
				v-model="client.middleName"
				type="text"
				placeholder="Отчество, если есть"
				label="Отчество"
			/>

			<Input
				v-model="client.birthday"
				type="date"
				label="Дата рождения"
				:required="true"
			/>

			<Input
				v-model="client.phone"
				type="tel"
				placeholder="В формате +71234567890"
				label="Телефон"
				:required="true"
				:size="11"
				pattern="\+7[0-9]{10}"
			/>

			<Radio v-model="client.sex" label="Пол" :items="data.sex" name="sex" />

			<Select
				v-model="client.group"
				label="Группа клиентов"
				:items="data.groups"
				:required="true"
				:multiple="true"
			/>

			<Select
				v-model="client.doctor"
				label="Лечащий врач"
				:items="data.doctors"
			/>

			<Checkbox v-model="client.sms" label="Отправлять СМС" id="sms" />

			<hr />

			<h2>Адрес</h2>

			<Input
				v-model="client.address.index"
				type="text"
				placeholder="Индекс"
				label="Индекс"
			/>

			<Input
				v-model="client.address.country"
				type="text"
				placeholder="Страна"
				label="Страна"
			/>

			<Input
				v-model="client.address.region"
				type="text"
				placeholder="Регион"
				label="Регион"
			/>

			<Input
				v-model="client.address.city"
				type="text"
				placeholder="Город"
				label="Город"
				:required="true"
			/>

			<Input
				v-model="client.address.street"
				type="text"
				placeholder="Улица"
				label="Улица"
			/>

			<Input
				v-model="client.address.house"
				type="text"
				placeholder="Дом"
				label="Дом"
			/>

			<hr />

			<h2>Паспорт</h2>

			<Select
				v-model="client.document.type"
				label="Тип документа"
				:items="data.documentType"
				:required="true"
			/>

			<div class="row">
				<Input
					v-model="client.document.series"
					type="text"
					placeholder="Серия"
					label="Серия"
				/>

				<Input
					v-model="client.document.number"
					type="text"
					placeholder="Номер"
					label="Номер"
				/>
			</div>

			<Input
				v-model="client.document.issuedBy"
				type="textarea"
				placeholder="Кем выдан"
				label="Кем выдан"
			/>

			<Input
				v-model="client.document.issueDate"
				type="date"
				label="Дата выдачи"
				:required="true"
			/>

			<hr />

			<div v-if="success" class="form__success">
				Новый клиент успешно создан!
			</div>
			<button class="btn">Сохранить</button>
		</form>
	</div>
</template>

<style lang="scss">
.form {
	max-width: 600px;
	margin: 0 auto;

	.btn {
		width: 100%;
	}

	.row {
		display: grid;
		grid-auto-flow: column;
		gap: 0 30px;
	}

	&__success {
		color: $green;
		margin-bottom: 15px;
		font-weight: 600;
	}
}
</style>
