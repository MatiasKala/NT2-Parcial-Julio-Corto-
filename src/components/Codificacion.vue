<template>

  <section>
    <input v-model="valor">
    <p>Cantidad caracteres = {{getCantidadCaracteresValor}}</p>
    <div v-if="this.valor">
      <b>{{valor | codificado}}(codificado)</b>
      <br>
      <br>
      <b>{{valor | aMayus}}(Mayuscula)</b>
      <br>
      <br>
      <b>{{valor | aMinus}}(Minuscula)</b>
      <br>
      <br>
      <b>{{valor | mayusIntercaladas}}(Mayuscula/Minuscula)</b>
      <br>
      <br>
      <b>{{valor | minusIntercaladas}}(Minuscula/Mayuscula)</b>
    </div>
    <hr>
    <p>Respuestas: 1:b 2:b 3:c 4:a,b 5:b</p>
  </section>

</template>

<script>

  export default  {
    name: 'codificacion',
    props: [],
    mounted () {

    },
    data () {
      return {
        valor:''
      }
    },
    filters:{
      aMayus(valor){
        return valor.toUpperCase()
      },
      aMinus(valor){
        return valor.toLowerCase()
      },
      mayusIntercaladas(valor){
        let mayus = true
        let str = ''
        Array.from(valor).forEach(element => {
          if(mayus){
            str += (element.toUpperCase())
            mayus = false
          } else {
            str += (element.toLowerCase())
            mayus = true
          }
        });
        return str
      },
      minusIntercaladas(valor){
        let minus = true
        let str = ''
        Array.from(valor).forEach(element => {
          if(minus){
            str += (element.toLowerCase())
            minus = false
          } else {
            str += (element.toUpperCase())
            minus = true
          }
        });
        return str
      },
      codificado(valor){
        valor = valor.toLowerCase()
        let arr = []
        Array.from(valor).forEach(element => {
          switch (element) {
            case 'a':
              arr.push('u')
              break;
            case 'e':
              arr.push('o')
              break;
            case 'o':
              arr.push('e')
              break;
            case 'u':
              arr.push('a')
              break;                                                    
            default:
              arr.push(element)
              break;
          }
        });
        return arr.join('')
      }
    },
    methods: {

    },
    computed: {
      getCantidadCaracteresValor(){return this.valor.length}
    }
}


</script>

<style scoped>
  .codificacion {

  }
</style>
