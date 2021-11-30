<template>
    <div class="row">
        <div class="task" v-if='task.value==="no"'>
            <h3>{{ task.name }}</h3>
            <Button @click='onDelete(task.id)' color='#99A799' name='delete'></Button>
            <Button @click='toggleModal()' color='#6E3CBC' name='edit'></Button>
        </div>

        <div v-if='isVisible'>
            <h1>Edit {{ task.name }}</h1>
            <input type='text' v-model='name' :placeholder='task.name'>
            <Button @click='onUpdate(task)' color='#6E3CBC' name='save'></Button>
        </div>
    </div>

</template>

<script>
    import Button from './Button';

    export default {
        name: 'Task',
        data() {
            return {
                isVisible: false,
            }
        },
        components: {
            Button
        },
        props: {
            task: Object,
            name: String
        },
        methods: {
            toggleModal() {
                this.isVisible = !this.isVisible
            },
            onUpdate(task) {
                let object = {
                    id: '',
                    name: '',
                    value: ''
                };
                if(this.name === undefined){
                    object.name = task.name;
                }
                else{
                    object.name = this.name;
                }
                object.id = task.id;
                object.value = task.value;
                object = JSON.stringify(object)
                fetch('http://localhost/vue-crud-app/api/update', {
                    method: 'POST',
                    mode : 'cors',
                    headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                    },
                    body: object
                })
                .then( response => response.json() )
                .then( 
                    data =>  {
                    alert('Task updated successfully!')
                    window.location.reload();
                })
            },
            onDelete(id){
                fetch('http://localhost/vue-crud-app/api/delete/'+id, {
                    method: 'POST',
                    mode : 'cors',
                    headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                    },
                    })
                    .then( response => response.json() )
                    .then( 
                        data =>  {
                        window.location.reload();
                    })
                }
            }
    }

</script>

<style scoped>
    @import '../assets/index.css';
    .task{
        background-color: #f4f4f4;
        margin: 5px;
        padding: 10px 20px;
        cursor: pointer;
    }
</style>