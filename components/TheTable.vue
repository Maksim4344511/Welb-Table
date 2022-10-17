<template>
	<div>
		<div class="filter">
			<div>
				<select v-model="param">
					<option value=" ">Параметр</option>
					<option value="name" >Название</option>
					<option value="quontity">Количество</option>
					<option value="distance">Расстояние</option>
				</select>
			</div>
			<div>
				<select v-model="op" placeholder="Значение">
					<option value=" ">Условие</option>
					<option value=">">Больше</option>
					<option value="<">Меньше</option>
					<option value="=">Равно</option>
					<option value="contains">Содержит</option>
				</select>
			</div>
		<div class="filter__param-form">
			Значения для фильтрации:<input type="text" v-model="valueToFilter">
		</div>
		<button type="submit" @click="applyFilter">Применить</button>
		<button @click="reset" v-show="res">Сбросить</button>
	</div>
		<div  class="table">
			<div class="table__wrap">
				<div class="table__title">
					<div>Дата</div>
					<div>Название</div>
					<div>Количество</div>
					<div>Расстояние</div>
				</div>
				<div class="table__rec" v-for="(rec, index) in part" :key="index">
					<div>{{ rec.date }}</div>
					<div>{{ rec.name }}</div>
					<div>{{ rec.quontity }}</div>
					<div>{{ rec.distance }}</div>
				</div>
			</div>
		</div>
		<button @click="back">назад</button> {{ pagin / 10 + 1 }} <button @click="next">вперед</button>
	</div>
</template>


<script>
export default {
	data() {
		return {
			pagin: 0,
			valueToFilter: ' ',
			param: ' ',
			op: ' ',
			res: false,
			resultFilter: [],
			schedule: [
				{date: '1.01.2022', name: 'AA', quontity: 8, distance: 6000},
				{date: '2.01.2022', name: 'aa', quontity: 6, distance: 5000},
				{date: '3.01.2022', name: 'Ab', quontity: 2, distance: 8000},
				{date: '4.01.2022', name: 'ab', quontity: 3, distance: 3400},
				{date: '5.01.2022', name: 'BB', quontity: 4, distance: 4500},
				{date: '6.01.2022', name: 'bb', quontity: 8, distance: 6000},
				{date: '7.01.2022', name: 'bA', quontity: 4, distance: 4500},
				{date: '8.01.2022', name: 'cc', quontity: 1, distance: 6220},
				{date: '9.01.2022', name: 'dd', quontity: 8, distance: 6000},
				{date: '10.01.2022', name: 'ff', quontity: 6, distance: 5000},
				{date: '11.01.2022', name: 'cc', quontity: 2, distance: 8000},
				{date: '12.01.2022', name: 'dd', quontity: 3, distance: 3400},
				{date: '13.01.2022', name: 'dd', quontity: 4, distance: 4500},
				{date: '14.01.2022', name: 'aa', quontity: 4, distance: 4500},
				{date: '16.01.2022', name: 'ff', quontity: 1, distance: 6220},
				{date: '17.01.2022', name: 'ff', quontity: 8, distance: 6000},
				{date: '18.01.2022', name: 'ff', quontity: 6, distance: 5000},
				{date: '19.01.2022', name: 'cc', quontity: 2, distance: 8000},
				{date: '20.01.2022', name: 'dd', quontity: 3, distance: 3400},
				{date: '21.01.2022', name: 'gg', quontity: 4, distance: 4500},
				{date: '22.01.2022', name: 'gg', quontity: 8, distance: 6000},
				{date: '23.01.2022', name: 'gg', quontity: 3, distance: 4500},
				{date: '24.01.2022', name: 'gg', quontity: 3, distance: 6220},
				{date: '25.01.2022', name: 'gg', quontity: 4, distance: 6220},
				{date: '26.01.2022', name: 'ff', quontity: 4, distance: 6220},
				{date: '27.01.2022', name: 'rr', quontity: 7, distance: 6220},
				{date: '28.01.2022', name: 'rr', quontity: 2, distance: 6220},
				{date: '29.01.2022', name: 'aa', quontity: 6, distance: 6220},
				{date: '30.01.2022', name: 'aa', quontity: 5, distance: 6220},
				{date: '31.01.2022', name: 'asdfgh', quontity: 3, distance: 6220},
			],
		}
	},
	created (){
		this.reset();
	},
	computed:{
		part() {
			let part= [];
			for (let i = this.pagin; i < this.pagin + 10; i++ ) {
				if (this.resultFilter[i]){
					part.push(this.resultFilter[i]);
				};
			};
			return part;
		},
	},

	methods: {
		back(){
			if (this.pagin >= 10) {
				this.pagin -= 10;
			};
		},
		next(){
			if (this.pagin < this.resultFilter.length - 10) {
				this.pagin += 10;
			};
		},
		applyFilter(){
			if( this.valueToFilter === ' ' || this.param === ' ' || this.op === ' '){
				return alert('Фильтр не заполнен');
			};
			if (this.op === '<'){
				this.resultFilter = this.schedule.filter(item => +item[this.param] < +this.valueToFilter);
			} else if (this.op === '='){
				this.resultFilter = this.schedule.filter(item => +item[this.param] === +this.valueToFilter);
			} else if (this.op === '>'){
				this.resultFilter = this.schedule.filter(item =>+item[this.param] > +this.valueToFilter);
			}else if (this.op === 'contains'){
				this.resultFilter = this.schedule.filter(item => (item[this.param]).toString().includes(this.valueToFilter));
			};
			this.res = true;
			this.pagin = 0;
		},

		reset(){
			this.resultFilter = this.schedule.filter(item => true);
			this.res = false;
			this.valueToFilter = ' ';
			this.param = ' ';
			this.op = ' ';
		},
	}
}
</script>


<style>
.table{
	height: 500px;
}

.table__wrap{
	width: 800px;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	border-right: 1px solid black;
}
.table__title{
	width: 800px;
	display: flex;
	justify-content: space-between;
	font-size: 28px;
}
.table__rec{
	width: 800px;
	display: flex;
	justify-content: space-between;
	font-size: 22px;
}
.table__title div{
	width: 200px;
	border: 1px solid black;
	border-right: 0px;
	text-align: start;
	padding-left: 15px;
	text-align: center;
}
.table__rec div{
	width: 200px;
	border: 1px solid black;
	border-top: 0px;
	border-right: 0px;
	text-align:start;
	padding-left: 15px;
	text-align: center;
}
.filter{
	width: 800px;
	justify-content: space-around;
	display: flex;
	margin-bottom: 40px;
}
</style>
