<template>
    <div>
     
        <form class="form" @submit="addUser()">
            <h3>Add New Person</h3>
            <input type="text" v-model="name" placeholder="User Name">
            <input type="text" v-model="address" placeholder="User Address">
            <input type="text" v-model="age" placeholder="User Age">
            <input type="text" v-model="isMonster" placeholder="Is the user a monster">
              
            <button type="submit" class="add-user-button">Add User</button>


        </form>
        <FilterUsers :filterUsers="filterUsers"/>


        <div class="user-wrapper">
            <div 
                v-for="user in users" 
                :key="user.id"
                class="user">
                <h3>Name: {{user.name}} </h3>
                <h3>Address: {{ user.address}}</h3>
                <h3>Age: {{ user.age}}</h3>
                <h3>Is this person a monster? {{ user.isMonster }}</h3>
                <button @click="destroyUser(user.id)" >delete</button>
                <button @click="showUpdateForm(user.id)" >update</button>
                <form v-if="isUpdateVisible" class="form" v-bind:class="{ active: isActive }" @submit="addUser()">
                    <h3>Update User</h3>
                    <input type="text" v-model="name" placeholder="User Name">
                    <input type="text" v-model="address" placeholder="User Address">
                    <input type="text" v-model="age" placeholder="User Age">
                    <input type="text" v-model="isMonster" placeholder="Is the user a monster">
                    <button type="submit" class="add-user-button">Update User</button>
                </form>
            </div>
        </div>



    </div>
  
</template>

<script>

import axios from 'axios'
import FilterUsers from '@/components/FilterUsers.vue'



export default {


name: "users",
components: {
    FilterUsers
},
  data() {
    return {
      users: [],
      fakeUpdate: {
          name: "Fred McUpdate",
          age: 12,
          address: "222 McUpdate Drive",
          isMonster: false
      },
        name: null,
        age: null,
        address: null,
        isMonster: null,
        isUpdateVisible: false
        };
  },
    methods: {
        async addUser(){ 
            // event.prevent.default();
            console.log("CLICKED")
            const api_url = 'http://localhost:3000/api/v1/users'
            let res = await axios.post(api_url, 
                {
                    user: {
                        name: this.name,
                        age: this.age,
                        address: this.address,
                        isMonster: this.isMonster
                    }
                }
            )
            console.log("addUser Res", res)
        },

        async destroyUser(id){
            const api_url = `http://localhost:3000/api/v1/users/${id}`
            let res = await axios.delete(api_url)
            this.fetchUsers()
            console.log("delete data", res.data)
        },

        showUpdateForm(id) {
            let userDiv = this.users.filter(val => val.id === id)
            console.log("user Div", userDiv[0].id)
            console.log("id", id)
            if (id === userDiv[0].id){
                this.isUpdateVisible = !this.isUpdateVisible
            }
   
            // this.isUpdateVisible = !this.isUpdateVisible
        },

        async filterUsers (event) {
            const limit = parseInt(event.target.options[event.target.options.selectedIndex].innerText)
            console.log(limit)
            if(!limit){
                this.fetchUsers()
            } else {
            let res = await axios.get(`http://localhost:3000/api/v1/users?_limit=${limit}`)
            this.users = res.data;
            console.log("RES", res.data)
            }
            
        },
        async fetchUsers(){
            
            const api_url = 'http://localhost:3000/api/v1/users'
            let res = await axios.get(api_url)
            // console.log("USERS RES", res.data)
            this.users = res.data
            // console.log("USERS DATA", this.users)
        },
    },
    computed: {

    },
    created(){
        this.fetchUsers()
    }

};
</script>

<style scoped>

h1, h3{
    margin: 0;
}

.user {
    border: 1px solid black;
    padding: 10px;
    }

.user-wrapper {
    display: grid;
    grid-template-columns: repeat(3,1fr);
    grid-gap: 1rem;
}

.add-user-button {
    border: 1px solid black;
    display: inline-block;
    padding: 5px;
    cursor: pointer;
    transition: .3s;
}

.add-user-button:hover {
    background-color: gray;
}

.form {
    display: flex;
    justify-content: center;
    /* align-content: center; */
    flex-direction: column;
    align-items: center;
    border: 1px solid black;
    margin: 10px 0;
}

.form input {
    width: 200px;
    margin: 10px;
}

.form button {
    width: 100px;
    margin: 10px;
}

</style>
