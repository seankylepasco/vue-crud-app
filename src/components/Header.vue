<template>

    <header>
        <h1>{{ title }}</h1>
        <Button name='Add task' @click='onToggle()' color='#6E3CBC' />
    </header>

    <div v-if='isVisible' class='modal'>
        <h1>Create new task</h1>
        <hr><br><br>
        <input type="text" v-model='name' placeholder='Enter task name .. '>
        <br><br>
        <Button name='Save' @click='onInsert()' color='#6E3CBC' />
    </div>

</template>

<script>
import Button from './Button';

export default {
    name: 'Header',
    data() {
        return {
            isVisible: false
        } 
    },
    props: {
        title: String,
        name: String
    },
    components: {
        Button
    },
    methods: {
        onToggle() {
            this.isVisible = !this.isVisible;
        },
        onInsert(){
             let object = {
                name: ''
            };
            if(this.name === undefined){
                alert('name is missing!')
            }
            else{
                object.name = this.name;
                object = JSON.stringify(object)
                fetch('http://localhost/vue-crud-app/api/insert', {
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
                    alert('Task added successfully!')
                    window.location.reload();
                })
            }
        }
    }
}

</script>

<style scoped>
    .modal{
        background-color: #f4f4f4;
        margin: 5px;
        padding: 10px 20px;
        height: max-content;
        cursor: pointer;
    }
</style>