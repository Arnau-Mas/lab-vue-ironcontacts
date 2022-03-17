<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from './components/HelloWorld.vue'
import contacts from "./contacts.json"
import {ref, reactive} from 'vue';
const fiveContacts = reactive(contacts.splice(0,5));
function addRandomContact(){
  if(contacts.length>0){
      let newContact = contacts.splice(Math.floor(Math.random()*contacts.length-1),1);
  fiveContacts.push(newContact[0]);
  }
}
function sortByName(){
  fiveContacts.sort(function (a, b) {
  if (a.name > b.name) {
    return 1;
  }
  if (a.name < b.name) {
    return -1;
  }
  return 0;
})
}
function sortByPopularity(){
  fiveContacts.sort(function (a, b) {
  if (a.popularity > b.popularity) {
    return 1;
  }
  if (a.popularity < b.popularity) {
    return -1;
  }
  return 0;
})
}
function deleteContact(id){
  let index = fiveContacts.findIndex(contact => contact.id == id);
  contacts.push(...fiveContacts.splice(index,1))
}
</script>

<template>
  <div class="ironContacts">
    <h1>IronContacts</h1>
    <button @click="addRandomContact">Add random contact</button>
    <div>
      <table>
        <tr>
          <th>Picture</th>
          <th @click="sortByName" class="orderElement name">Name ⇅</th>
          <th @click="sortByPopularity" class="orderElement popularity">Popularity ⇅</th>
          <th>Won an Oscar</th>
          <th>Won an Emmy</th>
        </tr>
        <tr v-for="contact in fiveContacts" :key="contact.id">
          <td><img :src="contact.pictureUrl" alt=""></td>
          <td>{{contact.name}}</td>
          <td>{{contact.popularity.toFixed(2)}}</td>
          <td v-if="contact.wonOscar">🏆</td>
          <td v-else></td>
          <td v-if="contact.wonEmmy">🏆</td>
          <td v-else></td>
          <td><button @click="deleteContact(contact.id)">Delete</button></td>
        </tr>
      </table>
    </div>
  </div>
</template>

<style>
#app {
  display: flex;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
td{
  padding: 0.5rem;
  padding-top: 0.5rem;
}
img{
  height: 110px;
}

.ironContacts{
  margin: auto;
  width: 45rem;
}

button{
  margin-bottom: 1rem;
}

.orderElement:hover{
  color:rgb(72, 212, 159);
  cursor: pointer;
}

</style>
