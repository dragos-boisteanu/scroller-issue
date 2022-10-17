<template>
  <div class="hello">
		<DynamicScroller
          id="virtualList"
          ref="dynamicScrollerRef"
          :items="items"
					key-field="seq"
          :min-item-size="10"
						style="height: 500px;
						width: 300px;
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
              :size-dependencies="[item.seq, item.content]"
              :data-index="index"
            >
              <div style="padding: 5px">
								<div>
									<span>{{item.id}}</span> - <span>{{ item.seq}}</span>
								</div>
								<div>
									{{item.content}}
								</div>
							</div>
            </DynamicScrollerItem>
          </template>
        </DynamicScroller>
  </div>
</template>

<script>
import 'vue-virtual-scroller/dist/vue-virtual-scroller.css'
import { DynamicScroller, DynamicScrollerItem } from "vue-virtual-scroller"


export default {
	components: {
		DynamicScroller,
		DynamicScrollerItem
	},
  name: 'HelloWorld',
  props: {
    msg: String
  },
	created() {
		this.items = [];

		for(let i = 0; i < 1000; i++) {
			const item = {
				id: null,
				seq: i,
				content: (Math.random() + 1).toString(36).substring(4)
			}

			this.items.push(item);
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
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
	max-height:  500px;
}


</style>
