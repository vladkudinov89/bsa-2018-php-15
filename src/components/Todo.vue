<template>

    <div class='ui centered card'>

        <div class="content" v-show="!isEditing">
            <div class='meta text-left'>
             <span class="meta_user">ID:</span>  {{ todo.id }}
            </div>
            <div class='header'>

                <img class="right floated mini ui image" v-if="todo.avatar" :src="todo.avatar" alt="">
                <img class="right floated mini ui image" v-else="todo.avatar" :src="imageUrl" alt="">

            </div>
            <div class='meta text-left'>
               <span class="meta_user">Name:</span> {{ todo.name }}
            </div>
            <div class='meta text-left'>
              <span class="meta_user">Email:</span>  {{ todo.email }}
            </div>
            <div class='meta text-left'>
                <span class="meta_user">Phone:</span>  {{ todo.phone }}
            </div>
            <div class="extra content">
                <div class="ui two buttons">
                    <div class="ui basic green button" v-on:click="showForm">
                        Edit
                    </div>
                    <div class="ui basic red button" v-on:click="deleteTodo(todo)">Delete</div>
                </div>
            </div>
        </div>

        <div class="content" v-show="isEditing">
            <div class='ui form'>
                <div class='field'>
                    <label>ID</label>
                    <input type='text' v-model="todo.id" readonly="readonly">
                </div>
                <div class='field'>
                    <label>Name</label>
                    <input type='text' v-model="todo.name">
                </div>
                <div class='field'>
                    <label>Email</label>
                    <input type='email' v-model="todo.email">
                </div>
                <div class='field'>
                    <label>Phone</label>
                    <input type='text' v-model="todo.phone">
                </div>
                <div class='ui two button attached buttons'>
                    <button class='ui basic blue button' v-on:click="hideForm">
                        Close X
                    </button>
                </div>
            </div>
        </div>

    </div>
</template>

<script> export default {
    props: ['todo'],
    data() {
        return {
            imageUrl: 'https://intellihr.com.au/wp-content/uploads/2017/06/avatar_placeholder_temporary.png',
            isEditing: false,
        };
    },
    methods: {
        showForm() {
            this.isEditing = true;
        }, hideForm() {
            this.isEditing = false;
        },
        deleteTodo(todo) {
            this.$emit('delete-todo', todo);
        },
    },
}; </script>

<style scoped>
    .header img {
        width: 50px;
        height: 50px;
    }
    .meta_user{
        font-weight: bold;
        color: #000;
        display: block;
    }
    .text-left{
        text-align: left;
    }
</style>