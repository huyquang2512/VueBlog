<template>
<div class="blog col-8">
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
            <tr v-for="blogs in dataBlog" :key="blogs.id">
                <th scope="row">{{blogs.id}}</th>
                <td>{{blogs.title}}</td>
                <td>{{blogs.category}}</td>
                <td>{{changeTextStatus(blogs.public)}}</td>
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
        const contry = [{
                text: 'Thời Sự',
                value: 1
            },
            {
                text: 'Kinh Tế',
                value: 2
            },
            {
                text: 'Kinh Tế',
                value: 3
            },
            {
                text: 'Kinh Doanh',
                value: 4
            }
        ]

        return {
            dataBlog: [],
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
        },
        changeTextStatus(status) {
            const publicData = status == true ? 'Yes' : 'No'

            return publicData;
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
