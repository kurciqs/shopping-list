<template>
  
  <h2>Nova polozka</h2>
  <input v-model="newItemName">
	<button @click="addItem()">Add to list</button>
  
  <h2>Polozky</h2>
	<ul>	
    <li v-for="item in validItems" :key="item.id">
      <span @click="deleteItem(item)" class="item"> X </span>
      {{item.text}}
    </li>
	</ul>

  <h2>Zmazane Polozky</h2>
	<ul>	
    <li v-for="item in deletedItems" :key="item.id">
      <s>
        {{item.text}}
      </s>
    </li>
	</ul>

</template>

<script>
export default {
	data() {
		return {
			newItemName: '',
			items: []
		}
	},
  methods: {
		addItem() {
			this.items.push({
				id: this.items.length + 1,
				text: this.newItemName,
				is_deleted: false
			})
			this.newItemName = ''
		},
    deleteItem(item) {
			item.is_deleted = true
		}
	},
  computed: {
		validItems() {
			return this.items.filter(item => !item.is_deleted)
		},

		deletedItems() {
			return this.items.filter(item => item.is_deleted)
		}
	}
}
</script>

<style>
.item {
	margin-right: 15px
}
</style>
