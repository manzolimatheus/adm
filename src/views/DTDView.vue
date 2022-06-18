<template>
  <div class="dtd">
    <section id="description">
      <h1>Dock To Dock Time</h1>
      <q
        >DTD é o tempo em horas e dias que uma matéria-prima permanece no
        estoque, um DTD <strong>MENOR</strong> significa que a empresa é mais
        <strong>COMPETITIVA</strong>, já que produz mais.</q
      >
    </section>
    <section id="form">
      <div class="row">
        <form @submit.prevent>
          <h1>
            <ion-icon name="document-text-outline"></ion-icon> Formulário DTD
          </h1>
          <br />
          <div class="form-group">
            <label for="materia">Matéria-Prima (M)</label><br />
            <input type="number" v-model="materiaPrima" id="materia" min="0" />
          </div>
          <div class="form-group">
            <label for="saida">Saídas diárias (SD)</label><br />
            <input type="number" v-model="saidasDiarias" id="saida" min="0" />
          </div>
          <div class="form-group">
            <label for="produto">Produto acabado (PA)</label><br />
            <input
              type="number"
              v-model="produtoAcabado"
              id="produto"
              min="0"
            />
          </div>
          <div class="form-group" id="tempo">
            <label for="jornada">Jornada Trabalho em horas (J)</label><br />
            <div class="row">
              <input
                type="number"
                v-model="jh"
                id="jornadaH"
                min="0"
                placeholder="Digite as horas (Ex: 7)"
              />
              <input
                type="number"
                v-model="jmin"
                id="jornadaMin"
                min="0"
                placeholder="Digite os minutos (Ex: 42)"
              />
            </div>
          </div>
          <div class="form-group">
            <label for="dtdCompetidor">DTD do competidor</label><br />
            <input
              type="number"
              v-model="dtdCompetidor"
              id="dtdCompetidor"
              min="0"
              step="0.01"
            />
          </div>
          <div class="form-group w-50" id="setores">
            <hr />
            <br />
            <h2><ion-icon name="business-outline"></ion-icon> Setores</h2>
            <br />
            <p v-if="setores.length < 1">Não há setores para exibir.</p>
            <div
              v-for="(valorSetor, index) in setores"
              :key="index"
              class="form-group"
            >
              <label :for="`setor${index}`">Setor {{ index + 1 }}</label
              ><br />
              <div class="addSetorGroup">
                <input
                  type="number"
                  v-model="setores[index]"
                  :id="`setor${index}`"
                  min="0"
                />
                <button class="button removeButton" @click="removeSetor(index)">
                  -
                </button>
              </div>
            </div>
            <hr />
            <div class="form-group">
              <label for="setorNovo">Novo setor</label><br />
              <div class="addSetorGroup">
                <input
                  type="number"
                  v-model="setorTemp"
                  id="setorNovo"
                  min="0"
                />
                <button class="button addButton" @click="addSetor">+</button>
              </div>
            </div>
          </div>
        </form>
        <div class="result">
          <h1><ion-icon name="sparkles-outline"></ion-icon> Resultado</h1>
          <br />
          <p>Total Produtos = {{ totalProdutos }}</p>
          <p>J = {{ jornadaTrabalho }}h</p>
          <p>SD = {{ sd }}</p>
          <p>DTD Horas = {{ dtdH }}</p>
          <p>DTD Dias = {{ dtdD }}</p>
          <hr />
          <p>Total Produtos = Matéria Prima + Produto Acabado + Setores</p>
          <p>
            Total Produtos = {{ materiaPrima }} + {{ produtoAcabado }} +
            {{ totalSetores }}
          </p>
          <p>Total Produtos = {{ totalProdutos }}</p>
          <hr />
          <p>SD = SD / J</p>
          <p>SD = {{ saidasDiarias }} / {{ jornadaTrabalho }}</p>
          <p>SD = {{ sd }}</p>
          <hr />
          <p>DTD Horas = Total Produtos / SD</p>
          <p>DTD Horas = {{ totalProdutos }} / {{ sd }}</p>
          <p>DTD Horas = {{ dtdH }}</p>
          <hr />
          <p>DTD Dias = DTD Horas / J</p>
          <p>DTD Dias = {{ dtdH }} / {{ jornadaTrabalho }}</p>
          <p>DTD Dias = {{ dtdD }}</p>
          <hr />
          <div v-show="dtdD > 0">
            <div v-if="dtdD > dtdCompetidor">
              <p>
                A outra empresa é mais competitiva, já que apresenta um DTD
                menor que nossa empresa.
              </p>
              <br />
              <img src="@/assets/sad.png" alt="Emoji triste" />
            </div>
            <div v-else>
              <p>
                Nossa empresa é mais competitiva, já que apresenta um DTD menor
                que o do competidor.
              </p>
              <br />
              <img src="@/assets/happy.webp" alt="Emoji feliz" />
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "DTDView",
  data() {
    return {
      materiaPrima: 0,
      saidasDiarias: 0,
      produtoAcabado: 0,
      jh: 0,
      jmin: 0,
      setorTemp: 0,
      setores: [],
      dtdCompetidor: 0,
    };
  },
  methods: {
    addSetor() {
      this.setores.push(this.setorTemp);
      this.setorTemp = 0;
    },
    removeSetor(index) {
      this.setores.splice(index, 1);
    },
  },
  computed: {
    totalSetores() {
      return this.setores.reduce((a, b) => a + b, 0);
    },
    totalProdutos() {
      return this.totalSetores + this.produtoAcabado + this.materiaPrima;
    },
    minEmHora() {
      return parseFloat((this.jmin / 60).toFixed(2));
    },
    jornadaTrabalho() {
      return this.jh + this.minEmHora;
    },
    sd() {
      return parseFloat((this.saidasDiarias / this.jornadaTrabalho).toFixed(2));
    },
    dtdH() {
      return parseFloat((this.totalProdutos / this.sd).toFixed(2));
    },
    dtdD() {
      return parseFloat((this.dtdH / this.jornadaTrabalho).toFixed(2));
    },
  },
};
</script>

<style scoped>
.button {
  color: white;
  border: none;
  border-radius: 5px;
  margin-left: 10px;
  padding: 2%;
  cursor: pointer;
  font-size: 16pt;
}

.addButton {
  background-color: #00bcd4;
}

.addButton:hover {
  background-color: #0097a7;
}

.removeButton {
  background-color: tomato;
}

.removeButton:hover {
  background-color: #e53935;
}

#tempo {
  width: 50%;
}

.result > h1 {
  margin-bottom: 2%;
}

@media (max-width: 768px) {
  .result {
    margin-top: 8%;
  }

  #tempo {
    width: 100%;
  }

  input {
    width: 96% !important;
  }

  #setores {
    width: 100%;
  }

  .addSetorGroup {
    display: flex;
    justify-content: space-between;
  }
}
</style>