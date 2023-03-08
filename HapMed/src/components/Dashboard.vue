<template>
  <div id="consulta-table" v-if="marcadas">
    <Message :msg="msg" v-show="msg" />
    <div>
      <div id="consulta-table-heading">
        <div class="order-id">#:</div>
        <div>Paciente:</div>
        <div>Especialidade:</div>
        <div>Data:</div>
        <div>Hora:</div>
        <div>Status:</div>
      </div>
    </div>
    <div id="consulta-table-rows">
      <div class="consulta-table-row" v-for="consulta in marcadas" :key="consulta.id">
        <div class="order-number">{{ consulta.id }}</div>
        <div>{{ consulta.nome }}</div>
        <div>{{ consulta.especialidade }}</div>
        <div>{{ consulta.dataconsulta }}</div>
        <div>{{ consulta.horaconsulta }}</div>
        <div>{{ consulta.status }}</div>
        <!-- <div>
          <ul v-for="(opcional, index) in consulta.opcionais" :key="index">
            <li>{{ opcional }}</li>
          </ul>
        </div> -->
        <div>
          <!-- <select name="status" class="status" @change="updateconsulta($event, consulta.id)">
            <option :value="s.tipo" v-for="s in status" :key="s.id" :selected="consulta.status == s.tipo">
              {{ s.tipo }}
            </option>
          </select> -->
          <button class="delete-btn" @click="deleteconsulta(consulta.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
  <div v-else>
    <h2>Não há pedidos no momento!</h2>
  </div>
</template>
<script>
import Message from './Message'

export default {
  name: "Dashboard",
  data() {
    return {
      marcadas: null,
      consulta_id: null,
      status: [],
      msg: null
    }
  },
  components: {
    Message
  },
  methods: {
    async getPedidos() {
      const req = await fetch('http://localhost:3000/marcadas')

      const data = await req.json()

      this.marcadas = data

      // Resgata os status de pedidos
      this.getStatus()

    },
    async getStatus() {

      const req = await fetch('http://localhost:3000/status')

      const data = await req.json()

      this.status = data

    },
    async deleteconsulta(id) {

      const req = await fetch(`http://localhost:3000/marcadas/${id}`, {
        method: "DELETE"
      });

      const res = await req.json()

      //colocar uma mensagem no sistema
      this.msg = "A consulta foi desmarcada."

      // clear message
      setTimeout(() => this.msg = "", 8080);

      this.getPedidos()

    }
  },
  mounted() {
    this.getPedidos()
  }
}
</script>

<style scoped>
#consulta-table {
  max-width: 1200px;
  margin: 0 auto;
}

#consulta-table-heading,
#consulta-table-rows,
.consulta-table-row {
  display: flex;
  flex-wrap: wrap;
}

#consulta-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}

.consulta-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #CCC;
}

#consulta-table-heading div,
.consulta-table-row div {
  width: 15%;
}

#consulta-table-heading .order-id,
.consulta-table-row .order-number {
  width: 5%;
}

select {
  padding: 12px 6px;
  margin-right: 12px;
}

.delete-btn {
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

.delete-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>