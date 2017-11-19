<template>
  <v-app dark>
    <v-content>
      <v-container>
        <v-layout row justify-center >
          <v-flex md6 xs10>
            <v-card>
              <div v-if="userWon">
                <h1 justify-center>Wygrałeś Milion !</h1>
                <img src="./assets/urbanski_milionerzy.jpg" alt="" width="100%"></div>
              <v-card-title>{{ currentQuestion.title }}</v-card-title>
              <v-card-text>
                <v-list>
                <v-list-tile
                  v-for="(answer, answerIndex) in currentQuestion.answers"
                  :key="answerIndex"
                  @click="getAnswer(answerIndex)"
                  :class ="getMyClass(answerIndex)"
                >
                  {{ answer }}
                </v-list-tile>
                </v-list>
              </v-card-text>
              <v-card-actions>
                <v-btn
                  v-if="isUserCorrect && !userWon"
                  @click="nextQuestion"
                >Dobrze !  - przejdź do następnego pytania !</v-btn>
                <v-btn
                  v-else-if="userAnswer!=null"
                  @click="resetQuiz"
                >Rozwiąż quiz od początku</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
          <v-flex md3>
              <add-question @new-question="addQuestion($event)"></add-question>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
  import { quiz } from './quiz'
  import AddQueston from './components/AddQuestions.vue'

  export default {
    components:{'add-question': AddQueston},
    data () {
      return {
        quiz: quiz,
        currentIndex: 0,
        userAnswer: null,
        userWon: false,
      }
    },
    computed: {
      currentQuestion () {
        return this.quiz[this.currentIndex]
      },
      isUserCorrect() {
        return this.currentQuestion.correctAnswerIndex === this.userAnswer
      },
      isAllQuestions(){
        return quiz.length-1 === this.currentIndex;
      }
    },
    methods: {
      getAnswer ( answerIndex ) {
       if (this.userAnswer === null) {
          this.userAnswer = answerIndex
       }
      },
      getMyClass(answerIndex) {
        if (this.currentQuestion.correctAnswerIndex === answerIndex && answerIndex === this.userAnswer){
          if (this.isAllQuestions) {
            this.userWon = true
          }
          return 'success'
        }
        else if(answerIndex != this.currentQuestion.correctAnswerIndex && answerIndex === this.userAnswer){
          return 'error'
        }
        else{
          return 'secondary'
        }
      },
      nextQuestion(){
        this.userAnswer = null
        this.currentIndex++
      },
      resetQuiz(){
        this.userAnswer = null
        this.currentIndex = 0
        this.userWon = false
      },
      addQuestion(event){
        this.quiz(event);
        //unshift
      }
    }

  }
</script>

<style>

</style>
