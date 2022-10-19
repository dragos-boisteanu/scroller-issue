<template>
<div style="padding: 5px" class="item">

	<div class="avatar">
		<img
		:key="item.avatar"
		:src="item.avatar"
		alt="avatar"
		class="image"
		>
	</div>

	<div class="details">
		<div class="name">
			{{item.name}}
		</div>
		<div class="content">
			{{item.content}}
		</div>
	</div>

</div>


</template>

<script>

	export default {
		props: {
			item: {type: Object, required: true}
		}
	}
</script>

<style scoped>
.item {
	display: flex;
	align-items: flex-start;
	column-gap: 16px;
	padding: 8px 16px;
	font-size: 12px;
}


.avatar {
  flex: auto 0 0;
  width: 32px;
  height: 32px;
  border-radius: 50%;
}
.avatar .image {
  max-width: 100%;
  max-height: 100%;
  border-radius: 50%;
}

.details {
	text-align: left;
}

.name {
	font-weight: bold;
}

.content {
	text-align: left;

}
</style>