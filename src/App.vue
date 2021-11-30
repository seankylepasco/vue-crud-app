<template>

  <div class='container'>
    <div class='card row'>
      <div class="container f-1 col">
        <Header title='Vue Crud Application' />
      </div>
      <div class="f-1  task-container">
        <Tasks :tasks="tasks" />
      </div>
    </div>
  </div>

</template>

<script>
import Header from './components/Header';
import Tasks from './components/Tasks';

export default {
  name: 'App',
  components: {
    Header,
    Tasks
  },
  data() {
    return {
      tasks: []
    }
  },
  mounted() {
    fetch('http://localhost/vue-crud-app/api/tests', {
      method: 'POST',
       mode : 'cors',
      headers: {
      'Content-Type': 'application/json',
      'Accept': 'application/json'
      },
    })
    .then( response => response.json() )
    .then( data =>  { this.tasks = data.payload} )
  }
}
</script>

<style>
 @import './assets/index.css';
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
