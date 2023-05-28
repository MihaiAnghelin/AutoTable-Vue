<template>
  <div class="loggedpageContainer">
    <div class="buttonsContainer">
      <div class="bContainer">
        <el-button round @click="toggleMethod">Toggle</el-button>
      </div>
      <div class="bContainer">
        <el-button round @click="statusMethod">Status</el-button>
        <div v-if="this.status" class="statusContainer">
          <p style="color: ">STATUS: {{ this.statusData }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      status: false,
      statusData: "a",
    };
  },
  methods: {
    statusHandler() {
      this.status = !this.status;
    },
    async toggleMethod() {
      try {
        const token = localStorage.getItem("token");
        const response = await axios.get(
          "https://api-autotable.mihaianghelin.ro/api/table/toggle",
          {
            headers: {
              Authorization: `Bearer ${token}`,
            },
          }
        );
        console.log(response.data);
      } catch (e) {
        console.log(e);
      }
    },
    async statusMethod() {
      try {
        this.statusHandler();
        const token = localStorage.getItem("token");
        const response = await axios.get(
          "https://api-autotable.mihaianghelin.ro/api/table/status",
          {
            headers: {
              Authorization: `Bearer ${token}`,
            },
          }
        );
        this.statusData = response.data
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>
