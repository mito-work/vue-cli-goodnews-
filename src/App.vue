<template>
  <div id="app">
    <h1>🎉Post Good News of the week🎉</h1>
    <FormItem @input-item="inputParentsItem($event)" />
    <List :postList="postList" @delete-item="deletParentItem($event)" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import FormItem from "./components/Form.vue";
import List from "./components/List.vue";
import { Post } from "./newsItem";

@Component({
  components: {
    FormItem,
    List,
  },
})
export default class App extends Vue {
  postList = [
    {
      id: 0,
      description: "新し靴を買ったこと",
    },
    {
      id: 1,
      description: "早起きできた",
    },
  ];

  inputParentsItem($event: string): void {
    const post: Post = { id: Date.now(), description: $event };
    this.postList.push(post);
  }
  deletParentItem($event: number): void {
    this.postList = this.postList.filter((val) => {
      return val.id != $event;
    });
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;

  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
button {
  border: none;
  border-radius: 8px;
  padding: 0.7rem 1.2rem;
  font-size: 1rem;
  font-weight: 500;
}
</style>
