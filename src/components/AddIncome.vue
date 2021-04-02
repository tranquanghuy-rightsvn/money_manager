<template>
	<div>
    <div class="alert-dialog-title">Them thu nhap</div>
    <div class="alert-dialog-content">
      <v-ons-list>
        <v-ons-list-item>
          <div class="center">
						<v-ons-input placeholder="So tien " float
              v-model="money"
              type="number"
            >
          </v-ons-input>
				</div>
        </v-ons-list-item>

				<v-ons-list-item>
						<div class="center">
						<v-ons-input placeholder="Noi dung" float
              v-model="content"
            >
            </v-ons-input>
          </div>
        </v-ons-list-item>
      </v-ons-list>      
    </div>
    <div class="alert-dialog-footer">
      <v-ons-button class="alert-dialog-button" @click="addIncome">Them</v-ons-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AddIncome',
  props: {
    showIncome: Boolean
  },
  data(){
    return {
      money: '',
      content: ''
    }
  },
  methods: {
    addIncome(){
      var data = {
        money: this.money,
        content: this.content
      }

      if(data.money && data.content){
				this.$emit('addIncome', data)
				this.resetDialog()
      }
    },
		resetDialog(){
			this.money = '',
			this.content = ''
    }
  }
}
</script>

<style scoped>
	div{
		text-align: center;
	}
	
</style>