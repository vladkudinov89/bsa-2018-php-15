<template>
    <div class="user_lists">

        <todo v-on:delete-todo="deleteTodo" v-for="todo in people" :todo.sync="todo" :key="todo.id"></todo>

    </div>
</template>

<script>
    import Todo from "./Todo";

    export default {
        name: "TodoList",
        props: ["people"],
        components: {
            Todo
        },
        methods: {
            deleteTodo(todo) {
                sweetAlert({
                    title: "Delete User?",
                    icon: "warning",
                    buttons: true,
                    dangerMode: true,
                })
                    .then((willDelete) => {
                        if (willDelete) {
                            const todoIndex = this.people.indexOf(todo);
                            this.people.splice(todoIndex, 1);
                            swal("User has been deleted!", {
                                icon: "success",
                            });
                        }
                    });
            },

        },
    };
</script>

<style>
    .user_lists{
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: center;
    }

    .user_lists > .ui.card{
        margin: 1em 0.5em;
    }

    .ui.card:hover{
        cursor: pointer;
        transition: 0.3s ease-in;
        box-shadow: 0px 0px 19px 0px rgba(0,0,0,0.75);
    }
</style>
