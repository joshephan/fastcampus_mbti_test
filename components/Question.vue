<template>
  <div>
    <h1>{{page}}. {{question}}</h1>
    <Button
      v-for="(item, index) in answers"
      styleType="blue"
      :key="index"
      :text="item.text"
      :clickEvent="() => {
        clickButton(item);
      }"
    />
    <Progress />
  </div>
</template>
<script>
export default {
  computed: {
    page() {
      return this.$store.state.page;
    },
    question() {
      return this.$store.state.questions[this.$store.state.page - 1].q;
    },
    answers() {
      return this.$store.state.questions[this.$store.state.page - 1].a;
    }
  },
  methods: {
    clickButton(item) {
      this.$store.dispatch("clickButton", item.value);

      // 마지막 질문일 때만 라우터 이동
      if (this.page === this.$store.state.questions.length) {
        const result = this.$store.state.result;
        this.$router.push({
          name: "result-mbti",
          params: {
            mbti: `${result.e ? "e" : "i"}${result.s ? "s" : "n"}${
              result.f ? "f" : "t"
            }${result.p ? "p" : "j"}`
          }
        });
      }
    }
  }
};
</script>
<style>
</style>
