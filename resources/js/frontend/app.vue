<template>
  <div class="todoListContainer">
    <div class="heading">
      <h2 id="title">Todo List</h2>
      <add-item-form
        v-on:reloadlist="getList()"
      />
    </div>
      <list-view
        :items="items"
        v-on:reloadlist="getList()"
      />
  </div>
</template>

<script>
import axios from 'axios';
import addItemForm from './addItemForm';
import listView from './listView';

export default {
  components: {
    addItemForm,
    listView
  },
  data() {
      return {
        items: []
      }
  },
  methods: {
    getList: function(){
      axios.get('api/items')
        .then(res => {
          this.items = res.data
        })
        .catch(err => {
          console.log(err);
        });
    }
  },
  created(){
    this.getList();
  }
};
</script>

<style scoped>
  .todoListContainer {
    width: 350px;
    margin: auto;
  }
  .heading {
    background: #e6e6e6;
    padding: 10px;
  }
  #title {
    text-align: center;
  }
</style>
