<!-- 
  v-on -> Diretiva para setar valor a uma variavel. Igual a @
  v-bind -> Diretiva que recebe o valor de uma variavel. Igual a :

-->

<template>
    <div>
        <h1 class="centralizado">{{ titulo }}</h1>
        
        <p class="centralizado" v-show="mensagem">{{ mensagem }}</p>

        <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="Filtro pelo título da foto" /> {{ filtro }}
        <ul class="lista-fotos">
            <li class="lista-fotos-item" v-for="foto of fotosComFiltro" :key="foto._id">
                <meu-painel :titulo="foto.titulo">
                    <imagem-responsiva v-meu-transform:scale.animate.reverse="1.2" :url="foto.url" :titulo="foto.titulo" />
                    <router-link :to="{ name: 'altera', params:{ id: foto._id }}" >
                        <meu-botao tipo="button" rotulo="Alterar" />
                    </router-link>
                    <meu-botao 
                        tipo="button" 
                        rotulo="Remover" 
                        @botaoAtivado="remover(foto)" 
                        :confirmacao="true" 
                        estilo="perigo" />
                </meu-painel>
            </li>
        </ul>
    </div>
</template>

<script>

import Painel from '../shared/painel/Painel.vue';
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue';
import Botao from '../shared/botao/Botao.vue';
import transform from '../../directives/Transform';
import FotoService from '../../domain/foto/FotoService';

export default {
    components: {
        'meu-painel': Painel,
        'imagem-responsiva': ImagemResponsiva,
        'meu-botao': Botao
    },

    directives: {
        'meu-transform': transform
    },

    data() {
        return {
            titulo: 'Alurapic',
            fotos: [],
            filtro: '',
            mensagem: ''
        }
    },

    computed: {
        fotosComFiltro() {
            if (this.filtro) {
                let exp = new RegExp(this.filtro.trim(), 'i');
                return this.fotos.filter(foto => exp.test(foto.titulo));
            } else {
                return this.fotos;
            }

        }
    },

    created() {

        this.service = new FotoService(this.$resource);
        this.service
            .lista()
            .then(fotos => this.fotos = fotos, err => this.mensagem = err.message);
    },

    methods: {
        remover(foto) {
            this.service = new FotoService(this.$resource);

            this.service
                .apaga(foto._id)
                .then(() => {
                        const indice = this.fotos.indexOf(foto);
                        this.fotos.splice(indice, 1);
                        this.mensagem = "Foto removida com sucesso!"
                    }, err => this.mensagem = "Erro ao remover a foto");
        }
    }
}
</script>

<style>

.centralizado {
    text-align: center;
}

.lista-fotos {
    list-style: none;
}

.lista-fotos .lista-fotos-item {
    display: inline-block;
}

.filtro {
    display: block;
    width: 100%;
}
</style>
