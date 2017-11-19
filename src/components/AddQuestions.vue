<template>
<v-dialog v-model="modalVisible">
  <v-btn slot="activator">Dodaj pytanie</v-btn>
  <v-card>
    <v-card-text>
      <v-text-field label="Treść pytania"
                    v-model="newQuestion"
      ></v-text-field>
      <v-text-field
        label="Odpowiedź 1"
        v-model="answer1"
      ></v-text-field>
      <v-text-field
        label="Odpowiedź 2"
        v-model="answer2"
      ></v-text-field>
      <v-text-field
        label="Odpowiedź 3"
        v-model="answer3"
      ></v-text-field>
      <v-text-field
        label="Indeks właściwej odpowiedzi"
        type="number"
        v-model="index"
      ></v-text-field>
    </v-card-text>
    <v-btn @click="addQuestion">Dodaj pytanie</v-btn>
    <v-btn @click="modalVisible = false ">Zamknij</v-btn>
  </v-card>
</v-dialog>
</template>

<script>
  export default {
    name: 'add-queston',
    data(){
      return{
        newQuestion:'',
        answer1:'',
        answer2:'',
        answer3:'',
        index:null,
        modalVisible:false
      }
    },
    computed:{
      normalizedQuestion(){
        return{
          title:this.newQuestion,
          answers:[this.answer1,this.answer2,this.answer3],
          correctAnswerIndex: +this.index
        }
      }
    },
    methods : {
      addQuestion(){
        this.$emit('new-question', this.normalizedQuestion)
      }
    }

  }
</script>
