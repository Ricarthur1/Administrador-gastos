<script setup>
    import { computed } from 'vue'
    import { CircleProgressBar } from 'circle-progress.vue';
    import { formatearCantidad } from '../helpers'

    defineEmits(['reset-app'])

    const props = defineProps ({
        presupuesto: {
            type: Number,
            required: true
        },
        disponible: {
            type: Number,
            required: true
        },
        gastado: {
            type: Number,
            required: true
        }
    })

    const porcentaje = computed(() => {
        return parseInt(((props.presupuesto - props.disponible) / props.presupuesto) * 100)
    })
</script>

<template>
    <div class="dos-columnas">
        <div class="contenedor-grafico">
            <CircleProgressBar 
            :value="porcentaje"  
            :max="100" 
            :size="250"
            :strokeWidth="10"
            colorUnfilled="#3b82f6"
            colorBack="#e1e1e1"
            percentage  
           rounded>
          {{ gastado }} / {{ presupuesto }}
          </CircleProgressBar>   
        </div>

        <div class="contenedor-presupuesto">
            <button
            class="reset-app"
            type="button"
            @click="$emit('reset-app')"
            >Resetear App
            </button>
            <p>
                <span>Presupuesto:</span>
                 {{ formatearCantidad(presupuesto) }}
            </p>
            <p>
                <span>Disponible:</span>
                 {{ formatearCantidad(disponible) }}
            </p>
            <p>
                <span>Gastado:</span>
                {{ formatearCantidad(gastado) }}
            </p>

        </div>
    </div>


</template>



<style scoped>

    .dos-columnas {
        display: flex;
        flex-direction: column;
    }

    .dos-columnas > :first-child {
        margin-bottom: 2rem;
    }

    @media (min-width: 768px) {
        .dos-columnas {
            flex-direction: row;
            gap: 4rem;
            align-items: center;
        }

        .dos-columnas > :first-child {
            margin-bottom: 0;
        }
    }


    .reset-app {
        background-color: #DB2777;
        border: none;
        padding: 1rem;
        width: 100%;
        color: var(--blanco);
        font-weight: 900;
        text-transform: uppercase;
        border-radius: 1rem;
        transition-property: background-color;
        transition-duration: 300ms;
    }

    .reset-app:hover {
        cursor: pointer;
        background-color: #a8195c;

    }


    .contenedor-presupuesto {
        width: 100%;
    }

    .contenedor-presupuesto p {
        font-size: 2.4rem;
        text-align: center;
        color: var(--gris-oscuro);
        
    }

    @media (min-width: 768px) {
        .contenedor-presupuesto p {
            font-size: 2.4rem;
            text-align: left;
            
        }

    }
    .contenedor-presupuesto span {
        font-weight: 900;
        color: var(--azul)
    }
</style>