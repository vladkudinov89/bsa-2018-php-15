<template>
    <div class="user_lists">

        <user-item v-on:delete-user="deleteUser" v-for="user in people" :user.sync="user" :key="user.id"></user-item>

    </div>
</template>

<script>
    import UserItem from "./UserItem";

    export default {
        name: "UsersList",
        props: ["people"],
        components: {
            UserItem
        },
        methods: {
            deleteUser(user) {
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
