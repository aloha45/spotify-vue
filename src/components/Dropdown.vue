<template>
	<div>
    <h1>Dropdown Component</h1>
		<select value="selectedValue" on:change="dropdownChange">
			{props.options.map((item, idx) => (
			<option v-for="item in options" :key="item.idx" value="item.id">
				{item.name}
			</option>
			))}
		</select>
	</div>
</template>

<script>
	export default {};
</script>

<style></style>
