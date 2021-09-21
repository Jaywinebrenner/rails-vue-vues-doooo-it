<template>
    <div>
        <h1>Users</h1> 


        <div class="user-wrapper">
            <div 
                v-for="user in users" 
                :key="user.id"
                class="user">
                <h3>Name: {{user.name}} </h3>
                <h3>Address: {{ user.address}}  </h3>
                <h3>Age: {{ user.age}}</h3>
                <h3>Is this person a monster? {{ user.isMonster }}</h3>
            </div>
        </div>

        <form @submit="onSubmit()">
            <input type="text" v-model="name" placeholder="User Name">
            <input type="text" v-model="address" placeholder="User Address">
            <input type="text" v-model="age" placeholder="User Age">
            <input type="text" v-model="isMonster" placeholder="Is the user a monster">
              
            <button type="submit" class="add-user-button">Add User</button>


        </form>

    </div>
  
</template>

<script>

import axios from 'axios'



export default {


    name: "users",
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
        isMonster: null
        };
  },
    methods: {
        async onSubmit(){ 
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
        async fetchUsers(){
            const api_url = 'http://localhost:3000/api/v1/users'
            let res = await axios.get(api_url)
            // console.log("USERS RES", res.data)
            this.users = res.data
            // console.log("USERS DATA", this.users)
        },
        // async addUser(){
        //     console.log("name", this.name)
        //     const api_url = 'http://localhost:3000/api/v1/users'
        //     let res = await axios.post(api_url, 
        //         {
        //             user: {
        //                 name: this.name,
        //                 age: this.age,
        //                 address: this.address,
        //                 isMonster: this.isMonster
        //             }
        //         }
        //     )
        //     console.log("addUser Res", res)
        // }
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

</style>
