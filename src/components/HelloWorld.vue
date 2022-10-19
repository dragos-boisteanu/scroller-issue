<template>
  <div class="hello">
		<DynamicScroller
          id="virtualList"
          ref="dynamicScrollerRef"
          :items="items"
					key-field="seq"
          :min-item-size="10"
						style="height: 100%;
						width: 500px;
						border: 1px solid black;
            overflow-y: auto;
            overflow-x: hidden;
            will-change: transform;
            padding: 0;
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
								:item="item"
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
