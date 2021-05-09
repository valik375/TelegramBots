<template>
  <div class="popup-container">
    <div class="popup-wrapper">
      <h3 class="popup-title">Crete new bot</h3>
      <p class="popup-close" @click="$emit('close')">X</p>
      <form @submit.prevent="formSubmit" class="popup-form">
        
        <div class="input-group">
          <label for="bot-name">Bot name</label>
          <input type="text" id="bot-name" v-model="botName"/>
          <p style="font-size:14px; color: red; margin-top:10px" v-if="errors.eName">{{errors.eName}}</p>
        </div>

        <div class="input-group">
          <label for="bot-description">Bot description</label>
          <textarea id="bot-description" cols="10" rows="4" v-model="botDescription"></textarea>
          <p style="font-size:14px; color: red; margin-top:10px" v-if="errors.eDescription">{{errors.eDescription}}</p>
        </div>

        <div class="input-group file">
          <label class="upload-image" for="bot-image">Upload image</label>
          <p class="file-name" v-if="botImage">File name: {{ botImage }}</p>
          <input type="file" id="bot-image" @change="onFileChange"/>
          <p style="font-size:14px; color: red; margin-top:10px" v-if="errors.eImage">{{errors.eImage}}</p>
        </div>

        <div class="input-group">
          <label for="bot-date">Date</label>
          <input type="date" id="bot-date" v-model="botDate"/>
          <p style="font-size:14px; color: red; margin-top:10px" v-if="errors.eDate">{{errors.eDate}}</p>
        </div>

        <button type="submit" class="btn">Create</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    botName: '',
    botDescription: '',
    botImage: '',
    botDate: '',
    botId: Date.now(),
    newBot: {},
    errors: {
      eName: '',
      eDescription: '',
      eImage: '',
      eDate: ''
    }
  }),
  methods: {
    formSubmit() {
      
      this.botName.length <= 0 ? this.errors.eName = 'Fill in the Name field' : this.errors.eName = ''
      this.botDescription.length <= 0 ? this.errors.eDescription = 'Fill in the Description field' : this.errors.eDescription = ''
      this.botImage.length <= 0 ? this.errors.eImage = 'Insert picture' : this.errors.eImage = ''
      this.botDate.length <= 0 ? this.errors.eDate = 'Fill in the Date field' : this.errors.eDate = ''

      if(this.botName && this.botDescription && this.botImage && this.botDate) {
        this.newBot = {
          name: this.botName,
          description: this.botDescription,
          image: this.botImage,
          date: this.botDate,
          id: this.botId,
        }
        this.$emit('close')
        this.$emit('array', this.newBot)
      }
    },
    onFileChange(event) {
      const fileData =  event.target.files[0];
      this.botImage = fileData.name;
    }
  }
};
</script>
