<template>
	<div class="filter">
		<div>
			<select>
				<option autofocus>Параметр</option>
				<option value="1">Название</option>
				<option value="2">Количество</option>
				<option value="3">Расстояние</option>
			</select>
		</div>
		<div>
			<select>
				<option autofocus>Условие</option>
				<option value="1">Больше</option>
				<option value="2">Меньше</option>
				<option value="3">Равно</option>
			</select>
		</div>
		<div class="search-form">
			<input type="text" placeholder="Значение">
		</div>
		<button type="submit">Применить</button>
	</div>
</template>



<style>
.filter{
	width: 800px;
	justify-content: space-around;
	display: flex;
	margin-bottom: 40px;
}
</style>