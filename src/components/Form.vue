<template>
  <div class="l-container__form">
    <label for="post">今週のうれしかったことを共有してください</label>
    <input type="text" id="post" v-model="inputDescription" />
    <p v-if="limitInputCheck" class="p-alert">{{ limitInputCheck }}</p>
    <button type="button" class="p-btn-post" @click="inputItem" :disabled="disabled">Post</button>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Emit } from "vue-property-decorator";

@Component
export default class Form extends Vue {
  inputDescription = "";
  disabled = true;

  //emit
  @Emit("input-item")
  inputItem(): string {
    return this.inputDescription;
  }

  //computed
  get limitInputCheck(): string | null {
    if (this.inputDescription.length >= 20 || this.inputDescription.length <= 0) {
      this.disabled = true;
    } else {
      this.disabled = false;
    }
    return this.inputDescription.length >= 20 ? "20文字以内でお願いします😮" : "";
  }
}
</script>

<style scoped>
input[type="text"] {
  padding: 0.5rem;
  font-size: 1.5rem;
  width: 500px;
}
button:disabled {
  border: none;
  filter: opacity(0.4);
  cursor: not-allowed;
}
.l-container__form {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}
.p-btn-post {
  background-color: #f70a8d;
  color: #fff;
}
.p-alert {
  color: #f70a8d;
  font-weight: bold;
}
</style>
