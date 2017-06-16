<template>
    <div>
        <button @click="executaAcao()" class="botao" :class="estiloDoBotao" :type="tipo">{{ rotulo }}</button>
    </div>
</template>

<script>
export default {
    props: {
        tipo: {
            required: true,
            type: String
        },
        rotulo: {
            required: true,
            type: String
        }, 
        confirmacao: {
            required: false,
            type: Boolean,
            default: false
        },
        estilo: {
            required: false,
            type: String,
            default: 'padrao'
        }
    },

    methods: {
        executaAcao() {
            if(this.confirmacao) {
                if (confirm('Confirma operação?'))
                    return this.$emit('botaoAtivado');
            }
            this.$emit('botaoAtivado');
        }
    },

    computed: {
        estiloDoBotao() {
            if(this.estilo == 'padrao') return 'botao-padrao';
            
            if (this.estilo == 'perigo') return 'botao-perigo';
        }
    }
}
</script>

<style scoped lang="sass">
    @import "./Botao.scss";
</style>
