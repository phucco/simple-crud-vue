<template>
    <div>
        <h1>Post Management</h1>
        <PostAdd :itemEdit="post" @save="clickSave" />
        <table class="table">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Title</th>
                    <th>Description</th>
                    <th>Status</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
				<tr v-for="item in list" :key="item.id">
                    <td>{{ item.id }}</td>            
                    <td>{{ item.title }}</td>            
                    <td>{{ item.description }}</td>            
                    <td>{{ item.status }}</td>
                    <td>
                        <button @click="clickEdit(item)">Edit</button>
                        <button @click="clickDelete(item)">Delete</button>
                    </td>        
                </tr>
			</tbody>
        </table>
    </div>
</template>

<script>
import PostAdd from './PostAdd.vue'

export default {
    components: {
        PostAdd
    },
    methods: {
        clickSave (itemSave) {
            let index = this.list.findIndex((c) => c.id === itemSave.id)
            if (index >= 0) {
                this.list.splice(index, 1, itemSave)
            } else {
                let max = 0
                for (let i=0;i<this.list.length;i++) {
                    if (this.list[i].id > max) {
                        max = this.list[i].id
                    }
                }                 
                itemSave.id = max + 1
                this.list.push(itemSave)
            }
            return;
        },
        clickEdit (itemEdit) {
            this.post = itemEdit
        },
        clickDelete (itemDelete) {
            for (let i=0;i<this.list.length;i++) {
                if (itemDelete.id === this.list[i].id) {
                    this.list.splice(i,1)
                }
            }
        }
    },
    data () {
        return {
            post: {},
            list: [
                {
                    id: 1,
                    title: 'Sample Post 1',
                    description: 'Lorem Ipsum 1',
                    status: 'Publish'
                },
                {
                    id: 2,
                    title: 'Sample Post 2',
                    description: 'Lorem Ipsum 2',
                    status: 'Draft'
                },
                {
                    id: 3,
                    title: 'Sample Post 3',
                    description: 'Lorem Ipsum 3',
                    status: 'Publish'
                }
            ]
        }
    }
}
</script>

<style scoped>
.table {
    border-collapse: collapse;
    width: 100%;
}
.table tr {
    line-height: 50px; 
}
.table td, .table th {
    border: 1px solid #000000;
    padding: 10px;
    text-align: left;
}
</style>