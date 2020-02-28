<template>
  <div class="row justify-center q-pt-md">
    <div>
      <img class="cartoes" id="cartao" src="statics/cartao.png"/>
      <img class="cartoes" id="cartao-verso" src="statics/cartao-verso.png"/>
      <canvas id="canva" width="400" height="300"></canvas>
      <q-input mask="#### #### #### ####" label="Numero" v-model="numero" @input="escrever()"/>
      <q-input label="Nome" v-model="nome" @input="escrever()"/>
      <q-input mask="####" label="CVV" v-model="cvv" @input="escreverCvv()"/>
      <q-input mask="##/####" label="Data de Validade" v-model="validade" @input="escrever()"/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      nome: '',
      numero: '',
      validade: '',
      cvv: '',
      canva: null,
      cartaoFrente: null,
      cartaoVerso: null
    }
  },
  mounted () {
    this.canva = document.getElementById('canva').getContext('2d')
    this.cartaoFrente = document.getElementById('cartao')
    this.cartaoVerso = document.getElementById('cartao-verso')
    this.canva.shadowBlur = 15
    this.canva.shadowColor = 'black'
    this.canva.drawImage(this.cartaoFrente, 10, 10)
  },
  methods: {
    escrever () {
      this.canva.clearRect(0, 0, 400, 400)
      this.canva.shadowBlur = 15
      this.canva.shadowColor = 'black'
      this.canva.drawImage(this.cartaoFrente, 10, 10)
      this.canva.fillStyle = 'white'
      this.canva.font = '15px Arial'
      this.canva.shadowBlur = 0
      this.canva.fillText(this.numero, 30, 150)
      this.canva.fillText('Data Validade', 190, 120)
      this.canva.fillText(this.validade, 215, 140)
      this.canva.fillText(this.nome, 30, 170)
    },
    escreverCvv () {
      this.canva.clearRect(0, 0, 400, 300)
      this.canva.shadowBlur = 15
      this.canva.shadowColor = 'black'
      this.canva.drawImage(this.cartaoVerso, 10, 10, this.cartaoFrente.width, this.cartaoFrente.height)
      this.canva.shadowBlur = 0
      this.canva.fillStyle = 'black'
      this.canva.font = '15px Arial'
      this.canva.fillText(this.cvv, 250, 100)
    }
  }
}
</script>

<style>
.cartoes {
  display: none;
}
#numero {
  border: solid;
  width: 300px;
  height: 300px;
}

</style>
