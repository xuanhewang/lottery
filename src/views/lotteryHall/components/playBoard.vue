<template>
	<div class="playBoard">
		<selectNumber ref="selectNumber" :key="Math.random()" :single="item.titleName == '包胆'" v-for="item in playBoardData" v-if="item.type == 'number'" :titleName="item.titleName" :numberData="item.numberData" v-model="selectedData"></selectNumber>
		<textareaNumber :titleName="item.titleName" v-else v-model="selectedData" @input="textareaChange"></textareaNumber>
	</div>
</template>

<script>
	import selectNumber from './selectNumber.vue'
	import textareaNumber from './textareaNumber.vue'

	export default {
		components: {
			selectNumber,
			textareaNumber
		},

		props: ['playBoardData'],
		data() {
			return {
				selectedData: [],
				emitData: []
			}
		},
		methods: {
      textareaChange() {
        // this.$emit('change', this.selectedData)
      },
      resetSelected() {
        this.playBoardData.forEach(v => {
//        	console.log(v)
          v.numberData.forEach(v1 => {
            v1.checked = false
          })
        })
      }
    },
		watch: {
			'playBoardData': function (n) {
				this.emitData = []
				this.playBoardData.forEach(i => {
					this.emitData.push({
						label: i.titleName,
						data: []
					})
				})
        this.$emit('playBoardType', this.playBoardData[0].type)
			},
			'selectedData': function (n) {
				this.emitData.forEach(i => {
					if(i.label == n.titleName) {
						i.data = n.data
					}
				})
				this.emitData.forEach((v, i) => {
					if(v.data.length > 0 && v.data[0].checked == false) {
						v.data = []
					}
				})
				this.$emit('change', this.emitData)

			}
		},
		destroyed() {
		  this.resetSelected()
    }
	}
</script>
