<script setup lang="ts">
import { computed } from '@vue/reactivity';
import { ref } from 'vue';



const number1 = ref(0);
const number2 = ref(0);
const operation = ref('add');

const getResult = (): number => {
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
    
    <div class="row gap-3 bg-info-subtle m-0 p-3 rounded">
        <div class="col  p-0">
            <div class="input-group ">
                <input class="form-control" type="number" v-model="number1">
                
                <span class="input-group-text d-flex justify-content-center" style="width: 40px;"
                    :class="{
                        'bg-primary-subtle': operation === 'add',
                        'bg-success-subtle': operation === 'subtract',
                        'bg-warning-subtle': operation === 'multiply',
                        'bg-danger-subtle': operation === 'divide'
                        }"
                >
                    <i class="fa-solid " :class="{
                        'fa-plus text-primary': operation === 'add',
                        'fa-minus text-success': operation === 'subtract',
                        'fa-xmark text-warning': operation === 'multiply',
                        'fa-divide text-danger': operation === 'divide'                    
                        }"></i>
                </span>
                
                <input class="form-control" type="number" v-model="number2">
                <span class="input-group-text bg-info-subtle">
                    <i class="fa-solid fa-equals text-info"></i>
                </span>
                <input disabled class="form-control" id="n-1" type="number" :value="result">
            </div>
        </div>
        <div class="col-md-auto p-0">
            <select class="form-select" v-model="operation">
                <option value="add">Somar</option>
                <option value="subtract">Subtrair</option>
                <option value="multiply">Multiplicar</option>
                <option value="divide">Dividir</option>
            </select>
        </div>
    </div>
</template>