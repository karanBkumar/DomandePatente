<template>
    <table class="table table-striped table-dark table-bordered border-white">
      <thead>
        <tr>
          <th scope="col"  class="border-white">#</th>
          <th scope="col">Immagine</th>
          <th scope="col">Domanda</th>
          <th scope="col">Tua Risposta</th>
          <th scope="col">Risposta Corretta</th>
          <th scope="col">Cap da ripassare</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in domandeSbagliate" :key="item.id">
          <th scope="row">{{domandeSbagliate.indexOf(item)+1}}</th>
          <td v-if="item.immagine!='NA'">
            <img class="rounded" src="../assets/logo.png" >
          </td>
          <td v-else>
            
          </td>
          <td v-html="item.domanda"></td>
          <td v-if="item.risposta=='V'">F</td>
          <td v-else-if="item.risposta=='F'">V</td>
          <td v-else>NA</td>
          <td>{{item.risposta}}</td>
          <td>{{item.nomecapitolo}}</td>
        </tr>
      </tbody>
    </table>
</template>

<script>
export default {
    name:"Table",
    props:{
        domandeSbagliate:Array
    }
}
</script>