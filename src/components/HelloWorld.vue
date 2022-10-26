<template>
  <div class="hello">
		<textarea style="resize: vertical"/>
		<DynamicScroller
          id="virtualList"
          ref="dynamicScrollerRef"
          :items="items"
					key-field="seq"
          :min-item-size="10"
						style="height: 100%;
						width: 100;
						border: 1px solid black;
            overflow-y: auto;
            overflow-x: hidden;
            will-change: transform;

          "
        >
          <template #default="{ item, index, active }">
            <DynamicScrollerItem
              :item="item"
              :active="active"
              :size-dependencies="[item.content]"
              :data-index="index"
            >
              <item
								:source="item"
								@updateContent="updateContent"
							/>
            </DynamicScrollerItem>
          </template>
        </DynamicScroller>
  </div>
</template>

<script>
import 'vue-virtual-scroller/dist/vue-virtual-scroller.css'
import { DynamicScroller, DynamicScrollerItem } from "vue-virtual-scroller"
import { faker } from '@faker-js/faker'
import item from "./item.vue"

export default {
	components: {
		item,
		DynamicScroller,
		DynamicScrollerItem
	},
  name: 'HelloWorld',
  props: {
    msg: String
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
body,
html {
	height: 100vh;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.hello {
	height:  500px
}




</style>
