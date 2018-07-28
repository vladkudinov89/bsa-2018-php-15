<template>
    <div class='ui basic content center aligned segment '>
        <button class='ui primary button' v-on:click="openForm" v-show="!isCreating">
            <i class='user icon'></i> +Add User
        </button>
        <div class='ui centered card' v-show="isCreating">
            <div class='content'>
                <div class='ui form'>
                    <div class='field'>
                        <label>ID</label>
                        <input v-model="id" type='text' readonly>
                    </div>
                    <div class='field'>
                        <label>Name</label>
                        <input v-model="name" type='text'>
                    </div>
                    <div class='field'>
                        <label>Email</label>
                        <input v-model="email" type='text'>
                    </div>
                    <div class='field'>
                        <label>Phone</label>
                        <input v-model="phone" type='text'>
                    </div>
                    <div class='ui two button attached buttons'>
                        <button class='ui basic blue button' v-on:click="sendForm()">
                            Create
                        </button>
                        <button class='ui basic red button' v-on:click="closeForm">
                            Cancel
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                id: this.people + 1 ,
                name: '',
                email: '',
                phone: '',
                isCreating: false,
            };
        },
        props : [ "people"],
        methods: {
            openForm() {
                this.isCreating = true;
            },
            closeForm() {
                this.isCreating = false;
            },
            sendForm() {
                if (
                    this.name.length > 0
                    &&
                    this.email.length > 0
                    &&
                    this.phone.length > 0
                ) {
                    const id = this.id;
                    const name = this.name;
                    const email = this.email;
                    const phone = this.phone;
                    const avatar = '';
                    this.$emit('create-user', {
                        id,
                        name,
                        email,
                        avatar,
                        phone
                    });
                    console.log("User Add");
                    this.name = '';
                    this.email = '';
                    this.phone = '';
                    this.isCreating = false;
                }
            },
        },
    };
</script>