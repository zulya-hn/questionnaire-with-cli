<template>
    <div>
      
        <h3>Right answers:</h3>
        
        <div v-for="(question, questIndex) in info">
          <br>
          <span class="mt-5 mb-3">
                    {{ (questIndex + 1) + ') ' + question.text }}
                </span>
          <br>
          <span v-for="corVar in question.correctVariants"
                class="form-check correct">
                    {{ question.variants[corVar] }}
                </span>
        </div>
        
        <hr>
        
        <h3>Your answers:</h3>
      
        <div v-for="(question, questIndex) in info">
          <br>
          <span class="mt-5 mb-3">
                {{ (questIndex + 1) + ') ' + question.text }}
            </span>
          <br>
          <span class="mt-5 mb-3"
                  :class="correctOrWrong(index, question.correctVariants)"
                  v-for="(variant, index) in answers[questIndex]">
                {{ variant }}
            </span>
        </div>
  
    </div>
</template>

<script>
    export default {
        props: {
            'answers': Array,
            'info': Array,
        },
        computed: {
        
        },
        methods: {
            correctOrWrong(userAnswer, correctAnswers) {
                return correctAnswers.includes(userAnswer) ? 'correct' : 'wrong';
            }
        }
    };
</script>

<style scoped>
  
  .correct {
    color: #4CAE4C;
  }
  
  .wrong {
    color: red;
  }
  

</style>
