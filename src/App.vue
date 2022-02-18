<template>
  <div class="container">
    <h1 style="color:green;">Todo List</h1>
    <div id="app">
      <div class="input-group mb-3">
        <input type="text" v-model="name" placeholder="Create Task" aria-label="Recipient's username" aria-describedby="button-addon2">
        <span v-if="editStatus == false">
          <button class="btn btn btn-warning" type="button" id="button-addon2" @click="addTask">Add</button>
        </span>
        <span v-else>
          <button class="btn btn btn-warning" type="button" id="button-addon2" @click="updateTask">Upadte</button>
        </span>
      </div>

      <table class="table table-striped">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Task</th>
            <th scope="col"></th>
            <th scope="col"></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in items" :key="item">
            <td>{{ index+1 }}</td>
            <td>{{ item }}</td>
            <td><button class="btn btn btn-secondary" type="button" id="button-addon2" @click="editTask(item, index)">Edit</button></td>
            <td><button class="btn btn btn-danger" type="button" id="button-addon2" @click="deleteTask(index)">Delete</button></td>
          </tr>
 
        </tbody>
      </table>

    </div>
  </div>


</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'


export default ({
  //el: '#app',

  data() {
    return {
      editStatus: false,
      tmp: "",
      name: "",
      items : [
        "Go Running",  "Pratice drawing"
      ],
    }
  },
  methods: {
    addTask: function() {
      if(this.name === "") return;
      else {
        this.items.push(this.name);
        this.name = "";
      }
    },

    updateTask: function() {
      this.items.splice(this.items.indexOf(this.tmp), 1, this.name);
      this.name = "";
    },

    editTask: function(item, index) {
      this.name = this.items[index];
      this.tmp = this.items[index];
      this.editStatus = true;
    },

    deleteTask: function(index) {
      this.items.splice(index, 1);
    }


  }
});
</script>

<style>
.container {
  margin-top: 50px;
}

#app {
  margin-top: 20px;
}
</style>
