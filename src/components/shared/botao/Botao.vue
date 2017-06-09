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
            console.log(this.estilo);
            if(this.estilo == 'padrao') return 'botao-padrao';
            
            if (this.estilo == 'perigo') return 'botao-perigo';
        }
    }
}
</script>

<style scoped>
.botao {
    display: inline-block;
    padding: 10px;
    border-radius: 3px;
    margin: 10px;
    font-size: 1.2em;
}

.botao-perigo {
    background: firebrick;
    color: white;
}

.botao-padrao {
    background: darkcyan;
    color: white;
}
</style>
