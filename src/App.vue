<template>
  <div class="wrapper">
    <div class="main-info">
      <h1>Telegram Bots</h1>
      <button class="btn" @click="popupState = true">Create bot</button>
    </div>

    <div class="bots-container">
      <ul class="all-bots" v-if="botsArray.length">
        <li class="bot-item" v-for="item in botsArray" :key="item.id">
          <h3 class="bot-title" @click="editBot(item)">{{item.name}}</h3>
          <button class="btn red" @click="deleteBot(item.id)">Delete</button> 
        </li>
      </ul>
      <p style="text-align: center" v-else> Create your first bot </p>
    </div>
  </div>

  <CreateBotForm 
    v-if="popupState" 
    @close="popupState = false" 
    @array="botsArray.push($event)"
  />
  
  <EditBotForm 
    v-if="popupEdit" 
    :name="edit.name"
    :date="edit.date"
    :description="edit.description"
    :image="edit.image"
    :id="edit.id"
    :key="edit.id"
    @close="popupEdit = false"
    @editedBot="edited($event)"
  />

</template>

<script>
import CreateBotForm from './components/CreateBotForm'
import EditBotForm from './components/EditBotForm'

export default {
  data: () => ({
    popupState: false,
    popupEdit: false,
    botsArray: [],
    edit: {}
  }),
  methods: {
    edited($event) {
      const botIdx = this.botsArray.findIndex(i => i.id === $event.id)
      this.botsArray[botIdx] = $event
    },
    getNewBot(value) {
      this.botsArray = value
    },
    editBot(item) {
      this.popupEdit = true
      this.edit = item
    },  
    deleteBot(id) {
      const botIdx = this.botsArray.findIndex(i => i.id === id)
      this.botsArray.splice(botIdx ,1)
    }
  },
  components: {
    CreateBotForm, EditBotForm
  }
}
</script>
