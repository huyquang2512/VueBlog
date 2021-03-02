<template>
<div class="blogEdit">
    <h1>Edit Blog</h1>
    <p>Tiêu đều</p>
    <input type="text" style="width: 50%;" v-model="dataBlog.title">
    <p>Mô tả ngắn</p>
    <input type="text" style="width: 50%;" v-model="dataBlog.des">
    <p>Chi tiết</p>
    <textarea name="" id="" cols="30" rows="10" style="width: 50%;" v-model="dataBlog.detail"></textarea>
    <p>Hình ảnh </p>
    <input type="file" name="" id="" />
    <p>Loại</p>
    <select v-model="dataBlog.category">
        <option v-for="category in category" :key="category.value" :value='category.value'>{{category.text}}</option>
    </select>
    <p>Vị trí</p>
    <input type="checkbox" name="" id=""><label for="vehicle1"> Việt Nam</label><br>
    <input type="checkbox" name="" id=""><label for="vehicle1"> Châu Âu</label><br>
    <input type="checkbox" name="" id=""><label for="vehicle1"> Châu Á</label><br>
    <input type="checkbox" name="" id=""><label for="vehicle1"> Châu Mỹ</label><br>
    <p>Public</p>
    <input type="radio" id="checkbox1" name="yes" :value="true" v-model="dataBlog.public"><label for="checkbox1">Yes</label><br>
    <input type="radio" id="checkbox2" name="no" :value="false" v-model="dataBlog.public"><label for="checkbox2">No</label><br>
    <p>Date Public</p>
    <input type="date" name="" id="" v-model="dataBlog.data_pubblic">
    <br><br><br>
    <button type="button" class="btn btn-success" @click="submitButton()">Success</button>
    <button type="button" class="btn btn-primary">Primary</button>
</div>
</template>

<script>
import axios from 'axios'
export default {
    components: {

    },
    data() {

        return {
            dataBlog: [],
            category: [{
                    value: '1',
                    text: 'Thời Sự'
                },
                {
                    value: '2',
                    text: 'Saab'
                },
                {
                    value: '3',
                    text: 'Opel'
                },
                {
                    value: '4',
                    text: 'Audi'
                }
            ],
            form: {
                'title': '',
                'des': '',
                'detail': '',
                'public2': '',
                'position': [],
                'data_pubblic': '',
            },
        }
    },
    mounted() {
        this.listData();
    },
    methods: {
        listData() {
            axios({
                method: 'GET',
                url: `http://localhost:4000/blogs/` + this.$route.params.id,

                data: null
            }).then(res => {
                console.log(this.$route.params.id),
                    this.dataBlog = res.data;
                console.log(this.dataBlog)
            }).catch(err => {
                console.log(err)
            })
        },
        submitButton() {
            axios.post('http://localhost:4000/blogs', this.form)
        }
    }
}
</script>

<style>
.blogEdit {
    width: 70%;
    height: auto;
    float: left;
}

.btn-success {
    margin-left: 40%;
}

p,
input,
select,
textarea {
    margin-left: 3%;
}
</style>
