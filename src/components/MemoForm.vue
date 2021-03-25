<template>
  <div class="memo-form">
    <form @submit.prevent="addMemo">
      <fieldset>
        <div>
          <input
            class="memo-form__title-form"
            type="text"
            v-model="title"
            placeholder="메모의 제목을 입력해주세요."
          />
          <textarea
            class="memo-form__content-form"
            type="text"
            v-model="content"
            placeholder="메모의 내용을 입력해주세요."
          />
          <button type="reset"><i class="fas fa-sync-alt"></i></button>
          <div class="btn_wrap">
            <button type="submit">등록하기</button>
          </div>
        </div>
      </fieldset>
    </form>
  </div>
</template>

<script>
export default {
  name: "MemoForm",
  data() {
    return {
      title: "",
      content: "",
    };
  },
  methods: {
    resetFields() {
      this.title = "";
      this.content = "";
    },
    addMemo() {
      const { title, content } = this;
      const id = new Date().getTime();

      const isEmpty = title.length <= 0 || content.length <= 0;
      if (isEmpty) {
        return false;
      }
      this.$emit("addMemo", { id, title, content });
      this.resetFields();
    },
  },
};
</script>

<style lang="scss" scoped>
.memo-form {
  margin-bottom: 24px;
  padding-bottom: 40px;
  border-bottom: 1px solid #eee;
  form {
    fieldset {
      > div {
        position: relative;
        padding: 24px;
        margin-bottom: 20px;
        box-shadow: 0 4px 10px -4px rgba($color: #000000, $alpha: 0.2);
        background-color: #fff;
        input,
        textarea {
          padding: 5px;
          border: 1px solid rgba($color: #000000, $alpha: 0.2);
        }
        button[type="reset"] {
          position: absolute;
          bottom: 100px;
          right: 25px;
          font-size: 16px;
          background: none;
        }
        .btn_wrap {
          position: relative;
          width: 150px;
          height: 50px;
          margin: 50px auto 10px;
          button[type="submit"] {
            width: 100%;
            padding: 12px 18px 12px 0;
            border-radius: 5px;
            background-color: rgb(245, 88, 114);
            color: #fff;
            font-size: 16px;
          }
        }
      }
      .memo-form__title-form {
        width: 100%;
        margin-bottom: 12px;
        font-size: 16px;
        line-height: 26px;
      }
      .memo-form__content-form {
        width: 100%;
        height: 200px;
        font-size: 14px;
        line-height: 22px;
        vertical-align: top;
      }
    }
  }
  input:focus {
    outline: none;
  }
}
</style>