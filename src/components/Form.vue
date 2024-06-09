<script setup lang="ts">
    import { computed } from '@vue/reactivity';
    import { ref } from 'vue';


    const number1 = ref(0);
    const number2 = ref(0);
    const operation = ref('add');

    const getResult = ():number => {
        let result = 0;
        switch (operation.value) {
            case 'add': result = number1.value + number2.value; break;
            case 'subtract': result = number1.value - number2.value; break;
            case 'multiply': result = number1.value * number2.value; break;
            case 'divide': {
                if (number1.value === 0 || number2.value === 0) {
                    break;
                }

                result = number1.value / number2.value; 
                break;
            }
            default: break;
        }
         
        return result;
    }

    const result = computed(() => getResult());

</script>


<template>
    <div class="row">
        <div class="input-group mb-3 col">
            <!-- <label class="form-label"  for="n-1">Número 1</label> -->
            <input class="form-control" type="number" v-model="number1">
            <span class="">
                <select class="form-select" v-model="operation">
                    <option value="add">Somar</option>
                    <option value="subtract">Subtrair</option>
                    <option value="multiply">Multiplicar</option>
                    <option value="divide">Dividir</option>
                </select>
            </span>
            <input class="form-control" type="number" v-model="number2">
            <span class="input-group-text">=</span>
            <input disabled class="form-control" id="n-1" type="number" :value="result">
        </div>
    </div>
</template>