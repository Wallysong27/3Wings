<template>
  <div>
    <Message :msg="msg" v-show="msg" />
    <div>
      <form id="consulta-form" method="POST" @submit="createconsulta">
        <div class="input-container">
          <label for="nome">Nome do paciente:</label>
          <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">
        </div>
        <div class="input-container">
          <label for="especialidade">Escolha a especialidade:</label>
          <select name="especialidade" id="especialidade" v-model="especialidade">
            <option value="">Selecione a especialidade</option>
            <option v-for="especialidade in especialidades" :key="especialidade.id" :value="especialidade.tipo">{{ especialidade.tipo }}</option>
          </select>
        </div>
        <div class="input-container">
          <label for="dataconsulta">Escolha a data:</label>
          <select name="dataconsulta" id="dataconsulta" v-model="dataconsulta">
            <option value="">Selecione a data</option>
            <option v-for="dataconsulta in dtconsulta" :key="dataconsulta.id" :value="dataconsulta.tipo">{{ dataconsulta.tipo }}</option>
          </select>
        </div>
        <div class="input-container">
          <label for="horaconsulta">Escolha a o horário:</label>
          <select name="dataconsulta" id="dataconsulta" v-model="horaconsulta">
            <option value="">Selecione o horário</option>
            <option v-for="hora in horaconsultadata" :key="hora.id" :value="hora.tipo">{{ hora.tipo }}</option>
          </select>
        </div>
        <div class="input-container">
          <input class="submit-btn" type="submit" value="Marcar Consulta">
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Message from './Message'

export default {
  name: "ConsultaForm",
  data() {
    return {
      especialidades: null,
      dtconsulta: null,
      horaconsultadata: null,
      nome: null,
      especialidade: null,
      dataconsulta: null,
      horaconsulta: null,
      status: "Solicitado",
      msg: null
    }
  },
  methods: {
    async getconsultas() {
      const req = await fetch('http://localhost:3000/consultas')
      const data = await req.json()

      this.especialidades = data.especialidades
      this.dtconsulta = data.dtconsulta
      this.horaconsultadata = data.horaconsulta
    },
    async createconsulta(e) {

      e.preventDefault()

      const data = {
        nome: this.nome,
        dataconsulta: this.dataconsulta,
        especialidade: this.especialidade,
        horaconsulta: this.horaconsulta,
        status: "Marcado"
      }

      const dataJson = JSON.stringify(data)

      const req = await fetch("http://localhost:3000/marcadas", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson
      });

      const res = await req.json()

      console.log(res)

      //colocar uma mensagem no sistema
      this.msg = "Consulta marcada!"

      // clear message
      setTimeout(() => this.msg = "", 3000)

      // limpar campos
      this.nome = ""
      this.dataconsulta = ""
      this.especialidade = ""
      this.horaconsulta = []

    }
  },
  mounted() {
    this.getconsultas()
  },
  components: {
    Message
  }
}
</script>

<style scoped>
#consulta-form {
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  ;
  padding: 5px 10px;
  border-left: 4px solid #10959c;
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}


.submit-btn {
  background-color: #222;
  color: #10959c;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: .5s;
}

.submit-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>