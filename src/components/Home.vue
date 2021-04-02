<template id="main-page">
  <v-ons-page>
    <v-ons-toolbar>
      <div class="center">Tong thu chi: {{handleSummary || 0}}$</div>
    </v-ons-toolbar>

    <MainInformation :info="info" />
    <div style="text-align: center">
      <span style="text-align: center">
        <v-ons-button @click="handleShowSpending"> 
          <span > Them Chi tieu </span>
        </v-ons-button>
      </span>
      <span style="text-align: center">
        <v-ons-button class="button button--outline" @click="handleShowIncome" > 
          <span> Them Thu nhap </span>
        </v-ons-button>
      </span>
    </div>

    <v-ons-alert-dialog
      cancelable
      :visible.sync="showSpending"
      animation="default"
    >
      <AddSpending :showSpending="showSpending" @addSpending="addSpending" />
    </v-ons-alert-dialog>

    <v-ons-alert-dialog
      cancelable
      :visible.sync="showIncome"
      animation="default"
    >
      <AddIncome :showIncome="showIncome" @addIncome="addIncome" />
    </v-ons-alert-dialog>

  </v-ons-page>
</template>

<script>
import AddSpending from './AddSpending.vue'
import AddIncome from './AddIncome.vue'
import MainInformation from './MainInformation.vue'

export default {
  name: 'Home',
  components: {
    MainInformation,
    AddSpending,
    AddIncome
  },
  props: {
    msg: String
  },
  data () {
    return {
      summary: 0,
      showSpending: false,
      showIncome: false,
      resetDialog: false,
      info: []
    }
  },
  methods: {
    closeDialogSpending ()  {
      this.showSpending = false
    },
    closeDialogIncome ()  {
      this.showIncome = false
    },
    addSpending(data){
      var info = this.info
      info.push({
        id: info[info.length - 1] ? info[info.length - 1].id + 1 : 0,
        money: data.money,
        content: data.content,
        type: 0
      })
      this.closeDialogSpending()
    },
    addIncome(data){
      var info = this.info
      info.push({
        id: info[info.length - 1] ? info[info.length - 1].id + 1 : 0,
        money: data.money,
        content: data.content,
        type: 1
      })
      this.closeDialogIncome()
    },
    handleShowSpending(){
      this.closeDialogIncome()
      this.showSpending = true
    },
    handleShowIncome(){
      this.closeDialogSpending()
      this.showIncome = true
    }
  },
  computed: {
    handleSummary(){
      return this.info.reduce((sum, item) => item.type == 0 ? sum - parseInt(item.money) : sum + parseInt(item.money), 0)
    }
  }
}
</script>

<style scoped>
  span:nth-child(1){
    margin-right: 5px;
  }
</style>