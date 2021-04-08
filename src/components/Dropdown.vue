<template>
  		<div>
			<select
				value={props.selectedValue}
				onChange={dropdownChange}>
				{props.options.map((item, idx) => (
					<option key={idx} value={item.id}>
						{item.name}
					</option>
				))}
			</select>
		</div>
</template>

<script>
export default {

}
</script>

<style>

</style>