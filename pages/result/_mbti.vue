<template>
  <main>
    <img :src="result[mbti].img" :alt="result[mbti].title" />
    <h1>{{result[mbti].title}}</h1>
    <p v-html="result[mbti].description"></p>
    <Button text="다시 테스트하기!" :clickEvent="resetPage" />
  </main>
</template>
<script>
export default {
  data() {
    return {
      mbti: null,
      result: {
        esfj: {
          img: "/esfj.jpeg",
          title: "솜사탕광 토니토니 쵸파",
          description: `밀집모자 해적단의 선의. 당신은 세상에 낫지 않는 병은 없다고 굳게 믿고 뭐든지 고칠 수 있는 의사가 되기 위해서 노력하는 쵸파를 닮았군요! 당신은 착한 마음 때문에 심지어 나쁜 적일찌라도 살리기 위해서 애씁니다.<br/><br/>당신의 따뜻함과 순수함은 세상에게 어쩌면 너무 깨끗할지도 모릅니다. 당신은 쉽게 다른 사람들에게 속임을 당하거나 배신을 경험하곤 합니다. 당신은 조용하고, 나서는 편은 아니지만 책임감이 강하고 맡은 일을 묵묵히 해냅니다. 남들에게 당신은 좋은 사람이지만 본인은 힘들 때가 많네요. 때로는 타인보다 자신을 보다듬어 준다면 그 누구보다 강한 사람이 될 겁니다.`
        }
      }
    };
  },
  created() {
    // this.mbti = this.$route.params.mbti;
    this.mbti = "esfj";

    // 예외 처리
    if (this.result[this.$route.params.mbti] === undefined) {
      this.$router.push({ name: "index" });
    }
  },
  methods: {
    resetPage() {
      this.$store.dispatch("clickResetButton");
      this.$router.push({ name: "index" });
    }
  }
};
</script>
<style>
</style>
