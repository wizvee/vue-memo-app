<template>
  <div class="memo-form">
    <form @submit.prevent="addMemo" @reset="resetFields">
      <fieldset>
        <div>
          <input
            v-model="title"
            type="text"
            class="memo-form__title-form"
            placeholder="메모의 제목을 입력해주세요."
          />
          <textarea v-model="content" class="memo-form__content-form" placeholder="메모의 내용을 입력해주세요."></textarea>
          <button type="reset">
            <i class="fa fa-sync-alt" aria-hidden="true"></i>
          </button>
        </div>
        <button type="submit">등록하기</button>
      </fieldset>
    </form>
  </div>
</template>

<script>
export default {
  name: 'memoForm',
  data() {
    return {
      // 사용자가 입력할 제목과 콘텐츠가 저장될 state
      title: '',
      content: ''
    };
  },
  methods: {
    resetFields() {
      this.title = '';
      this.content = '';
    },
    addMemo() {
      const { title, content } = this;
      // const id = new Date().getTime();
      // 제목이나 내용을 입력하지 않았을 경우
      const isEmpty = [title.trim(), content.trim()].includes('');
      if (isEmpty) return;
      // addMemo 이벤트를 발생
      // this.$emit('addMemo', { id, title, content });
      this.$emit('addMemo', { title, content });
      // 메모 등록 후 내용 초기화
      this.resetFields();
    }
  }
};
</script>

<style scoped>
.memo-form {
  margin-bottom: 24px;
  padding-bottom: 40px;
  border-bottom: 1px solid #eee;
}
.memo-form form fieldset div {
  position: relative;
  padding: 24px;
  margin-bottom: 20px;
  box-shadow: 0 4px 10px -4px rgba(0, 0, 0, 0.2);
  background: #fff;
}
.memo-form form fieldset div button[type='reset'] {
  position: absolute;
  right: 20px;
  bottom: 20px;
  font-size: 16px;
  background: none;
}
.memo-form form fieldset button[type='submit'] {
  float: right;
  width: 96px;
  padding: 12px 0;
  border-radius: 4px;
  background: #ff5a00;
  color: #fff;
  font-size: 16px;
}
.memo-form form fieldset .memo-form__title-form {
  width: 100%;
  margin-bottom: 12px;
  font-size: 18px;
  line-height: 26px;
}
.memo-form form fieldset .memo-form__content-form {
  width: 100%;
  height: 66px;
  font-size: 14px;
  line-height: 22px;
  vertical-align: top;
}
.memo-form input:focus,
.memo-form textarea {
  outline: none;
}
</style>