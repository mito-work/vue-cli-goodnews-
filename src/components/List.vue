<template>
  <div class="l-container__list">
    <!-- <ul>
      <li v-for="post in postList" :key="post.id">{{ post.id }}</li>
    </ul> -->
    <p v-if="postList.length <= 0">投稿お待ちしています～😉</p>
    <ul class="p-list">
      <li v-for="post in postList" :key="post.id">
        <p>{{ post.description }}</p>
        <button type="button" class="p-btn-delete" @click="deleteItem(post.id, post.description)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Emit, Prop } from "vue-property-decorator";
import { Post } from "../newsItem";

@Component
export default class List extends Vue {
  @Prop() postList!: Post[];

  @Emit("delete-item")
  deleteItem(id: number, description: string): number | null {
    if (confirm(`${description}を削除してよいですか？`)) {
      return id;
    }
    return null;
  }
}
</script>

<style scoped>
.p-btn-delete {
  padding: 0 2rem;
  background-color: rgb(128, 194, 233);
  color: #fff;
}
.p-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  gap: 0.5rem;
}
.p-list li {
  padding: 1rem 0.5rem;
  background-color: rgb(203, 240, 252);
  font-weight: bold;
  width: 500px;
  display: flex;
  justify-content: space-between;
}
</style>
