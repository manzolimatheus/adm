<template>
  <div class="kanban">
    <section id="description">
      <h1>Kanban</h1>
      <q
        >Em administração da produção, Kanban é um quadro de sinalização que
        controla os fluxos de produção ou transportes em uma indústria. O cartão
        pode ser trocado por outro sistema de sinalização, como luzes, caixas
        vazias e até locais vazios demarcados.</q
      >
    </section>
    <section id="form">
      <div class="row">
        <form>
          <h1><ion-icon name="document-text-outline"></ion-icon> Formulário Kanban</h1>
          <br />
          <div class="form-group">
            <label for="demanda">Demanda (D)</label><br />
            <input type="number" v-model="d" id="demanda" min="0" />
          </div>
          <div class="form-group" id="tempo">
            <label for="jornada"
              >Jornada Trabalho em horas (J)
              <ion-icon name="arrow-forward-outline"></ion-icon>
              {{ jornadaEmMinutos }} min</label
            ><br />
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
            <label for="tempoSetup">Tempo setup em min (TS)</label><br />
            <input type="number" v-model="ts" id="tempoSetup" min="0" />
          </div>
          <div class="form-group">
            <label for="tempoMovimentacao">Tempo Movimentação em min (TM)</label
            ><br />
            <input type="number" v-model="tm" id="tempoMovimentacao" min="0" />
          </div>
          <div class="form-group">
            <label for="tempoKanban">Tempo Produçao Kanban (TKB)</label><br />
            <input type="number" v-model="tkb" id="tempoKanban" min="0" />
          </div>
          <div class="form-group">
            <label for="pecasConstrutor">Número de peças construtor (NCT)</label
            ><br />
            <input type="number" v-model="nct" id="pecasConstrutor" min="0" />
          </div>
        </form>
        <div class="result">
          <h1><ion-icon name="sparkles-outline"></ion-icon> Resultado</h1>
          <p>D = {{ d }}</p>
          <p>TS = {{ ts }}</p>
          <p>TM = {{ tm }}</p>
          <p>J = {{ jornadaEmMinutos }}</p>
          <p>TKB = {{ tkb }}</p>
          <p>NCT = {{ nct }}</p>
          <p>TSM = {{ tsm }}</p>
          <p>TKB = {{ tpkb }}</p>
          <p>N = {{ n }}</p>
          <hr />
          <p>TSM = (TS + TM) / J</p>
          <p>TSM = ({{ ts }} + {{ tm }}) / {{ jornadaEmMinutos }}</p>
          <p>TSM = {{ tsm }}</p>
          <hr />
          <p>TKB = TKB / J</p>
          <p>TKB = {{ tkb }} / {{ jornadaEmMinutos }}</p>
          <p>TKB = {{ tpkb }}</p>
          <hr />
          <p>N = D * (TSM + TKB) / NCT</p>
          <p>N = {{ d }} * ({{ tsm }} + {{ tpkb }}) / {{ nct }}</p>
          <p>N = {{ n }}</p>
          <hr />
          <p>Total de cartões = {{ Math.ceil(n) }}</p>
          <p>{{ Math.floor(n) }} cartões com {{ nct }} peças</p>
          <p v-show="cartoesSobra">
            {{ cartoesSobra }} cartão com {{ nSobra }} peças
          </p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>

export default {
  name: "KanbanView",
  data() {
    return {
      d: 0,
      ts: 0,
      tm: 0,
      jh: null,
      jmin: null,
      tkb: 0,
      nct: 0,
    };
  },
  computed: {
    jornadaEmMinutos() {
      return this.jh * 60 + this.jmin;
    },
    tsm() {
      return ((this.ts + this.tm) / this.jornadaEmMinutos).toFixed(2);
    },
    tpkb() {
      return (this.tkb / this.jornadaEmMinutos).toFixed(2);
    },
    n() {
      return (
        (this.d * (parseFloat(this.tsm) + parseFloat(this.tpkb))) /
        this.nct
      ).toFixed(2);
    },
    cartoesSobra() {
      return parseFloat(this.n) - Math.floor(this.n) > 0 ? 1 : 0;
    },
    nSobra() {
      return (this.nct * (parseFloat(this.n) - Math.floor(this.n))).toFixed(2);
    },
  },
};
</script>

<style scoped>

#tempo{
    width: 50%;
  }

.result > h1{
  margin-bottom: 2%;
}

@media (max-width: 768px) {
  .result {
    margin-top: 8%;
  }

  #tempo {
    width: 100%;
  }

  input{
    width: 96% !important;
  }
}

</style>