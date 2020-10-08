<template>
  
  <div v-if="questIndex === currentQuestion">
    <h4 class="mt-5 mb-3">
      {{ question.text }}
    </h4>
    
    <div v-for="(variant, varNum) in question.variants"
         class="form-check">
      <label class="form-check-label">
        <input class="form-check-input"
               :type="question.type"
               :value="answers[questIndex]"
               :name="questIndex"
               @click="chooseAnswer(variant, varNum)"
        >
        
        {{ variant }}
      
      </label>
    </div>
    
    <div class="mt-5">
      <button class="btn btn-primary"
              @click="toGoNext"
              :disabled="!isGoNext[questIndex]"
      >
        Дальше
      </button>
    </div>
  </div>
  
</template>

<script>
    export default {
        props: {
            'question': Object,
            'questIndex': Number,
            'currentQuestion': Number,
            'answers': Array,
            'isGoNext': Array,
        },
        methods: {
            chooseAnswer(variant, varNum) {
                this.$emit('choose-answer', {variant, varNum});
            },
            toGoNext() {
                this.$emit('go-next');
            }
        }
    };
</script>
