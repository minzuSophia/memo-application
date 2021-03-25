<template>
  <div class="memo-app">
    <memo-form @addMemo="addMemo" />
    <ul class="memo-list">
      <memo
        v-for="memo in memos"
        :key="memo.id"
        :memo="memo"
        @deleteMemo="deleteMemo"
        @updateMemo="updateMemo"
      />
    </ul>
  </div>
</template>

<script>
import Memo from "./Memo.vue";
import MemoForm from "./MemoForm.vue";
export default {
  name: "MemoApp",
  data() {
    return {
      memos: [],
    };
  },
  created() {
    this.memos = localStorage.memos ? JSON.parse(localStorage.memos) : [];
  },
  components: { MemoForm, Memo },
  methods: {
    addMemo(payload) {
      this.memos.push(payload);
      this.storeMemo();
    },
    storeMemo() {
      const memoToString = JSON.stringify(this.memos);
      localStorage.setItem("memos", memoToString);
    },
    deleteMemo(id) {
      const tartgetIndex = this.memos.findIndex((v) => v.id === id);
      this.memos.splice(tartgetIndex, 1);
      this.storeMemo();
    },
    updateMemo(payload) {
      const { id, content } = payload;
      const tartgetIndex = this.memos.findIndex((v) => v.id === id);
      const targetMemo = this.memos[tartgetIndex];
      this.memos.splice(tartgetIndex, 1, { ...targetMemo, content });
      this.storeMemo();
    },
  },
};
</script>

<style lang="scss" scoped>
.memo-app {
  display: flex;
  align-items: start;
  justify-content: center;
  width: 100%;
  margin: 0 auto;
  padding: 20px 0;
  .memo-list {
    margin: 0 0 10px;
  }
}
</style>