<template>
	<div>
		 <TheFilter />
		<div style="height:800px">
			<div class="table">
				<div class="table__title">
					<div>Дата</div>
					<div>Название</div>
					<div>Количество</div>
					<div>Расстояние</div>
				</div>
				<div class="table__rec" v-for="(rec, index) in part" :key="index" >
					<div>{{ rec.date }}</div>
					<div>{{ rec.name }}</div>
					<div>{{ rec.qvontity }}</div>
					<div>{{ rec.distanse }}</div>
				</div>
			</div>
		</div>
		<button @click="back">назад</button> {{ pagin / 2 + 1 }} <button @click="next">вперед</button>
	</div>
</template>


<script>
export default {
	data() {
		return {
			pagin: 0,
			part:[],
			schedule: [
				{date: 1, name: 1, qvontity: 8, distanse: 600},
				{date: 2, name: 2, qvontity: 6, distanse: 500},
				{date: 3, name: 3, qvontity: 2, distanse: 800},
				{date: 4, name: 4, qvontity: 3, distanse: 340},
				{date: 5, name: 6, qvontity: 4, distanse: 450},
				{date: 6, name: 5, qvontity: 8, distanse: 600},
				{date: 7, name: 6, qvontity: 4, distanse: 450},
				{date: 8, name: 15, qvontity: 1, distanse: 622},
			],
		}
	},
	created (){
		this.group();
	},
	
	methods: {
		group() {
			this.part = [];
			for (let i = this.pagin; i <= (this.pagin + 1); i++ ) {
				this.part.push(this.schedule[i]);
			}
		},

		back(){
			if(this.pagin >= 2) {
				this.pagin -= 2;
				this.group();
			};
		},
		next(){
			if(this.pagin < this.schedule.length -2) {
				this.pagin += 2;
				this.group();
			};
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
	border-collapse: collapse;
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



</style>