<template>
    <!--
  This example requires some changes to your config:
  
  ```
  // tailwind.config.js
  module.exports = {
    // ...
    plugins: [
      // ...
      require('@tailwindcss/forms'),
    ],
  }
  ```
-->
    <!--
  This example requires updating your template:

  ```
  <html class="h-full bg-white">
  <body class="h-full">
  ```
-->
    <div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
        <div class="sm:mx-auto sm:w-full sm:max-w-sm">
            <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">Login</h2>
        </div>

        <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
            <form @submit.prevent="enter()" class="space-y-6" action="#" method="POST">
                <div>
                    <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Username</label>
                    <div class="mt-2">
                        <input v-model="username" id="email" name="email" type="text" autocomplete="email" required
                            class="pl-[20px] block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6">
                    </div>
                </div>

                <div>
                    <div class="flex items-center justify-between">
                        <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Password</label>
                    </div>
                    <div class="mt-2">
                        <input v-model="password" id="password" name="password" type="password"
                            autocomplete="current-password" required
                            class="pl-[20px] block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6">
                    </div>
                </div>

                <div>
                    <button type="submit"
                        class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Enter</button>
                </div>
            </form>

        </div>
    </div>
</template>

<script>
import axios from "axios"
export default {
    data() {
        return {
            password: "",
            username: "",
        }
    },
    methods: {
        async enter() {
            // {
            //     id: "teacher:1",
            //     username: "fits",
            //     password: "123",
            // }
            // console.log(this.password);
            // console.log(this.username);
            let teachers = []
            await axios.get("https://654df66acbc3253557422903.mockapi.io/users")
                .then(response => teachers = response.data)

            for (let i of teachers) {
                console.log(i);
                if (i.username == this.username && i.password == this.password) {
                    window.localStorage.user = JSON.stringify(i)
                    window.localStorage.login = true
                    import.meta.env.VITE_LOGIN = true
                    this.$router.push("/")
                }
            }
            // axios.post("https://654df66acbc3253557422903.mockapi.io/users",
            //     {
            //         "id": "2",
            //         "username": "khakim",
            //         "password": "2003"
            //     })

            // axios.post("https://654df66acbc3253557422903.mockapi.io/groups",
            // {
            //     idd: "teacher:2",
            //     groupId: '-972180657',
            //     groupname: "14:00",
            //     students: [
            //       {
            //         studentId: 122,
            //         studentname: "Салохиддин"
            //       },
            //       {
            //         studentId: 32,
            //         studentname: "Гавхар"
            //       },
            //       {
            //         studentId: 33,
            //         studentname: "Дарья"
            //       },
            //       {
            //         studentId: 44,
            //         studentname: "Лола"
            //       },
            //       {
            //         studentId: 44,
            //         studentname: "Абдусаллох"
            //       },
            //       {
            //         studentId: 44,
            //         studentname: "О.Давлатбек"
            //       },
            //       {
            //         studentId: 44,
            //         studentname: "Х.Давлатбек"
            //       },
            //       {
            //         studentId: 44,
            //         studentname: "Сардорбек"
            //       },
            //       {
            //         studentId: 44,
            //         studentname: "Зафар"
            //       },
            //     ],
            // })

        }
    }
}
</script>

<style></style>