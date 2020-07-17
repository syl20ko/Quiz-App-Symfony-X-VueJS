<template>
  <div class="container pt-5">
    <div class="row justify-content-md-center mt-5">
      <div class="col-md-6">
        <div class="jumbotron pt-4 pb-4">
          <h2 style="color:blue" class="text-center">Un Quiz en Symfony et VueJs</h2>
          <hr />
          <div v-if="fin == false" show>
            <h5 class="text-center mb-2">{{questions[index].question}}</h5>
            <hr />
            <div class="list-group">
              <button
                type="button"
                class="list-group-item list-group-item-action text-center"
                v-for="(item, index) in questions[index].answers"
                :key="item.id"
                @click="action(index)"
              >{{ item }}</button>
            </div>
          </div>
          <button type="button"
              class="btn btn-primary btn-lg btn-block" v-if="voirReponse && !fin" @click="continuer">Continuer !</button>
          <div
            class="alert alert-info text-center"
            v-if="fin"
            show
          >Votre score est : {{ score }} / {{ questions.length }}</div>
          <div v-if="fin">
            <hr />
            <button
              type="button"
              class="btn btn-primary btn-lg btn-block"
              @click="recommencer"
            >Recommencer !</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data: function() {
    return {
      fin: false,
      index: 0,
      score: 0,
      variants: [...Array(4)],
      voirReponse: false,
      questions: [
        {
          question:
            "Quel révolutionnaire et grand orateur a déclaré en 1792 : “De l’audace, encore de l’audace, toujours de l’audace.”",
          answers: ["Desmoulin", "Danton", "Robespierre", "Saint Just"],
          ok: 1
        },
        {
          question: "Dans quel pays peut-on trouver le mont Elbrouz ?",
          answers: ["Russie", "Azerbaïdjan", "Géorgie", "Iran"],
          ok: 0
        },
        {
          question: "Qui a dit “Ich bin ein Berliner” ?",
          answers: ["Bismarck", "Reagan", "De Gaulle", "Kennedy"],
          ok: 3
        }
      ]
    };
  },
  methods: {
    action: function(index) {
    // Test bonne réponse
    if(index == this.questions[this.index].ok) {
      this.score++;
    } else {
      this.variants[index] = 'danger';
    }
    this.voirReponse = true;
    this.variants[this.questions[this.index].ok] = 'success';
    if(this.index == this.questions.length - 1) {
      this.fin = true;
    }
  },
    recommencer: function() {
    this.voirReponse = this.fin = this.index = this.score = 0;
    this.variants = [...Array(4)];
  },
    continuer: function() {
    this.voirReponse = false;
    this.variants = [...Array(4)];
    this.index++;  
  }
  }
};
</script>

<style>
</style>