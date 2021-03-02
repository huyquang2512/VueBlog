<template>
<div class="blog">
    <h3>Search Blog</h3><br>
    <div>Tiêu đề &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<input style="width: 80%;" v-model="search"></div><br>
    <button type="button" class="btn btn-success">Search</button><br>
    <br>
    <h3>List Blog</h3>
    <table class="table table-bordered">
        <thead>
            <tr>
                <th scope="col">Id</th>
                <th scope="col">Tin</th>
                <th scope="col">Loại</th>
                <th scope="col">Trạng Thái</th>
                <th scope="col">Ngày public</th>
                <th scope="col">Edit</th>
                <th scope="col">Delete</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="blogs in filterB">
                <th scope="row">{{blogs.id}}</th>
                <td>{{blogs.title}}</td>
                <td>{{blogs.category}}</td>
                <td>{{blogs.public}}</td>
                <td>{{blogs.data_pubblic}}</td>
                <td>
                    <nuxt-link :to="`/blogs/${blogs.id}`">Edit</nuxt-link>
                </td>
                <td><button type="button" class="btn btn-outline-danger" @click="deleted(blogs.id)">Delete</button></td>
            </tr>
        </tbody>
    </table>
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
            search: '',
        }
    },
    mounted() {
        this.listData();
    },
    methods: {
        listData() {
            axios({
                method: 'GET',
                url: 'http://localhost:4000/blogs',
                data: null
            }).then(res => {
                this.dataBlog = res.data;
            }).catch(err => {
                console.log(err)
            })
        },
        deleted(id) {
            axios.delete('http://localhost:4000/blogs/' + id)
                .then(() => {
                    this.dataBlog.splice(id, 4),
                        this.listData()
                });
        },
        updateBlog: function (data, id) {
            this.$router.push(id)
        }
    },
    computed: {
        filterB: function () {

            return this.dataBlog.filter((blog) => {

                return blog.title.match(this.search)
            })
        }
    }
}
</script>

<style>
.blog {
    width: 70%;
    height: 80vh;
    float: left;
}

td {
    border: 2px solid black;
}
</style>
