<template>
  <div class="hello">
    <!--
      cette prop msg est donnée dans App.vue
    -->
    <h1>{{ msg }}</h1>
    <!--
      la directive v-if permet d'afficher l'élement en fonction du booléen
      tout ce qui commence par v- est fourni et géré par vuejs
    -->
    <div id="counter" v-if="test">
      un titre!!
    </div>
    <!--
      le v-bind: (raccourci en : ) permet d'utiliser les propriétés vuejs
      dans l'attribut class, on peut ainsi conditionner une classe à une variable vuejs
      on peut garder l'attribut class HTML avec un :class de vuejs
    -->
    <div id="counter" v-bind:class="{hide: test}">
      un autre titre!!
    </div>
    <!-- 
      différence entre v-model et :value =>
      l'élement avec v-model peut changer la valeur de test ou model,
      l'élement avec le :value ne fait que récupérer la valeur de base
    -->
    <input type="checkbox" v-model="test">
    <input type="checkbox" :value="test">
    <br>
    {{model}}
    <input type="text" v-model="model">
    <br>
    {{valeur}}
    <input type="text" :value="valeur">
    <br>
    pour modifier la valeur : 
    <input type="text" v-model="valeur">
    <br>


    <input type="text" v-model="text">
    <!--
      le @ remplace un v-on: qui sert à gérer les évenements.
    -->
    <button @click="newElement" >
      add element to list
    </button>
    <ul>
      <!--
        le module list à été créé dans le fichier list.vue et importé dans ce module
        le v-for récupère ici l'élément item et son index key dans le tableau theList
        le v-for affiche l'élément dont il est l'attribut autant de fois qu'il à d'objets
        le v-for nécéssite un :key qui sera une clé unique pour chaque élément du v-for
      -->
      <list v-for="(item, key) in theList" :key="key" :msg="item.text" @remove="removeRow(key)"></list>
      <!--
        on passe la props msg au module list avec comme valeur le text contenu dans l'élément item
        le @remove attends l'émission d'un évènement remove de la part du module (voir le fichier list.vue)

      -->
    </ul>

  </div>
</template>

<script>
// import du sous-module list
import list from './list.vue'

//! export du module helloworld pour qu'il soit réutilisé dans un module parent (c'est la base de vuejs)
export default {
  //nom du module
  name: 'HelloWorld',
  //paramètres pouvant êtres passés au module
  props: {
    msg: String
  },
  // variables du module
  data() {
    return {
      test: false,
      theList: [
        {text: 'test'},
        {text: 'test1'},
        {text: 'test2'},
        {text: 'test3'},
        {text: 'test4'}
      ],
      text: "",
      model: "avec v-model",
      valeur: "avec :value"
    }
  },
  // sopus-modules inclus dans le module
  components: {
    list
  },
  //méthodes du module
  methods: {
    newElement() {
      // le this se rapporte au component, le $data aux variables.
      this.$data.theList.push({text: this.$data.text})
      this.$data.text = ""
    },
    removeRow(removedId) {
      // on retire un élément à partir de l'id removedId passé en paramètre
      this.$data.theList.splice(removedId,1)
    }
  }
}
</script>

<!-- le scoped permet au CSS de n'être appliqué que dans ce module et ses sous modules (voir li) -->
<style scoped>
li {
  margin: 0 10px;
  color: red;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
a {
  color: #42b983;
}
.hide {
  display: none;
}
</style>
