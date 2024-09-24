<template>
  <div>
    <div class="row flex-center q-mt-md">
      <q-input
        v-model="nomeLista"
        filled
        label="Nome da lista"
        class="col-11"
      ></q-input>
    </div>

    <div class="row flex-center q-mt-md">
      <q-input
        v-model="nomeNovo"
        filled
        label="Adicionar um produto"
        class="col-9"
      ></q-input>
      <q-btn
        flat
        class="col-2 q-py-md"
        @click="addProduto"
      >
        <i class="fa-solid fa-circle-plus fa-2x text-positive"></i>
      </q-btn>
    </div>
    <AlertasApp
      v-if="alerta"
      :texto="msgAlerta"
      :status="statusAlerta"
    />

    <!-- PRODUTO LISTADO -->
    <div id="lista">
      <div
        v-for="(item, index) in listaProdutos"
        :key="item.nome"
        class="item-produto row flex-center q-mt-md"
      >
        <div class="col-11 flex items-center justify-between">
          <!-- NOME PRODUTO -->
          <div
            class="nome"
            style="width: 80px"
          >
            {{ item.nome }}
          </div>
          <!-- /NOME PRODUTO -->

          <!-- QUANT PRODUTO -->
          <div class="quant col-2">
            <q-btn
              icon="add"
              size="sm"
              dense
              @click="incrItem(index)"
              style="margin-top: -3px"
            ></q-btn>
            <input
              v-model="listaProdutos[index].quantidade"
              class="text-center q-pt-sm"
              min="0"
              max="99"
              type="number"
              style="max-width: 30px; border: none; outline: none"
            />
            <q-btn
              icon="remove"
              size="sm"
              dense
              @click="decrItem(index)"
              style="margin-top: -3px"
            ></q-btn>
          </div>
          <!-- /QUANT PRODUTO -->

          <!-- VALOR PRODUTO -->
          <div class="valor flex items-center">
            R$ &nbsp;
            <q-input
              v-model="listaProdutos[index].valor"
              filled
              mask="#.##"
              fill-mask="0"
              reverse-fill-mask
              input-class="text-right"
              bg-color="grey-1"
              dense
              inputmode="numeric"
              style="max-width: 80px"
            />
          </div>
          <!-- /VALOR PRODUTO -->

          <!-- EXCLUIR PRODUTO -->
          <div class="exl">
            <q-btn
              flat
              class="col-2 q-py-md"
              @click="delProduto(index)"
            >
              <i class="fa-solid fa-trash fa-2x text-red"></i>
            </q-btn>
          </div>
          <!-- /EXCLUIR PRODUTO -->
        </div>
      </div>
      <!-- /PRODUTO LISTADO -->
    </div>
    <!-- /LISTA -->

    <!-- RODAPE -->
    <div
      id="rodape"
      class="bg-primary"
    >
      <div class="q-ma-md text-h5 flex justify-between items-center">
        <div class="text-white">
          <p>
            <strong>Produtos: {{ totalProdutos }}</strong>
          </p>
          <p>
            <strong>Valor total: {{ totalValor }}</strong>
          </p>
        </div>
        <div>
          <div>
            <q-btn
              color="white"
              text-color="primary"
              icon="save"
              label="Salvar"
              size="lg"
              @click="calcTotalValor"
            />
          </div>
        </div>
      </div>
    </div>
    <!-- /RODAPE -->
  </div>
</template>

<script setup>
  import AlertasApp from 'src/components/comuns/AlertasApp.vue';

  defineOptions({
    name: 'NovaLista',
    data() {
      return {
        nomeLista: '',
        listaProdutos: [],
        nomeNovo: '',
        quantNovo: 1,
        valorNovo: '0.00',
        alerta: false,
        msgAlerta: '',
        statusAlerta: '',
        totalProdutos: 0,
        totalValor: 0,
      };
    },
    watch: {
      listaProdutos: {
        handler(newVal, oldVal) {
          this.calcTotalProduto();
          this.calcTotalValor();
        },
        deep: true, // Monitora mudanças profundas nos objetos do array
      },
    },
    methods: {
      addProduto() {
        //
        if (!this.nomeNovo) {
          this.alerta = true;
          this.msgAlerta = 'É necessário preencher o nome do produto';
          this.statusAlerta = 'erro';
        } else {
          let produtoNovo = {
            nome: this.nomeNovo,
            quantidade: this.quantNovo,
            valor: this.valorNovo,
          };
          this.listaProdutos.push(produtoNovo);
          console.log(this.listaProdutos);

          this.nomeNovo = '';
          this.alerta = false;
        }
      },
      delProduto(indexProduto) {
        this.listaProdutos.splice(indexProduto, 1);
        console.log(this.listaProdutos);
      },
      incrItem(i) {
        if (this.listaProdutos[i].quantidade <= 98) {
          this.listaProdutos[i].quantidade++;
        }
      },
      decrItem(i) {
        if (this.listaProdutos[i].quantidade >= 2) {
          this.listaProdutos[i].quantidade--;
        }
      },
      calcTotalProduto() {
        let quantidadeTotal = this.listaProdutos.reduce((total, produto) => {
          return total + produto.quantidade;
        }, 0);
        this.totalProdutos = quantidadeTotal;
      },
      calcTotalValor() {
        let valorTotal = this.listaProdutos.reduce((total, produto) => {
          return total + parseFloat(produto.valor);
        }, 0);
        this.totalValor = Number(valorTotal.toFixed(2));
      },
    },
  });
</script>

<style scoped>
  .item-produto {
    border-top: 1px solid rgba(128, 128, 128, 0.463);
    border-bottom: 1px solid rgba(128, 128, 128, 0.463);
    padding: 20px 5px;
  }

  #lista {
    max-height: calc(100vh - 350px);
    overflow: auto;
  }

  #rodape {
    width: 100%;
    position: fixed;
    bottom: 0;
    box-shadow: 2px 2px 5px 2px black;
    text-shadow: 2px 2px 2px 5px black;
  }
</style>
