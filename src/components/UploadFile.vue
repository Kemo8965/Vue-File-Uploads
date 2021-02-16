<template>
  <div class="container">
    <div class="large-12 medium-12 small-12 cell">
      <label>File
        <input type="file" id="files" ref="files" v-on:change="handleFileUploads()"/>
      </label>
      <br>
      <br>
      <br>
        <button v-on:click="submitFiles()">Submit</button>
    </div>
  </div>
</template>

<script>

import axios from 'axios';

  export default {

    data(){
  return {
    files: ''
  }
},
    methods: {
      
      submitFiles(){
        let formData = new FormData();
        for( var i = 0; i < this.files.length; i++ ){
  let file = this.files[i];

  formData.append('files[' + i + ']', file);
}
        
        axios.post( '/about',
  formData,
  {
    headers: {
        'Content-Type': 'multipart/form-data'
    }
  }
).then(function(){
  console.log('SUCCESS!!');
})
.catch(function(){
  console.log('FAILURE!!');
});
      },

      handleFileUploads(){
        this.files = this.$refs.files.files[0];

      }
    }
  }
</script>