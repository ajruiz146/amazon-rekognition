<template>
  <h1>Upload file</h1>
  <input type="file" accept="image/*" @change="handleFileUpload">
  <button type="button" @click="pre_process()">Send</button>
</template>

<script>
  import axios from 'axios'

  export default {
    data: () => ({
      file: null,
    }),
    methods: {
      pre_process: function () {
        let formData = new FormData()
        formData.append('file', this.file)
        axios.post( '/api/preprocess',
            formData,
            {
              headers: {
                'Content-Type': 'multipart/form-data'
              }
            }
        ).then(function(){
          console.log('SUCCESS!!')
        })
        .catch(function(){
          console.log('FAILURE!!')
        });
      },
      handleFileUpload(event){
        this.file = event.target.files[0]
      },
    }
  }
</script>
