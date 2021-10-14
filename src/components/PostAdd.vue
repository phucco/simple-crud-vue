<template>
    <div>
        <div class="form-group">
            <label>Title: </label>
            <input type="text" v-model="post.title">
        </div>
        <div class="form-group">
            <label>Description: </label>
            <input type="text" v-model="post.description">
        </div>
        <div class="form-group">
            <label>Status: </label>
            <input type="text" v-model="post.status">
        </div>
        <button class="button" @click="clickSave">Save</button>
    </div>
</template>

<script>
export default {
    props: {
        itemEdit: {
            type: Object,
            default: null
        }
    },
    watch: {
        itemEdit() {
            if (this.itemEdit) {
                this.post = Object.assign({}, this.itemEdit)
            } else {
                this.post = {}
            }
        }
    },
    methods: {
        clickSave() {
            this.$emit('save', this.post)
            this.post = {
                id: Math.floor(Math.random()*1000),
                title: '',
                description: '',
                status: ''
            }
        }
    },
    data () {
        return {
            post: {
                id: Math.floor(Math.random()*1000),
                title: '',
                description: '',
                status: ''
            }
        }
    }
}
</script>

<style>
.form-group {
    margin-bottom: 10px;
}
.button {
    margin-bottom: 15px;
    margin-left: 15px;
}
</style>