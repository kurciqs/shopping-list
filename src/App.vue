<template>
  
  <h2>Nova polozka</h2>
  <input v-model="input">
	<button @click="addItem()">Add to list</button>
  
  <h2>Polozky</h2>
	<ul>	
    <li v-for="item in validItems" :key="`item-${item.id}`">
      <span @click="deleteItem(item)" style="margin-right: 15px"> X </span>
      {{item.text}}
    </li>
	</ul>

  <h2>Zmazane Polozky</h2>
	<ul>	
    <li v-for="item in deletedItems" :key="`item-${item.id}`">
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
			input: '',
			items: []
		}
	},
  methods: {
		addItem() {
			this.items.push({
				id: this.items.length + 1,
				text: this.input,
				is_deleted: false
			})
			this.input = ''
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

</style>
