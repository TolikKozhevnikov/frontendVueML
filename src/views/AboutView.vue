<template>
  <div class="about">
    <h1>This is an about page</h1>
    <v-container>
      <v-card class="mx-auto pa-12 pb-8" elevation="8" max-width="448" rounded="lg">
        <div class="row">
          <v-file-input v-model="file" v-on:change="handleFileUpload()"></v-file-input>
          <v-spacer></v-spacer>
          <v-row align="center" justify="center">
            <v-btn class="center" color="success" text @click="dialog = false" v-on:click="submitFile()">
              <h5>Начать проверку</h5>
            </v-btn>
          </v-row>
          <button v-on:click="uploadFile()">Upload</button>
        </div>
        <v-list density="compact">
          <v-list-subheader>REPORTS</v-list-subheader>
          <v-list-item v-for="item in info" :key="item" :title="item"></v-list-item>
        </v-list>
      </v-card>

    </v-container>
  </div>
</template>



<script>

export default {
  data() {
    return {
      file: '',
      info: null
    }

  },
  methods: {

    uploadFile() {

      this.file = this.$refs.file.files[0];
      this.$refs.file.value = '';
      this.axios.post('http://127.0.0.1:7000/predict', this.file,
        {
          headers: {
            'Content-Type': 'application/json'
          }
        })
        .then(response => (this.info = response.data))
        .catch(function (error) {
          console.log(error);
        });

    },
    handleFileUpload() {
      this.file = this.$refs.file.files[0];
    },

  },

}
</script>
