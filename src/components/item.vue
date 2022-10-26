<template>
<div style="padding: 5px" class="item">
	<div class="avatar">
		<img
		:key="source.avatar"
		:src="source.avatar"
		alt="avatar"
		class="image"
		>
	</div>

	<div class="details">
		<div class="name">
			{{source.name}}
		</div>
		<textareaComp v-if="idState.showEdit" :content="source.content" @close="toggleEdit" @save="saveEdit"/>
		<div v-else class="content">
			{{source.content}}
		</div>
		<button @click="toggleEdit">Edit</button>
	</div>
</div>
</template>

<script>
import { IdState } from 'vue-virtual-scroller'
import textareaComp from './input.vue'
export default {
	mixins: [
		IdState({
			// You can customize this
			idProp: vm => vm.source.seq,
		}),
	],
	components: {
		textareaComp
	},
	props: {
		source: {type: Object, required: true}
	},

	idState () {
		return {
			showEdit: false,
		}
	},

	methods: {
		toggleEdit() {
			this.idState.showEdit = !this.idState.showEdit
		},
		saveEdit(content) {
			this.$parent.$parent.$emit("updateContent", {
				seq: this.source.seq,
				content,
			});
			this.$emit('updateContent', {
				seq: this.source.seq,
				content,
			})
		}
	}
}
</script>

<style scoped>
.item {
	width: 100%;
	display: flex;
	align-items: flex-start;
	column-gap: 16px;
	padding: 8px 16px;
	font-size: 12px;
	padding: 16px;
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
	flex: 1 1 auto;
}

.name {
	font-weight: bold;
}

.content {
	text-align: left;

}
</style>