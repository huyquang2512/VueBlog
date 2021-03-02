<template>
<blog-edit></blog-edit>
</template>

<script>
import BlogEdit from '@/components/AppEditCreate/blogEdit.vue'

export default {
    components: {
        BlogEdit
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
