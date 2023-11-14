<template>
    <div class="p-[10px]">
        <div class="flex justify-between">
            <div class="flex items-center">
                <button @click="this.$router.push('/')" class="btn-primary btn text-white">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 19.5L8.25 12l7.5-7.5" />
                    </svg>

                </button>
                <!-- Open the modal using ID.showModal() method -->
                <button class="btn btn-primary ml-[10px]" onclick="my_modal_1.showModal()">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round"
                            d="M21.75 6.75v10.5a2.25 2.25 0 01-2.25 2.25h-15a2.25 2.25 0 01-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25m19.5 0v.243a2.25 2.25 0 01-1.07 1.916l-7.5 4.615a2.25 2.25 0 01-2.36 0L3.32 8.91a2.25 2.25 0 01-1.07-1.916V6.75" />
                    </svg>

                </button>
                <dialog id="my_modal_1" class="modal">
                    <div class="modal-box">
                        <h3 class="font-bold text-lg">Send Message</h3>
                        <textarea placeholder="Write something" class="border border-[silver] outline-none caret-primary p-[10px] text-primary sendmessage_send font-[600] border-solid w-[100%] mt-[20px] rounded-[10px] h-[150px]" type="text"> </textarea>
                        <div class="modal-action">
                            <form method="dialog" class="w-[100%]">
                                <!-- if there is a button in form, it will close the modal -->
                                <button @click="sendMEssage()" class="btn btn-primary w-[100%]">Send</button>
                            </form>
                        </div>
                    </div>
                </dialog>
            </div>
            <div>
                <span class="mr-[10px]">Chat ID</span>
                <input :value="this.grp.groupId" class="chatId_send bg-[#11111] btn outline-none caret-black w-[120px]"
                    type="text">
            </div>
        </div>
        <div class="flex justify-between mt-[40px] mb-[20px]">
            <h1 class="text-[20px] font-[1000]">{{ this.user.username }}</h1>
            <h2 class="text-[20px] font-[1000] text-primary">{{ this.grp.groupname }}</h2>
            <div v-if="!this.editMode" @click="this.editMode = true"
                class="bg-primary flex items-center justify-center rounded-[8px] w-[30px] h-[30px]">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="w-6 h-6 text-white">
                    <path stroke-linecap="round" stroke-linejoin="round"
                        d="M10.5 6h9.75M10.5 6a1.5 1.5 0 11-3 0m3 0a1.5 1.5 0 10-3 0M3.75 6H7.5m3 12h9.75m-9.75 0a1.5 1.5 0 01-3 0m3 0a1.5 1.5 0 00-3 0m-3.75 0H7.5m9-6h3.75m-3.75 0a1.5 1.5 0 01-3 0m3 0a1.5 1.5 0 00-3 0m-9.75 0h9.75" />
                </svg>

            </div>
            <div v-if="this.editMode" @click="this.editMode = false"
                class="bg-success flex items-center justify-center rounded-[8px] w-[30px] h-[30px]">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="w-6 h-6 text-white">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M4.5 12.75l6 6 9-13.5" />
                </svg>


            </div>
        </div>
        <div>
            <div class="overflow-x-auto">
                <table class="table">
                    <!-- head -->
                    <thead>
                        <tr>
                            <th>Name</th>
                            <th>Graduate</th>
                            <th v-if="!this.editMode">ATD</th>
                            <th v-if="this.editMode">Delete</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- row 1 -->
                        <tr v-for="item of this.grp.students" :key="item.id">
                            <td>
                                <p>{{ this.grp.students.indexOf(item) + 1 }}.<span class="names_send">{{ item.studentname
                                }}</span></p>
                                <div class="mt-[10px] w-[80px] result_send">
                                    <output>100</output>
                                    /
                                    <output>50</output>
                                    <output>🟩</output>
                                </div>
                            </td>
                            <td>
                                <input
                                    oninput="this.parentElement.previousElementSibling.children[1].children[0].value = this.value; (+event.target.parentElement.previousElementSibling.children[1].children[1].value + +event.target.parentElement.previousElementSibling.children[1].children[0].value) >= 150 ? event.target.parentElement.previousElementSibling.children[1].children[2].innerHTML = '🟩': event.target.parentElement.previousElementSibling.children[1].children[2].innerHTML = '🟥'"
                                    type="range" min="0" max="100" value="100" class="range range-primary" step="10" />
                                <div class="w-full flex justify-between text-xs px-2 ">
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                </div>
                                <input
                                    oninput="this.parentElement.previousElementSibling.children[1].children[1].value = this.value; (+event.target.parentElement.previousElementSibling.children[1].children[1].value + +event.target.parentElement.previousElementSibling.children[1].children[0].value) >= 150 ? event.target.parentElement.previousElementSibling.children[1].children[2].innerHTML = '🟩': event.target.parentElement.previousElementSibling.children[1].children[2].innerHTML = '🟥'"
                                    type="range" min="0" max="100" value="50" class="range range-success" step="10" />
                                <div class="w-full flex justify-between text-xs px-2 ">
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                    <span>|</span>
                                </div>
                            </td>
                            <td v-if="this.editMode">
                                <button class="btn bg-[red] text-white h-[100px]">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                        stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                                        <path stroke-linecap="round" stroke-linejoin="round"
                                            d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
                                    </svg>

                                </button>
                            </td>
                            <td v-if="!this.editMode">
                                <input type="checkbox"
                                    onchange="this.checked ?  parentNode.parentNode.style.background = 'transparent': parentNode.parentNode.style.background = 'rgb(236, 71, 71)'"
                                    checked="checked" class="checkbox attendance_send checkbox-primary" />
                            </td>
                        </tr>
                        <tr v-if="this.editMode">
                            <th colspan="3">
                                <div
                                    class="btn w-[100%] h-[100%] w-[100%] bg-primary p-[10px] rounded-[10px] flex justify-center">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="3"
                                        stroke="currentColor" class="w-6 h-6 text-white">
                                        <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
                                    </svg>
                                </div>

                            </th>
                        </tr>
                        <tr @click="send()" v-if="!this.editMode">
                            <th colspan="3">
                                <div
                                    class="btn w-[100%] h-[100%] w-[100%] bg-primary p-[10px] rounded-[10px] text-white flex justify-center">
                                    Send
                                </div>

                            </th>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios"
