<template>
    <div class="Model3">


        <v-card class="mx-auto pa-12 pb-8" elevation="8" max-width="500" rounded="lg">
            <h3 class="text-h5 ">
                Модель 1
            </h3>
            <br>
            <v-divider :thickness="1" class="border-opacity-25"></v-divider>
            <br>
            
            <v-file-input v-model="file" v-on:change="handleFileUpload()" ref="file"
                label="Нажмите, чтобы загрузить файл">
            <div ></div></v-file-input>

            <v-divider :thickness="1" class="border-opacity-25"></v-divider>
            <br>
            <v-btn class="center" color="success" text @click="dialog = false" v-on:click="submitFile()">
                <h5>Начать проверку</h5>
            </v-btn>
            <div v-if="trigerFile">
                <br>
                <v-alert type="warning" title="Файл не добавлен!"></v-alert>
            </div>
            <div v-else>
                <div v-if="info">
                    <br>
                    <v-divider :thickness="1" class="border-opacity-25"></v-divider>
                    <br>
                    <v-table>
                        <thead>
                            <tr>
                                <th class="text-center">
                                    Результаты
                                </th>
                                <th class="text-center">
                                    Оценка
                                </th>

                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="item in res" :key="item.name">
                                <td>{{ item.name }}</td>
                                <td>{{ item.answer }}</td>
                            </tr>
                        </tbody>
                    </v-table>
                </div>
            </div>


        </v-card>
    </div>
</template>

<script>

import axios from "axios";
export default {
    data() {

        return {
            trigerFile: false,
            name: "",
            file: "",
            info: "",
            res: ""

        };
    },
    methods: {

        submitFile() {
            if (this.file != "") {
                
                this.XnetIsComplite = false;
                let formData = new FormData();

                formData.append("title", this.name);
                if (this.file != null) {
                    formData.append("image", this.file);
                    axios.post('http://127.0.0.1:7000/predict', this.file,
                        {
                            headers: {
                                'Content-Type': 'application/json'
                            }
                        })
                        .then(response => (this.info = response.data, this.res = [
                            {
                                name: 'Болезнь 1',
                                answer: this.info[0],
                            },
                            {
                                name: 'Болезнь 2',
                                answer: this.info[1],
                            },
                            {
                                name: 'Болезнь 3',
                                answer: this.info[2],
                            },
                            {
                                name: 'Болезнь 4',
                                answer: this.info[3],
                            },
                            {
                                name: 'Болезнь 5',
                                answer: this.info[4],
                            },
                            {
                                name: 'Болезнь 6',
                                answer: this.info[5],
                            },
                            {
                                name: 'Болезнь 7',
                                answer: this.info[6],
                            },
                        ], this.trigerFile = !this.trigerFile
                        ))
                        .catch(function (error) {
                            console.log(error);
                        });


                }
            } else {
                this.trigerFile = true;
            }
        },
        handleFileUpload() {
            this.file = this.$refs.file.files[0]
            return this.file
        },
        mounted() {
            this.NormalOrNot = "";
        },
    },
};

</script>



