<template>
  <li class="memo-item">
    <p>{{ memo.id }}</p>
    <strong>{{ memo.title }}</strong>
    <p @dblclick="handleDblClick">
      <template v-if="!isEditing">{{ memo.content }}</template
      ><input
        v-else
        type="text"
        ref="content"
        :value="memo.content"
        @keydown.enter="updateMemo"
      />
    </p>
    <button type="button" @click="deleteMemo">
      <i class="fas fa-times"></i>
    </button>
  </li>
</template>

<script>
export default {
  name: "Memo",
  data() {
    return {
      isEditing: false,
    };
  },
  props: {
    memo: {
      type: Object,
    },
  },
  beforeUpdate() {
    console.log("beforeUpdate =>", this.$refs.content);
  },
  updated() {
    console.log("update =>", this.$refs.content);
  },
  methods: {
    deleteMemo() {
      const id = this.memo.id;
      this.$emit("deleteMemo", id);
    },
    handleDblClick() {
      this.isEditing = true;
      this.$nextTick(() => {
        this.$refs.content.focus();
      });
    },
    updateMemo(e) {
      const id = this.memo.id;
      const content = e.target.value.trim();
      if (content.length <= 0) {
        return false;
      }
      this.$emit("updateMemo", { id, content });
      this.isEditing = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.memo-item {
  width: 300px;
  overflow: hidden;
  position: relative;
  margin-bottom: 20px;
  padding: 20px;
  box-shadow: 0 4px 10px -4px rgba($color: #000000, $alpha: 0.2);
  background-color: #fff;
  list-style: none;
  button {
    background: none;
    position: absolute;
    right: 20px;
    top: 20px;
    font-size: 20px;
    color: #e5e5e5;
    border: 0;
  }
  strong {
    display: block;
    margin-bottom: 12px;
    font-size: 18px;
    font-weight: normal;
    word-break: break-all;
  }
  p {
    margin: 0;
    font-size: 14px;
    line-height: 22px;
    color: #666;
    input[type="text"] {
      box-sizing: border-box;
      width: 100%;
      padding: 3px 0;
      font-size: inherit;
      border: 1px solid rgba(0, 0, 0, 0.2);
    }
  }
}
</style>