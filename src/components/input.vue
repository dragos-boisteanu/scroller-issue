<template>
	<div class="textarea__container">
		<textarea v-model="text"/>
		<div contenteditable class="editable__div"/>
		<div class="action__bnts">
			<button @click="close">Cancel</button>
			<button @click="save">Save</button>
		</div>
	</div>

</template>

<script>


export default {
	props: {
		content: {type: String, rquired: true}
	},
	data() {
		return {
			text: ""
		}
	},
	mounted() {
		this.text = this.content
	},

	methods: {
		close() {
			this.$emit('close')
		},
		save() {
			this.$emit('save', this.text)
			this.close()
		}
	}
}

</script>

<style scoped>
.editable__div {
	border: 1px solid black;
	padding: 4px;
}
.textarea__container {
	width: 100%;
}
textarea {
	width: 95%;
	resize: vertical;
}
.action__btns {
	display: flex;
	align-items: center;
	justify-content: flex-end;
	column-gap: 8px;
}

</style>