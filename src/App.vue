<script setup>
import { reactive} from 'vue';
    const estado = reactive({
        num1: '',
        num2: '',
        operacoes: {
            soma: (a, b) => a + b,
            subtracao: (a, b) => a - b,
            multiplicacao: (a, b) => a * b,
            divisao: (a, b) => (b !== 0 ? a / b : 'Divisão por zero'),
    },
        resultado: 0,
    })

    const resultadoFinal = () => {
        const { num1, num2, operacaoMatematica } = estado;
        estado.resultado = estado.operacoes[operacaoMatematica](parseFloat(num1), parseFloat(num2));
};
</script>

<template>
    <section class="container col-6 d-flex align-items-center mt-5 flex-column">
        <div>
            <header>
                <div>
                    <h1>CALCULADORA</h1>
                </div>
            </header>
            <div class="mb-4">
                <p class="d-flex align-items-center flex-column">Digite o primeiro número:</p>
                <input class="col-12" type="number" v-model="estado.num1" @input="resultadoFinal" required placeholder="0">
            </div>
            <div class="mb-4">
                <p class="d-flex align-items-center flex-column">Digite o segundo número:</p>
                <input class="col-12" type="number" v-model="estado.num2" @input="resultadoFinal" required placeholder="0">
            </div>
            <div class="mb-4 d-flex align-items-center flex-column">
                <p>Selecione a operação matematica:</p>
                <select v-model="estado.operacaoMatematica" @change="calcula">
                    <option value="soma">Soma</option>
                    <option value="subtracao">Subtração</option>
                    <option value="divisao">Divisão</option>
                    <option value="multiplicacao">Multiplicação</option>
                </select>
            </div>
            <div class="d-flex align-items-center flex-column">
                <p class="fw-bold">Resultado:</p>
                <span>{{ estado.resultado }}</span>
            </div>
        </div>
    </section>
</template>

<style scoped>
input[type=number]::-webkit-inner-spin-button { 
    -webkit-appearance: none;
    
}
input[type=number] { 
   -moz-appearance: textfield;
   appearance: textfield;
}
</style>
