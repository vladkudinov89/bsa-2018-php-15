<template>
    <div id="app">

        <div class="ui container">

            <div class='search_panel'>
                <h2>Search</h2>
                <div>
                    <div class="ui left icon input search_input">
                        <input type="text" placeholder="Search users..." v-model="searchUser">
                        <i class="users icon"></i>
                    </div>
                </div>

               <div class="">
                   <div>Select search by</div>
                   <select class="ui dropdown selection search_select " v-model="searchBy" >
                       <option v-for="paramSearch in paramsSearch" v-bind:value="paramSearch.nameParam">
                           {{paramSearch.nameParam}}
                       </option>
                   </select>
               </div>
                <button class="ui primary button" v-bind:class="{disabled : btnSearch }" @click="filterUser">Search</button>
            </div>

            <create-user v-on:create-user="createUser" v-bind:people="people.length"></create-user>
            <TodoList v-bind:people="people"/>
        </div>

    </div>
</template>

<script>
    // import HelloWorld from "./components/HelloWorld";
    import sweetalert from 'sweetalert';
    import TodoList from "./components/TodoList";
    import CreateUser from "./components/CreateUser";

    export default {
        name: "App",
        components: {
            TodoList,
            CreateUser
        },
        data() {
            return {
                todos: [
                    {
                        title: "Todo A",
                        project: "Project A",
                        done: false
                    },
                    {
                        title: "Todo B",
                        project: "Project B",
                        done: true
                    },
                    {
                        title: "Todo C",
                        project: "Project C",
                        done: false
                    },
                    {
                        title: "Todo D",
                        project: "Project D",
                        done: false
                    }
                ],
                people: [
                    {
                        id: 1,
                        name: "Leanne Graham",
                        email: "Sincere@april.biz",
                        avatar: "https://cdn.iconscout.com/public/images/icon/free/png-512/avatar-user-business-man-399587fe24739d5a-512x512.png",
                        phone: "54846886446"
                    },
                    {
                        id: 2,
                        name: "Ervin Howell",
                        email: "Shanna@melissa.tv",
                        avatar: '',
                        phone: "010-692-6593 x09125",
                    },
                    {
                        id: 3,
                        name: "Clementine Bauch",
                        email: "Nathan@yesenia.net",
                        avatar: '',
                        phone: "1-463-123-4447",
                    },
                    {
                        id: 4,
                        name: "Patricia Lebsack",
                        email: "Julianne.OConner@kory.org",
                        avatar: 'https://cdn.iconscout.com/public/images/icon/free/png-512/avatar-user-teacher-312a499a08079a12-512x512.png',
                        phone: "(254)954-1289",
                    },
                    {
                        id: 5,
                        name: "Chelsey Dietrich",
                        email: "Lucio_Hettinger@annie.ca",
                        avatar: 'https://cdn.iconscout.com/public/images/icon/free/png-512/avatar-user-teacher-312a499a08079a12-512x512.png',
                        phone: "(254)954-1289",
                    }
                ],
                searchUser: '',
                searchBy: '',
                btnSearch: true,
                paramsSearch: [
                    {nameParam: 'name', value: 1},
                    {nameParam: 'email', value: 2}
                ],
            };
        },
        watch: {
            searchBy: function () {
                if (this.searchBy.length > 0) {
                    this.btnSearch = false;
                }
            }
        },
        methods: {
            createUser(newUser) {
                // console.log(newUser);
                // console.log("Create User Method");
                this.people.push(newUser);
                sweetalert('Success!', 'New User created!', 'success');
            },
            filterUser() {
                const searchBy = this.searchBy;
                console.log(searchBy);
                const searchUser = this.searchUser;
                // if(searchBy){
                //     this.btnSearch = false;
                // }
                if (searchBy === 'name') {
                    this.people = this.people.filter(function (findUser) {
                        return findUser.name.indexOf(searchUser) > -1;
                    });
                }
                if (searchBy === 'email') {
                    this.people = this.people.filter(function (findUser) {
                        return findUser.email.indexOf(searchUser) > -1;
                    });
                }
            },
        }
        ,
    }
    ;
</script>

<style>
    #app {
        font-family: "Avenir", Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    .search_panel{
        border-bottom: 1px solid #174c73;
        padding-bottom: 10px;
    }
    .search_input{
        margin-bottom: 20px;
    }

    .search_select{
        margin-bottom: 20px;
    }

</style>
