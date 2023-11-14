<script>
import axios from 'axios';
export default {
  data() {
    return {
      user: JSON.parse(window.localStorage.user),
      grp: []
    }
  },
  methods: {
    async ungroup() {
      let a = []
      await axios.get("https://654df66acbc3253557422903.mockapi.io/groups")
        .then(response => a = response.data)

      for (let i of a) {
        if (i.idd.split(":")[1] == this.user.id) {
          this.grp.push(i)
        }
      }
    },
    enter(item) {
      window.localStorage.group = JSON.stringify(item)
      this.$router.push("/group/" + item.groupId)
    }
  },
  created() {
    this.ungroup()

  }
}
</script>

<template>
  <main>

    <div class="navbar bg-base-100">
      <div class="flex-1">
        <a class="btn btn-ghost normal-case text-xl">{{ this.user.username }}</a>
      </div>
      <div class="flex-none">

        <details class="dropdown">
          <summary class="m-1 btn btn-primary"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
              stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
              <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
            </svg>
          </summary>
          <ul class="p-2 absolute right-[0] shadow menu dropdown-content z-[1] bg-base-100 rounded-box w-52">
            <li @click="this.$router.push('/auth')">
              <b class="text-[17px]">Leave</b>
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                stroke="currentColor" class="w-6 h-6 text-[black]">
                <path stroke-linecap="round" stroke-linejoin="round"
                  d="M15.75 9V5.25A2.25 2.25 0 0013.5 3h-6a2.25 2.25 0 00-2.25 2.25v13.5A2.25 2.25 0 007.5 21h6a2.25 2.25 0 002.25-2.25V15m3 0l3-3m0 0l-3-3m3 3H9" />
              </svg>

            </li>
            <li>
              <b class="text-[17px]">Add Group</b>
            </li>
          </ul>
        </details>
      </div>
    </div>

    <div class="px-[20px]">
      <div class="overflow-x-auto">
        <table class="table table-zebra">
          <!-- head -->
          <thead>
            <tr>
              <th></th>
              <th>Group</th>
              <th class="text-right">Quantity</th>
            </tr>
          </thead>
          <tbody>
            <!-- row 1 -->
            <tr @click="enter(item)" v-for="item of this.grp" :key="item.id">
              <th> {{ this.grp.indexOf(item) + 1 }} </th>
              <td> {{ item.groupname }} </td>
              <td class="text-right">{{ item.students.length }}</td>
            </tr>
            <!-- row 2 -->

          </tbody>
        </table>
      </div>
    </div>

  </main>
</template>
