<template>
	<div>
		<div class="filter">
			<div>
				<select v-model="param">
					<option value=" ">Параметр</option>
					<option value="name" >Название</option>
					<option value="qvontity">Количество</option>
					<option value="distanse">Расстояние</option>
				</select>
			</div>
			<div>
				<select v-model="op"  placeholder="Значение">
					<option value=" ">Условие</option>
					<option value=">">Больше</option>
					<option value="<">Меньше</option>
					<option value="=">Равно</option>
				</select>
			</div>
		<div class="filter__param-form">
			<input type="text" placeholder="Значение" v-model="valueToFilter">
		</div>
		<button type="submit" @click="applyFilter">Применить</button>
		<button @click="reset" v-show="res">Сбросить</button>
	</div>
		<div style="height:800px">
			<div class="table">
				<div class="table__title">
					<div>Дата</div>
					<div>Название</div>
					<div>Количество</div>
					<div>Расстояние</div>
				</div>
				<div class="table__rec" v-for="(rec, index) in part" :key="index">
					<div>{{ rec.date }}</div>
					<div>{{ rec.name }}</div>
					<div>{{ rec.qvontity }}</div>
					<div>{{ rec.distanse }}</div>
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
			valueToFilter: '',
			param: ' ',
			op: ' ',
			res: false,
			resultFilter: [],
			schedule: [
				{date: 1, name: 132, qvontity: 8, distanse: 6000},
				{date: 2, name: 454, qvontity: 6, distanse: 5000},
				{date: 3, name: 344, qvontity: 2, distanse: 8000},
				{date: 4, name: 433, qvontity: 3, distanse: 3400},
				{date: 5, name: 622, qvontity: 4, distanse: 4500},
				{date: 6, name: 523, qvontity: 8, distanse: 6000},
				{date: 7, name: 622, qvontity: 4, distanse: 4500},
				{date: 8, name: 125, qvontity: 1, distanse: 6220},
				{date: 9, name: 132, qvontity: 8, distanse: 6000},
				{date: 10, name: 454, qvontity: 6, distanse: 5000},
				{date: 11, name: 344, qvontity: 2, distanse: 8000},
				{date: 12, name: 433, qvontity: 3, distanse: 3400},
				{date: 13, name: 622, qvontity: 4, distanse: 4500},
				{date: 14, name: 523, qvontity: 8, distanse: 6000},
				{date: 15, name: 622, qvontity: 4, distanse: 4500},
				{date: 16, name: 125, qvontity: 1, distanse: 6220},
				{date: 17, name: 132, qvontity: 8, distanse: 6000},
				{date: 18, name: 454, qvontity: 6, distanse: 5000},
				{date: 19, name: 344, qvontity: 2, distanse: 8000},
				{date: 20, name: 433, qvontity: 3, distanse: 3400},
				{date: 21, name: 623, qvontity: 4, distanse: 4500},
				{date: 22, name: 523, qvontity: 8, distanse: 6000},
				{date: 23, name: 622, qvontity: 3, distanse: 4500},
				{date: 24, name: 356, qvontity: 3, distanse: 6220},
				{date: 25, name: 132, qvontity: 4, distanse: 6220},
				{date: 26, name: 121, qvontity: 4, distanse: 6220},
				{date: 27, name: 245, qvontity: 7, distanse: 6220},
				{date: 28, name: 145, qvontity: 2, distanse: 6220},
				{date: 29, name: 325, qvontity: 6, distanse: 6220},
				{date: 30, name: 425, qvontity: 5, distanse: 6220},
				{date: 31, name: 155, qvontity: 3, distanse: 6220},
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
			if( this.valueToFilter === '' || this.param === ' ' || this.op === ' '){
				return alert('Фильтр не заполнен');
			};
			if (this.op === '<'){
				this.resultFilter = this.schedule.filter(item => item[this.param] < this.valueToFilter);
			} else if (this.op === '='){
				this.resultFilter = this.schedule.filter(item => +item[this.param] === +this.valueToFilter);
			} else if (this.op === '>'){
				this.resultFilter = this.schedule.filter(item =>item[this.param] > this.valueToFilter);
			};
			this.res = true;
		},
		reset(){
			this.resultFilter = this.schedule.filter(item => true);
			this.res = false;
		},
	}
}
</script>


<style>
.table{
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
}
.table__rec div{
	width: 200px;
	border: 1px solid black;
	border-top: 0px;
	border-right: 0px;
	text-align:start;
	padding-left: 15px;
}

.filter{
	width: 800px;
	justify-content: space-around;
	display: flex;
	margin-bottom: 40px;
}


</style>