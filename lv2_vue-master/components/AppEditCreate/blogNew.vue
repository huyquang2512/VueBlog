<template>
<div class="blogNew">
    <h1>New Blog</h1>
    <p>Tiêu đều</p>
    <input type="text" style="width: 50%;" v-model="form.title">
    <p>Mô tả ngắn</p>
    <input type="text" style="width: 50%;" v-model="form.des">
    <p>Mô tả ngắn</p>
    <textarea name="" id="" cols="30" rows="10" style="width: 50%;" v-model="form.detail"></textarea>
    <p>Hình ảnh </p>
    <input type="text" name="" id="" v-model="form.thumbs" />
    <p>Loại</p>
    <select v-model="form.category">
        <option value="1">Thời Sự</option>
        <option value="2">Saab</option>
        <option value="3">Opel</option>
        <option value="4">Audi</option>
    </select>
    <p>Vị trí</p>
    <ul class="list-group list-group-flush">
        <li v-for="(post,key) in CONTRY" :key="post" class="list-group-control">
            <div class="custom-control custom-checkbox">
                <input type="checkbox" :value="post" class="custom-control-input" :id="'check' + key + 1" v-model="form.position">
                <label class="custom-control-label" :for=" 'check' + key + 1">{{ post }}</label>
            </div>
        </li>
    </ul>
    <p>Public</p>
    <input type="radio" id="checkbox1" name="yes" :value="true" v-model="form.public2"><label for="checkbox1">Yes</label><br>
    <input type="radio" id="checkbox2" name="no" :value="false" v-model="form.public2"><label for="checkbox2">No</label><br>
    <p>Date Public</p>
    <input type="date" name="" id="" v-model="form.data_pubblic">
    <br><br><br>
    <button type="button" class="btn btn-success" @click="submitButton()">Success 1</button>
    <button type="button" class="btn btn-primary">Primary</button>
</div>
</template>

<script>
import axios from 'axios'
export const CONTRY = ["Việt Nam", 'Châu Âu', 'Châu Á', 'Châu Mỹ']
export default {
    components: {

    },
    data() {
        return {
            CONTRY,
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
    methods: {
        submitButton() {
            axios.post('http://localhost:4000/blogs', this.form)
        }
    }
}
</script>

<style>
.blogNew {
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
