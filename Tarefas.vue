<template>
  <Formulario @aoSalvarTarefa="salvarTarefa" />
  <div class="lista">
    <Box v-if="semTarefas">
      Você não está muito produtivo hoje
      <span class="has-text-weight-bold">:(</span>
    </Box>
    <div class="field">
      <p class="control has-icons-left">
        <input
          class="input"
          type="text"
          placeholder="Digite para filtrar"
          v-model="filtro"
        />
        <span class="icon is-small is-left">
          <i class="fas fa-search"></i>
        </span>
      </p>
    </div>
    <Tarefa
      v-for="(tarefa, index) in paginacaoTarefas"
      :tarefa="tarefa"
      :key="index"
      @aoTarefaClicada="selecionarTarefa"
    />


    <!-- Paginação -->


    <div class="paginacao" v-if="paginasTotal > 1">
      <button class="paginacao-first" @click="goTo(1)">
        <svg data-v-5696714e="" xmlns="http://www.w3.org/2000/svg" width="15.109" height="9.361" viewBox="0 0 15.109 9.361"><g data-v-5696714e="" transform="translate(0.5 8.789) rotate(-90)"><path data-v-5696714e="" fill="#495057" stroke="#fff" d="M8.064,6.5,1.785.225a.773.773,0,0,0-1.092,0L.231.688a.773.773,0,0,0,0,1.092L5.5,7.052.225,12.33a.774.774,0,0,0,0,1.092l.462.462a.773.773,0,0,0,1.092,0L8.064,7.6a.779.779,0,0,0,0-1.1Z" transform="translate(0 0)"></path></g></svg>
        <svg data-v-5696714e="" xmlns="http://www.w3.org/2000/svg" width="15.109" height="9.361" viewBox="0 0 15.109 9.361"><g data-v-5696714e="" transform="translate(0.5 8.789) rotate(-90)"><path data-v-5696714e="" fill="#495057" stroke="#fff" d="M8.064,6.5,1.785.225a.773.773,0,0,0-1.092,0L.231.688a.773.773,0,0,0,0,1.092L5.5,7.052.225,12.33a.774.774,0,0,0,0,1.092l.462.462a.773.773,0,0,0,1.092,0L8.064,7.6a.779.779,0,0,0,0-1.1Z" transform="translate(0 0)"></path></g></svg>
      </button>
      <button class="paginacao-prev" @click="prev()">
        <svg data-v-5696714e="" xmlns="http://www.w3.org/2000/svg" width="15.109" height="9.361" viewBox="0 0 15.109 9.361"><g data-v-5696714e="" transform="translate(0.5 8.789) rotate(-90)"><path data-v-5696714e="" fill="#495057" stroke="#fff" d="M8.064,6.5,1.785.225a.773.773,0,0,0-1.092,0L.231.688a.773.773,0,0,0,0,1.092L5.5,7.052.225,12.33a.774.774,0,0,0,0,1.092l.462.462a.773.773,0,0,0,1.092,0L8.064,7.6a.779.779,0,0,0,0-1.1Z" transform="translate(0 0)"></path></g></svg>
      </button>
     


      <ul class="paginacao-btns">
        <li class="paginacao-btn" v-for="(pagina, index) in paginas" :key="index"
        @click="goTo(pagina)" :class="{'ativo': pagina === page}">
          {{pagina}}
        </li>
      </ul>


      <button class="paginacao-next" @click="next()">
        <svg data-v-5696714e="" xmlns="http://www.w3.org/2000/svg" width="15.109" height="9.361" viewBox="0 0 15.109 9.361"><g data-v-5696714e="" transform="translate(0.5 8.789) rotate(-90)"><path data-v-5696714e="" fill="#495057" stroke="#fff" d="M8.064,6.5,1.785.225a.773.773,0,0,0-1.092,0L.231.688a.773.773,0,0,0,0,1.092L5.5,7.052.225,12.33a.774.774,0,0,0,0,1.092l.462.462a.773.773,0,0,0,1.092,0L8.064,7.6a.779.779,0,0,0,0-1.1Z" transform="translate(0 0)"></path></g></svg>
      </button>
      <button class="paginacao-last" @click="goTo(paginasTotal)">
        <svg data-v-5696714e="" xmlns="http://www.w3.org/2000/svg" width="15.109" height="9.361" viewBox="0 0 15.109 9.361"><g data-v-5696714e="" transform="translate(0.5 8.789) rotate(-90)"><path data-v-5696714e="" fill="#495057" stroke="#fff" d="M8.064,6.5,1.785.225a.773.773,0,0,0-1.092,0L.231.688a.773.773,0,0,0,0,1.092L5.5,7.052.225,12.33a.774.774,0,0,0,0,1.092l.462.462a.773.773,0,0,0,1.092,0L8.064,7.6a.779.779,0,0,0,0-1.1Z" transform="translate(0 0)"></path></g></svg>
        <svg data-v-5696714e="" xmlns="http://www.w3.org/2000/svg" width="15.109" height="9.361" viewBox="0 0 15.109 9.361"><g data-v-5696714e="" transform="translate(0.5 8.789) rotate(-90)"><path data-v-5696714e="" fill="#495057" stroke="#fff" d="M8.064,6.5,1.785.225a.773.773,0,0,0-1.092,0L.231.688a.773.773,0,0,0,0,1.092L5.5,7.052.225,12.33a.774.774,0,0,0,0,1.092l.462.462a.773.773,0,0,0,1.092,0L8.064,7.6a.779.779,0,0,0,0-1.1Z" transform="translate(0 0)"></path></g></svg>
      </button>
    </div>
   
    <!-- Fim Paginação -->


    <Modal :mostrar="tarefaSelecionada != null">
      <template v-slot:cabecalho>
        <p class="modal-card-title">Editando uma tarefa</p>
        <button @click="fecharModal" class="delete" aria-label="close"></button>
      </template>
      <template v-slot:corpo>
        <div class="field">
          <label for="descricaoDaTarefa" class="label"> Descrição </label>
          <input
            type="text"
            class="input"
            v-model="tarefaSelecionada.descricao"
            id="descricaoDaTarefa"
          />
        </div>
      </template>
      <template v-slot:rodape>
        <button @click="alterarTarefa" class="button is-success">
          Salvar alterações
        </button>
        <button @click="fecharModal" class="button">Cancelar</button>
      </template>
    </Modal>
  </div>
</template>


<script lang="ts">
import { computed, defineComponent, ref, watchEffect } from "vue";
import Formulario from "../components/Formulario.vue";
import Tarefa from "../components/Tarefa.vue";
import Box from "../components/Box.vue";
import Modal from "../components/Modal.vue";
import { useStore } from "@/store";
import {
  ALTERAR_TAREFA,
  CADASTRAR_TAREFA,
  OBTER_PROJETOS,
  OBTER_TAREFAS,
} from "@/store/tipo-acoes";
import ITarefa from "@/interfaces/ITarefa";


export default defineComponent({
  name: "App",
  components: {
    Formulario,
    Tarefa,
    Box,
    Modal
  },
  data() {
    return {
      tarefaSelecionada: null as ITarefa | null,
      page: 1,
      tarefasPorPagina: 4
    };
  },
  methods: {
    salvarTarefa(tarefa: ITarefa): void {
      this.store.dispatch(CADASTRAR_TAREFA, tarefa);
    },
    selecionarTarefa(tarefa: ITarefa) {
      this.tarefaSelecionada = tarefa;
    },
    fecharModal() {
      this.tarefaSelecionada = null;
    },
    alterarTarefa() {
      this.store
        .dispatch(ALTERAR_TAREFA, this.tarefaSelecionada)
        .then(() => this.fecharModal());
    },
    next() {
      this.page++;


      const lastPage = this.page > this.paginasTotal;
      if (lastPage) {
        this.page = this.paginasTotal;
      }
    },
    prev(){
      this.page--;


      const firstPage = this.page < 1;
      if (firstPage) {
        this.page++;
      }
    },
    goTo(pg: number) {
      if (pg < 1) {
        pg = 1;
      }


      this.page = +pg;


      if (pg > this.tarefasTotal) {
        this.page = this.tarefasTotal;
      }
    }
  },
  computed: {
    semTarefas(): boolean {
      return this.tarefas.length == 0;
    },
    tarefasTotal(): number{
      return this.tarefas.length;
    },
    paginas() {
      const range = 5;
      const offset = Math.floor(range / 2) + 1;
      const pagesArray = [];


      for (let i = 1; i <= this.paginasTotal; i++) {
        pagesArray.push(i);
      }
     
      pagesArray.splice(0, this.page - offset);
      pagesArray.splice(range, this.paginasTotal);


      return pagesArray;
    },
    paginasTotal(): number{
      const total = this.tarefasTotal / this.tarefasPorPagina;
      return total !== Infinity ? Math.ceil(total) : 0;
    },
    paginacaoTarefas(): ITarefa[]{
      let page = this.page - 1;
      // estou tirando 1, porque o array começa em 0.
      let start = page * this.tarefasPorPagina;
      let end = start + this.tarefasPorPagina;


      return this.tarefas.slice(start, end);
    }
  },
  setup() {
    const store = useStore();
    store.dispatch(OBTER_TAREFAS);
    store.dispatch(OBTER_PROJETOS);


    const filtro = ref("");


    // const tarefas = computed(() =>
    //   store.state.tarefa.tarefas.filter(
    //     (t) => !filtro.value || t.descricao.includes(filtro.value)
    //   )
    // );


    watchEffect(() => {
      store.dispatch(OBTER_TAREFAS, filtro.value);
    });


    return {
      tarefas: computed(() => store.state.tarefa.tarefas),
      store,
      filtro,
    };
  },
});
</script>
<style scoped>
@media(min-width: 769px){
  .paginacao{
    position: absolute;
    bottom: 20px;
    left: 45%;
}
}


.paginacao,
.paginacao-btns{
  display: flex;
  justify-content: center;
}
.paginacao button{
  border: none;
}
.paginacao-btn,
.paginacao-first,
.paginacao-prev,
.paginacao-next,
.paginacao-last{
  border-radius: 12px;
  color: #0D3860;
  background: #fff;
  font-size: 14px;
  margin-right: 8px;
  height: 40px;
  width: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
.paginacao-btn.ativo{
  background-color: #0D3860;
  color: #fff;
}
.paginacao-first svg,
.paginacao-prev svg{
  transform: rotate(-90deg);
}
.paginacao-first svg{
  margin: 0 -5px;
}
.paginacao-next svg,
.paginacao-last svg {
  transform: rotate(90deg);
}
.paginacao-last svg{
  margin: 0 -5px;
}
</style>
