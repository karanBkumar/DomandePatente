<template>
  <div id="ShowDomande" class="card border-2 border-dark mb-3" style="width: 25rem">
    <div class="d-flex justify-content-center bg-dark text-white">
      <Timer @inputChange="handleChange"/>
    </div>
    <div class="card-header bg-transparent border-2 border-dark" v-if="domande[numero].immagine != 'NA'">
      <img src="../assets/logo.png" class="card-img-top" />
    </div>
    <div class="card-body">
      <p class="card-text" v-html="domande[numero].domanda"></p>
    </div>
        <form @submit.prevent="NextDomanda()">
              <div class="card-footer bg-transparent border-2 border-dark">
               <div class="btn-group" role="group" aria-label="Basic mixed styles example">
                   <div class="row" id="TrueFalse">
                       <div class="col-6">
                            <button type="button" @click="rispostaAllaDomanda='V'" class="btn-lg btn-success" value="V">Vero</button>
                       </div>
                       <div class="col-6">
                            <button type="button" @click="rispostaAllaDomanda='F'" class="btn-lg btn-danger" value="F">Falso</button>
                       </div>
                   </div>
                </div>
              </div>
              <button type="submit" id="next" class="mt-2 mb-3 btn-lg btn-dark">Next</button>
              <br/>
              <small class="mt-2" id="errore" style="color:red;display:none">Selezionare una risposta</small>
        </form>
    <button @click="ShowRisTab" class="mt-3 btn btn-dark" id="mostraRis" style="display: none;">Sumbit</button>
  </div>
  <div class="row">
    <div class="mt-2 col-12" id="risultatoTabella" style="display:none;">
      <h1>Sei stato 
        <span style="color:red" v-if="risposteSbagliate.length>3">bocciato</span> 
        <span style="color:green" v-else>promosso</span>
      </h1>
      
      <div class="d-flex">
        <div class="mr-auto p-2">
          <h2>Tabella errori fatti</h2>
        </div>
        <div class="p-2">
          <button class="btn btn-dark">Home</button> <!--Da impostare l'evento decide te se vuoi farlo ritornare alla pagina home o far ripartire il quiz :)-->
        </div>
      </div>
      <Tabella :domandeSbagliate="this.risposteSbagliate" />
    </div>
  </div>
</template>

<script>
import Timer from "./Timer.vue";
import Tabella from './Tabella.vue'
export default {
  name: "Card",
  components:{
    Timer,
    Tabella
  },
  props: {
    domande: Array,
  },
  data() {
    return {
      numero: 0,
      risposteSbagliate:[],
      rispostaAllaDomanda:" ",
      On:true
    };
  },
  methods: {
    NextDomanda() {
      
      if(this.rispostaAllaDomanda==" ")
      {
        document.getElementById("errore").style.display="block";
        return -1
      }
    
      if(this.numero==this.domande.length-1)
      {
        document.getElementById("next").remove();
        document.getElementById("mostraRis").style.display = "block";
      }

      this.Correzione(this.rispostaAllaDomanda)
    
      if(this.numero<this.domande.length-1)
        this.numero += 1;
      
      document.getElementById("errore").style.display="none";
    },
    handleChange() {
      this.On = false;
      document.getElementById("next").remove();
      document.getElementById("TrueFalse").remove();
      document.getElementById("mostraRis").style.display = "block";
      document.getElementById("errore").style.display="none";
    },
    ShowRisTab()
    {
      if(this.On==false)
      {
        for(let i=this.numero;i<this.domande.length;i++)
        {
          this.risposteSbagliate.push(this.domande[i])
          this.risposteSbagliate[this.risposteSbagliate.length-1].risposta+=" "
        }
           
      }
      document.getElementById("risultatoTabella").style.display="block";
      document.getElementById("ShowDomande").style.display="none";
    },
    Correzione(scelta)
    {
        if(scelta==" ")
        {
          this.risposteSbagliate.push(this.domande[this.numero])
          this.risposteSbagliate[this.risposteSbagliate.length-1].risposta+=" "
        }
        else if(scelta!=this.domande[this.numero].risposta)
          this.risposteSbagliate.push(this.domande[this.numero])

        this.rispostaAllaDomanda=" ";
    },
  },
};
</script>
