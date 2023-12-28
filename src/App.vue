<template>
  <div id="app">
    <h1>Barzelletta di Natale</h1>
    <p v-if="joke">{{ joke.question }}</p>
    <p v-if="joke">{{ joke.answer }}</p>
    <button @click="getJoke">Ottieni una nuova barzelletta</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      joke: null
    };
  },
  methods: {
    async getJoke() {
      // Try Block: Tutte le istruzioni all'interno del blocco try vengono eseguite normalmente. Quindi, sto cercando di effettuare una richiesta Axios per ottenere una barzelletta di Natale.
      try {
        // La keyword await viene utilizzata in JavaScript all'interno di funzioni asincrone (async) per attendere che una Promise venga risolta o rifiutata. Nello specifico, await axios.get sta aspettando che la richiesta HTTP effettuata con Axios venga completata e che la Promise associata a tale richiesta venga risolta.
        // Quando si esegue una richiesta HTTP, come ad esempio axios.get, questa restituirà una Promise che rappresenta il risultato della richiesta. Utilizzando await, dico al programma di attendere che questa Promise si risolva prima di procedere con l'esecuzione del codice successivo. In altre parole, l'esecuzione del codice viene messa in pausa fino a quando la richiesta HTTP non è stata completata e la Promise restituita è stata risolta.
        const response = await axios.get("https://christmascountdown.live/api/joke");
        this.joke = response.data;
      } catch (error) { // Catch Block: Se si verifica un errore nel blocco try, l'esecuzione del codice nel blocco try viene interrotta, e il controllo passa al blocco catch. Il parametro error in catch (error) conterrà l'oggetto errore che è stato generato.
        console.error("Errore durante il recupero della barzelletta:", error);
      }
    }
  },
  mounted() {

    this.getJoke();
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

button {
  padding: 10px 20px;
  margin-top: 20px;
  cursor: pointer;
}
</style>