<script lang="ts">
export default {
  name: "permissionButton"
};
</script>

<script setup lang="ts">
import { ref } from "vue";
import { storageSession } from "/@/utils/storage";
import { getToken } from "/@/utils/auth";

const auth = ref<boolean>(JSON.parse(getToken()).username || "admin"); //ref<boolean>(storageSession.getItem("info").username || "admin");

function changRole(value) {
  storageSession.setItem("info", {
    username: value,
    accessToken: `eyJhbGciOiJIUzUxMiJ9.${value}`
  });
  window.location.reload();
}
</script>

<template>
  <el-card>
    <template #header>
      <div class="card-header">
        <el-radio-group v-model="auth" @change="changRole">
          <el-radio-button label="admin" />
          <el-radio-button label="test" />
        </el-radio-group>
      </div>
    </template>
    <p v-auth="'v-admin'">只有admin可看</p>
    <p v-auth="'v-test'">只有test可看</p>
  </el-card>
</template>
