<template>
    <div>
        <h3>Filter Components</h3>
        <select @change="filterUsers($event)">
            <option value="All" selected>All</option>
            <option value="1">1</option>
            <option value="5">5</option>
            <option value="10">10</option>
            <option value="15">15</option>
            <option value="20">20</option>


        </select>


    </div>
  
</template>

<script>




export default {


name: "filterUsers",
  data() {
    return {

        };
  },
  props: {
      filterUsers: Function
  },
    methods: {
    },
    computed: {

    },
    created(){

    }

};
</script>

<style scoped>
h3 {
    margin-bottom: 0px;
    display: inline-block;
}
select {
    margin: 0px 0 20px 0;
    padding: 6px;
    border: black;
}


</style>
