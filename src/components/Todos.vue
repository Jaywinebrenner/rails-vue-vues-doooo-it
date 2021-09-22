<template>
    <div>
        <!-- <h3>Todos</h3>
        <div class="legend">
            <span>Double click to mark as complete</span>
            <span>
                <span class="incomplete-box"></span> = incomplete
            </span>
            <span>
                <span class="complete-box"></span> = complete
            </span>
        </div>
        <div class="todos">
            <div 
                v-for="todo in allTodos"
                :key="todo.id"
                class="todo"
                @dblclick="onDoubleClick(todo)"
                v-bind:class="{'is-complete' : todo.completed}"
            >
            {{todo.title}}
            <i 
            class="fas fa-trash-alt"
            @click="deleteTodo(todo.id)" />
              
            </div>
        </div> -->

    </div>
  
</template>

<script>

import {mapGetters, mapActions} from 'vuex'


export default {


    name: "todos",
    methods: {
        ...mapActions([
            'fetchTodos', 
            'deleteTodo', 
            'updateTodo'
        ]),
        onDoubleClick(currentTodo){
            const updatedTodo = {
                id: currentTodo.id,
                title: currentTodo.title,
                complete: !currentTodo.completed
            }
            this.updateTodo(updatedTodo)
        }
    },
    computed: {
        ...mapGetters([
            'allTodos',
        ])
    },
    created(){
        this.fetchTodos();
    }

};
</script>

<style scoped>

.todos{
    display: grid;
    grid-template-columns: repeat(3,1fr);
    grid-gap: 1rem;
}
.todo {
    border: 1px solid black;
    /* background: pink; */
    padding: 1rem;
    text-align: center;
    position: relative;
    cursor: pointer;
}

i {
    position: absolute;
    bottom: 10px;
    right: 10px;
    color: blueviolet;
    cursor: pointer;
}

.legend {
    display: flex;
    justify-content: space-around;
    margin-bottom: 1rem;

}

.complete-box {
    display: inline-block;
    width: 10px;
    height: 10px;
    background: #35495e;
}

.incomplete-box {
    display: inline-block;
    width: 10px;
    height: 10px;
    background: burlywood
}

.is-complete {
    background: #35495e;
    color: #fff;
}

@media (max-width: 500px) {
    .todos {
        grid-template-columns: 1fr;
    }
}

</style>
