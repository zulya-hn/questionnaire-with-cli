<template>
  <div class="wrapper">
    <div class="sample">
      
      <template v-if="!formSubmitted">
        <app-questions v-for="(question, questIndex) in info"
                       :question="question"
                       :questIndex="questIndex"
                       :answers="answers"
                       :currentQuestion="currentQuestion"
                       :isGoNext="isGoNext"
                       :key="question.id"
                       @choose-answer="pushAnswer(questIndex, $event)"
                       @go-next="goNext">
        
        </app-questions>
      </template>
      
      <template v-else>
        <app-answers :answers="answers"
                     :info="info">
        </app-answers>
      </template>
    
    </div>
  </div>
</template>

<script>
    import AppQuestions from './components/Questions';
    import AppAnswers from './components/Answers';
    
    export default {
        data() {
            return {
                currentQuestion: 0,
                info: [
                    {
                        id: 101,
                        text: 'Какие из этих тегов строчные?',
                        variants: ['a', 'div', 'span', 'img'],
                        correctVariants: [0, 2],
                        type: 'checkbox',
                    },
                    {
                        id: 102,
                        text: 'Какой тег задаёт ссылку?',
                        variants: ['a', 'div', 'span', 'img'],
                        correctVariants: [0],
                        type: 'radio',
                    },
                ],
                answers: [],
                isGoNext: [],
            };
        },
        methods: {
            pushAnswer(questIndex, {variant, varNum}) {
                if (this.answers[questIndex] === undefined) {
                    this.answers[questIndex] = [];
                }
                
                if (this.info[questIndex].type === 'checkbox') {
                    
                    if (this.answers[questIndex][varNum] === undefined) {
                        this.answers[questIndex][varNum] = variant;
                        this.checkGoNext();
                        
                        return;
                    }
                    
                    this.answers[questIndex][varNum] = undefined;
                    this.checkGoNext();
                }
                
                if (this.info[questIndex].type === 'radio') {
                    this.answers[questIndex] = [];
                    this.answers[questIndex][varNum] = variant;
                    
                    this.checkGoNext();
                }
                
            },
            checkGoNext() {
                this.isGoNext = this.answers.map((variants) => {
                    return variants.length > 0;
                });
            },
            goNext() {
                this.currentQuestion++;
            },
        },
        computed: {
            formSubmitted: function () {
                return this.currentQuestion === this.info.length;
            }
        },
        components: {
            AppQuestions,
            AppAnswers
        }
    };
    
    /*
                 this.answers = [];
           =>
                 this.answers[0] = undefined
                 this.answers[1] = undefined
                 ...
                 this.answers[500] = undefined
                 
                 this.answers[0] = []
           =>
                 this.answers[0][0] = undefined
                 this.answers[0][1] = undefined
                 ...
                 this.answers[0][500] = undefined
                 
                 
                 this.answers[1][0]
                 this.answers[1][1]
                 this.answers[1][2]
                 
                 
                 this.answers[0][0] = div
                 this.answers[0][1] = span
                 =>
                 this.answers[0] = [div, span]
                 
                 this.answers[0] = []
                 =>
                 this.answers[0][0] = undefined
                 this.answers[0][1] = undefined
           */

</script>

<style scoped>
  .wrapper {
    max-width: 600px;
    margin: 20px auto;
  }

</style>