export default {
    data() {
        return {
            editMode: false,
            grp: JSON.parse(window.localStorage.group),
            user: JSON.parse(window.localStorage.user),
        }
    },
    methods: {
        sendMEssage(){
            let chatId_send = document.querySelector(".chatId_send")
            let a = document.querySelector(".sendmessage_send").value
            console.log(a);
            axios.post(`https://api.telegram.org/bot6555827924:AAHA1P6I6pNUk-r6OzzeQ8PlALtbw9xS_Fw/sendMessage?chat_id=${chatId_send.value}&text=${a}`)
        },
        send() {


            let getDate = new Date()
            let message = `Результаты ${getDate.getDate()}.${getDate.getMonth() + 1}.${getDate.getFullYear()} %0A`

            let chatId_send = document.querySelector(".chatId_send")
            let names_send = document.querySelectorAll(".names_send")
            let result_send = document.querySelectorAll(".result_send")
            let attendance_send = document.querySelectorAll(".attendance_send")


            for (let i = 0; i < this.grp.students.length; i++) {
                if (!attendance_send[i].checked) {
                } else {
                    message += `${names_send[i].innerHTML} - ${result_send[i].children[1].innerHTML}/${result_send[i].children[0].innerHTML} ${result_send[i].children[2].innerHTML} %0A`
                }

            }
                axios.post(`https://api.telegram.org/bot6555827924:AAHA1P6I6pNUk-r6OzzeQ8PlALtbw9xS_Fw/sendMessage?chat_id=${chatId_send.value}&text=${message}`)

        }
    },
    mounted() {
        console.log(this.grp);
    }
}
</script>

<style></style>