<template>
  <div>
    <h3>Right answers:</h3>

    <div v-for="(question, questIndex) in info" :key="`quest-${questIndex}`">
      <br />
      <span class="mt-5 mb-3">
        {{ questIndex + 1 + ") " + question.text }}
      </span>
      <br />
      <span
        v-for="(corVar, corVarIndex) in question.correctVariants"
        class="form-check correct"
        :key="`corvar-${corVarIndex}`"
      >
        {{ question.variants[corVar] }}
      </span>
    </div>

    <hr />

    <h3>Your answers:</h3>

    <div v-for="(question, questIndex) in info" :key="`question-${questIndex}`">
      <br />
      <span class="mt-5 mb-3">
        {{ questIndex + 1 + ") " + question.text }}
      </span>
      <br />
      <span
        class="mt-5 mb-3"
        v-for="(variant, variantNumber) in answers[questIndex]"
        :key="`variant-${variantNumber}`"
        :class="correctOrWrong(variantNumber, question.correctVariants)"
      >
        {{ variant }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    answers: Array,
    info: Array,
  },
  computed: {},
  methods: {
    correctOrWrong(userVariant, correctVariants) {
      return correctVariants.includes(userVariant) ? "correct" : "wrong";
    },
  },
};
</script>

<style scoped>
.correct {
  color: #4cae4c;
}

.wrong {
  color: red;
}
</style>
