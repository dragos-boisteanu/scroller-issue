<template>
  <div class="hello">
		<virtual-list style="height: 500px; overflow-y: auto; order: 1px solid black"
      :data-key="'seq'"
      :data-sources="items"
      :data-component="itemComponent"
			@updateContent="updateContent"
    />
  </div>
</template>

<script>
import VirtualList from 'vue-virtual-scroll-list'
import { faker } from '@faker-js/faker'
import item from "./item.vue"

export default {
	components: {
		VirtualList,
	},
  name: 'HelloWorld',
  props: {
    msg: String
  },
	data() {
		return {
			itemComponent: item
		}

	},
	created() {
		this.items = [];

		for(let i = 0; i < 10000; i++) {
			const item = {
				id: null,
				seq: i,
				name: faker.name.fullName(),
				content:  faker.lorem.text(),
				avatar: faker.internet.avatar(),
			}

			this.items.push(item);
		}
	},
	methods: {
		updateContent(data) {

			const itemIndex = this.items.findIndex(item => item.seq === data.seq)
			console.log('updateContent', data)
			if(itemIndex > -1) {
				this.$set(this.items[itemIndex], 'content', data.content)
			}
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">


.hello {
	height:  500px;
	margin-top: 100px;
	padding-top: 24px;
	border-top: 1px solid black;
}




</style>
