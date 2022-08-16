<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">Todo list</h1>
        <v-text-field label="Another task" v-model="newTask"></v-text-field>
        <v-btn color="primary" class="rounded-0" @click="addTask" :disabled="newTask.length==0">
          {{action}}
        </v-btn>        
         <v-simple-table class="todo-table">
          <template>
            <thead class="todo-table__header">     
              <tr>
                <th class="text-left"> Tasks </th>
                <th class="text-right ">Actions</th>    
              </tr>       
            </thead>
            <tbody>
              <tr  v-for="(item, index) in tasks" :key="index" class="todo-table__item">              
                <td class="text-left d-flex align-center todo-table__item__task" :class="`${ item.checked ? 'todo-table__item__task--done' : ''}`">
                  <v-checkbox small v-model="item.checked"  color="success" class="task-done-checkbox"></v-checkbox>
                  <p class="mb-0"> {{ item.task }}</p>                 
                </td>
                <td class="text-right todo-table__item__actions">
                  <v-icon small color="primary" class="mr-2" @click="editItem(item,index)">
                    mdi-pencil
                  </v-icon>
                  <v-icon small color="primary"  @click="deleteItem(index)"> mdi-delete </v-icon>
                </td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>       
      </v-col>      
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "HelloWorld",
  data: () => ({
    ecosystem: [
      {
        text: "vuetify-loader",
        href: "https://github.com/vuetifyjs/vuetify-loader",
      },
      {
        text: "github",
        href: "https://github.com/vuetifyjs/vuetify",
      },
      {
        text: "awesome-vuetify",
        href: "https://github.com/vuetifyjs/awesome-vuetify",
      },
    ],
    importantLinks: [
      {
        text: "Documentation",
        href: "https://vuetifyjs.com",
      },
      {
        text: "Chat",
        href: "https://community.vuetifyjs.com",
      },
      {
        text: "Made with Vuetify",
        href: "https://madewithvuejs.com/vuetify",
      },
      {
        text: "Twitter",
        href: "https://twitter.com/vuetifyjs",
      },
      {
        text: "Articles",
        href: "https://medium.com/vuetify",
      },
    ],
    whatsNext: [
      {
        text: "Explore components",
        href: "https://vuetifyjs.com/components/api-explorer",
      },
      {
        text: "Select a layout",
        href: "https://vuetifyjs.com/getting-started/pre-made-layouts",
      },
      {
        text: "Frequently Asked Questions",
        href: "https://vuetifyjs.com/getting-started/frequently-asked-questions",
      },
    ],
    headers: [
      { text: "Type", align: "start", sortable: false, value: "checked"},
      { text: "Tasks", align: "start", sortable: false, value: "task"},
      { text: "actions", align: "end", sortable: false, value: "actions" },
    ],
    tasks: [
      {
        checked: false, 
        task: "There are many variations of passages of Lorem Ipsum available",
      },
      {
        checked: false, 
        task: "There are many variations of passages of Lorem Ipsum available",
      },
      {
        checked: false, 
        task: "There are many variations of passages of Lorem Ipsum available",
      },
      {
        checked: false, 
        task: "There are many variations of passages of Lorem Ipsum available",
      },
      {
        checked: false, 
        task: "There are many variations of passages of Lorem Ipsum available",
      },
      {
        checked: false, 
        task: "There are many variations of passages of Lorem Ipsum available",
      },
      {
        checked: false, 
        task: "There are many variations of passages of Lorem Ipsum available",
      },
      {
        checked: false, 
        task: "There are many variations of passages of Lorem Ipsum available",
      },
      {
        checked: true, 
        task: "There are many variations of passages of Lorem Ipsum available",
      },
      {
        checked: true, 
        task: "There are many variations of passages of Lorem Ipsum available",
      },
    ],
    newTask: "",
    action: "add",
    editIndex : null, 
  }),
  created() {},
  mounted() {},
  methods: {
    addTask(){
      if(this.newTask ){
        if(this.action == "add"){
          this.tasks.unshift({
            checked: false, 
            task: this.newTask 
          })    
        }
        else{
          this.tasks[this.editIndex].task = this.newTask ;
        } 
        this.newTask = ""   ;
        this.action = "add"   
      }     
    },
    deleteItem(index){
      if( index == this.editIndex ){
        this.editIndex = null ;
        this.action = "add";
        this.newTask = "" ;
      }    
      this.tasks.splice(index , 1) 
    },
    editItem(item,index){
      this.action = "edit"; 
      this.newTask = item.task ; 
      this.editIndex = index
    }
  }
};
</script>
<style lang="scss">
.todo-table{
  &__item{
    &__task{        
        border-left: 2px solid #e00025;
        background: #F8F9FA;
      p{  
        position: relative;        
        &:before{
          content: "";
          width: 0;
          height: 2px;
          position: absolute;
          top: calc(50% - 1px);
          left: 0;
          background-color: #000;
          -webkit-transition: all .2s ease-in-out;
          transition: all .2s ease-in-out;
        }
      }      
      &--done{
        border-left: 2px solid #00A491;
        p{
          &:before{
            width: 100%;
          }
        }
      }
    }
    &__actions{     
      background: #F8F9FA;     

    }
  }
}
.task-done-checkbox{
  .v-icon.v-icon{
    font-size: 18px;
  }
}
</style>
