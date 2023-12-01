<template>
    <div id="app" data-v-app="">
        <header class="container mx-auto text-center"><img src="./logoSitmotul.svg" alt="logotipo del sitmotul"
                class="w-20 mx-auto mt-7">
            <h1 class="font-bold text-xl">SITMOTUL</h1>
            <p class="font-medium text-s sr-only">Sistema Institucional de Tutoría del ITS Motul</p>
        </header>
        <main class="w-full md:w-2/3 lg:w-1/2 md:mx-auto">
            <div>
                <h2 class="font-medium text-center mb-5">Estado de la evaluación tutor del 2023b <br> al Martes 28 de
                    Noviembre de 2023</h2>
                <p class="mt-4 font-bold  text-center">Del:{{ formatoFechaInicio }}</p>
                <p class="mt-4 font-bold  text-center">Al:{{ formatoFechaFin }}</p>

                <div class="mx-auto mt-8 h-48 bg-gradient-to-r bg-amber-500 to-red-500 p-1 rounded-full shadow-lg">
                    <p class="mt-4 text-white text-center">Quedan:</p>
                    <div class="relative w-24 h-24 mx-auto bg-white rounded-full shadow-md">
                        <div class="flex items-center justify-center w-full h-full text-black text-2xl font-semibold">
                            <p class="text-center">{{ diasrestantes }} <br> <span class="text-red-800">DÍAS</span></p>
                        </div>
                    </div>
                    <p class="mt-4 text-white text-center">Para finalizar</p>
                </div>
                <br>
                <div class="flex flex-col gap-5 md:flex-row">
                    <!-- Primer Elemento - Gráfico de Barras -->
                    <div class="w-full md:w-3/4 mx-auto bg-sky-800 rounded-lg text-sky-200 px-10 py-8 shadow-md">
                        <div class="flex items-center justify-between mb-4">
                            <h3 class="text-5xl font-bold">{{ progreso }}%</h3>
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                                stroke="currentColor" class="w-12 h-12">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M11.35 3.836c-.065.21-.1.433-.1.664 0 .414.336.75.75.75h4.5a.75.75 0 00.75-.75 2.25 2.25 0 00-.1-.664m-5.8 0A2.251 2.251 0 0113.5 2.25H15c1.012 0 1.867.668 2.15 1.586m-5.8 0c-.376.023-.75.05-1.124.08C9.095 4.01 8.25 4.973 8.25 6.108V8.25m8.9-4.414c.376.023.75.05 1.124.08 1.131.094 1.976 1.057 1.976 2.192V16.5A2.25 2.25 0 0118 18.75h-2.25m-7.5-10.5H4.875c-.621 0-1.125.504-1.125 1.125v11.25c0 .621.504 1.125 1.125 1.125h9.75c.621 0 1.125-.504 1.125-1.125V18.75m-7.5-10.5h6.375c.621 0 1.125.504 1.125 1.125v9.375m-8.25-3l1.5 1.5 3-3.75">
                                </path>
                            </svg>
                        </div>
                        <!-- Barra de Progreso -->
                        <div class="bg-white h-20 rounded-full">
                            <div class="bg-sky-500 h-full rounded-full" style="width: 62%;"></div>
                        </div>
                        <p class="text-center mt-4">{{ info.alEvaluados }} de {{ info.alTotal }} realizadas</p>
                    </div>

                    <!-- Segundo Elemento - Gráfico de Barras -->
                    <div class="w-full md:w-3/4 mx-auto bg-red-800 rounded-lg text-sky-200 px-10 py-8 shadow-md">
                        <div class="flex items-center justify-between mb-4">
                            <h3 class="text-5xl font-bold">{{ calcularPorcentaje }}%</h3>
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                                stroke="currentColor" class="w-12 h-12">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M12 9v3.75m9-.75a9 9 0 11-18 0 9 9 0 0118 0zm-9 3.75h.008v.008H12v-.008z"></path>
                            </svg>
                        </div>
                        <!-- Barra de Progreso -->
                        <div class="bg-white h-20 rounded-full">
                            <div class="bg-red-500 h-full rounded-full" :style="{ 'width': calcularPorcentaje + '%' }">
                            </div>
                        </div>
                        <p class="text-center mt-4">{{ info.alTotal - info.alEvaluados }} faltan por realizar</p>
                    </div>
                </div>

            </div>
            <br>
            <div class="container mx-auto mt-8 p-4">

                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">

                    <!-- Sistemas Computacionales -->
                    <div
                        class="bg-gradient-to-br from-blue-700 via-blue-800 to-indigo-900 text-white rounded-lg shadow-md overflow-hidden transition-transform transform hover:scale-105">
                        <div class="p-6">
                            <h3 class="text-sm font-medium mb-2">Sistemas Computacionales</h3>
                            <div class="flex items-center justify-center mb-4">
                                <div class="w-full bg-gray-300 rounded-full">
                                    <div class="bg-green-500 text-white py-1 rounded-full"
                                        :style="{ 'width': barraprogreso + '%' }">{{ barraprogreso }}%</div>

                                </div>
                            </div>

                            <p class="text-white">{{ iscData.listas }} de {{ iscData.listas + iscData.faltantes }}
                                completadas</p>
                            <p class="text-white">{{ (iscData.listas + iscData.faltantes) - iscData.listas }} pendientes</p>

                        </div>
                    </div>

                    <!-- Electromecánica -->
                    <div
                        class="bg-gradient-to-br from-blue-600 via-blue-700 to-indigo-800 text-white rounded-lg shadow-md overflow-hidden transition-transform transform hover:scale-105">
                        <div class="p-6">
                            <h3 class="text-sm font-medium mb-2">Electromecánica</h3>
                            <div class="flex items-center justify-center mb-4">
                                <div class="w-full bg-gray-300 rounded-full">
                                    <div class="bg-green-500 text-white py-1 rounded-full"
                                        :style="{ 'width': barraprogresoiem + '%' }">{{ barraprogresoiem }}%</div>
                                </div>
                            </div>
                            <p class="text-white">{{ iemData.listas }} de {{ iemData.listas + iemData.faltantes }}
                                completadas</p>
                            <p class="text-white">{{ (iemData.listas + iemData.faltantes) - iemData.listas }} pendientes</p>
                        </div>
                    </div>

                    <!-- Electrónica -->
                    <div
                        class="bg-gradient-to-br from-blue-500 via-blue-600 to-indigo-700 text-white rounded-lg shadow-md overflow-hidden transition-transform transform hover:scale-105">
                        <div class="p-6">
                            <h3 class="text-sm font-medium mb-2">Electrónica</h3>
                            <div class="flex items-center justify-center mb-4">
                                <div class="w-full bg-gray-300 rounded-full">
                                    <div class="bg-green-500 text-white py-1 rounded-full"
                                        :style="{ 'width': barraprogresoie + '%' }">{{ barraprogresoie }}%</div>
                                </div>
                            </div>
                            <p class="text-white">{{ ieData.listas }} de {{ ieData.listas + ieData.faltantes }} completadas
                            </p>
                            <p class="text-white">{{ (ieData.listas + ieData.faltantes) - ieData.listas }} pendientes</p>
                        </div>
                    </div>

                    <!-- Energías Renovables -->
                    <div
                        class="bg-gradient-to-br from-blue-400 via-blue-500 to-indigo-600 text-white rounded-lg shadow-md overflow-hidden transition-transform transform hover:scale-105">
                        <div class="p-6">
                            <h3 class="text-sm font-medium mb-2">Energías Renovables</h3>
                            <div class="flex items-center justify-center mb-4">
                                <div class="w-full bg-gray-300 rounded-full">
                                    <div class="bg-green-500 text-white py-1 rounded-full"
                                        :style="{ 'width': barraprogresoier + '%' }">{{ barraprogresoier }}%</div>
                                </div>
                            </div>
                            <p class="text-white">{{ ierData.listas }} de {{ ierData.listas + ierData.faltantes }}
                                completadas</p>
                            <p class="text-white">{{ (ierData.listas + ierData.faltantes) - ierData.listas }} pendientes</p>
                        </div>
                    </div>

                    <!-- Industrial -->
                    <div
                        class="bg-gradient-to-br from-blue-300 via-blue-400 to-indigo-500 text-white rounded-lg shadow-md overflow-hidden transition-transform transform hover:scale-105">
                        <div class="p-6">
                            <h3 class="text-sm font-medium mb-2">Industrial</h3>
                            <div class="flex items-center justify-center mb-4">
                                <div class="w-full bg-gray-300 rounded-full">
                                    <div class="bg-green-500 text-white py-1 rounded-full"
                                        :style="{ 'width': barraprogresoii + '%' }">{{ barraprogresoii }}%</div>
                                </div>
                            </div>
                            <p class="text-white">{{ iiData.listas }} de {{ iiData.listas + iiData.faltantes }} completadas
                            </p>
                            <p class="text-white">{{ (iiData.listas + iiData.faltantes) - iiData.listas }} pendientes</p>
                        </div>
                    </div>

                    <div
                        class="bg-gradient-to-br from-blue-300 via-blue-400 to-indigo-500 text-white rounded-lg shadow-md overflow-hidden transition-transform transform hover:scale-105">
                        <div class="p-6">
                            <h3 class="text-sm font-medium mb-2">Total de retrícula evaluada</h3>
                            <div class="flex items-center justify-center mb-4">
                                <div class="w-full bg-gray-300 rounded-full">
                                    <div class="bg-green-500 text-white py-1 rounded-full"
                                        :style="{ 'width': barraprogresoretricula + '%' }">{{ barraprogresoretricula }}%
                                    </div>
                                </div>
                            </div>
                            <p class="text-white">{{ sumalista }} de {{ sumalista + divfalt }} completadas en total
                            </p>
                            <p class="text-white">{{ (sumalista + divfalt) - sumalista }} pendientes en total</p>
                        </div>
                    </div>
                </div>

            </div>
        </main>
    </div>
</template>
  
  
<script setup>

import { ref, onMounted } from 'vue';
import dayjs from 'dayjs';
import { computed } from 'vue';
import 'dayjs/locale/es'; // Importa el idioma español
import Chart from 'chart.js/auto';

dayjs.locale('es');
const info = ref('');
const info2 = ref('');
async function fetchData() {
    try {
        const response = await fetch('https://sitmotul.com.mx/api/statusEval');
        const data = await response.json();
        info.value = data;
        console.log(info.value);
    } catch (error) {
        console.error('Error al obtener datos:', error);
    }
}

onMounted(() => {
    fetchData();
});


// const finicio = dayjs(info.inicio).format('DD-MM-YYYY');
// const ffin = dayjs(info.fin).format('DD-MM-YYYY');

const formatoFechaInicio = computed(() => {
    return dayjs(info.value.inicio).format('DD-MM-YYYY');
});

const formatoFechaFin = computed(() => {
    return dayjs(info.value.fin).format('dddd, DD [de] MMMM [del] YYYY');
});


const diasrestantes = computed(() => {
    const fnow = dayjs();
    const ffin = dayjs(info.value.fin);

    const diferencia = ffin.diff(fnow, 'days');

    return diferencia
});

const iscData = ref({
    listas: 0,
    faltantes: 0
});
const iemData = ref({
    listas: 0,
    faltantes: 0
});

const ierData = ref({
    listas: 0,
    faltantes: 0
});

const ieData = ref({
    listas: 0,
    faltantes: 0
});

const iiData = ref({
    listas: 0,
    faltantes: 0
});

const fetchData2 = async () => {
    try {
        const response = await fetch('https://sitmotul.com.mx/api/statusEvalIng');
        const data = await response.json();

        // Verifica que la propiedad "ISC" exista en los datos
        if (data.ISC) {
            iscData.value.listas = data.ISC.listas;
            iscData.value.faltantes = data.ISC.faltantes;
            iemData.value.listas = data.IEM.listas;
            iemData.value.faltantes = data.IEM.faltantes;
            ierData.value.listas = data.IER.listas;
            ierData.value.faltantes = data.IER.faltantes;
            ieData.value.listas = data.IE.listas;
            ieData.value.faltantes = data.IE.faltantes;
            iiData.value.listas = data.II.listas;
            iiData.value.faltantes = data.II.faltantes;
            console.log(iscData.value.listas);
        } else {
            console.error('La propiedad no está presente en los datos recibidos:', data);
        }
    } catch (error) {
        console.error('Error al obtener datos:', error);
    }
};

onMounted(() => {
    fetchData2();
});


const calcularPorcentaje = computed(() => {
    if (info.value && info.value.alTotal && info.value.alEvaluados) {
        const porcentaje = ((info.value.alTotal - info.value.alEvaluados) / info.value.alTotal) * 100;
        return Math.round(porcentaje);
    } else {
        return 0;
    }
});

const progreso = computed(() => {
    if (info.value && info.value.alTotal && info.value.alEvaluados) {
        const numero = (info.value.alEvaluados / info.value.alTotal) * 100;
        return Math.round(numero);
    } else {
        return 0;
    }
});



const barraprogreso = computed(() => {
    if (iscData.value.listas && iscData.value.faltantes) {
        const porc = (iscData.value.listas / (iscData.value.listas + iscData.value.faltantes)) * 100;
        return Math.round(porc);
    } else {
        return 0;
    }
});


const barraprogresoiem = computed(() => {
    if (iemData.value.listas && iemData.value.faltantes) {
        const porce = (iemData.value.listas / (iemData.value.listas + iemData.value.faltantes)) * 100;
        return Math.round(porce);
    } else {
        return 0;
    }
});

const barraprogresoier = computed(() => {
    if (ierData.value.listas && ierData.value.faltantes) {
        const porce = (ierData.value.listas / (ierData.value.listas + ierData.value.faltantes)) * 100;
        return Math.round(porce);
    } else {
        return 0;
    }
});

const barraprogresoie = computed(() => {
    if (ieData.value.listas && ieData.value.faltantes) {
        const porce = (ieData.value.listas / (ieData.value.listas + ieData.value.faltantes)) * 100;
        return Math.round(porce);
    } else {
        return 0;
    }
});

const barraprogresoii = computed(() => {
    if (iiData.value.listas && iiData.value.faltantes) {
        const porce = (iiData.value.listas / (iiData.value.listas + iiData.value.faltantes)) * 100;
        return Math.round(porce);
    } else {
        return 0;
    }
});

const sumalista = ref();
const divfalt = ref();

const barraprogresoretricula = computed(() => {
    if (
        iscData.value.listas &&
        iscData.value.faltantes &&
        iiData.value.listas &&
        iiData.value.faltantes &&
        iemData.value.listas &&
        iemData.value.faltantes &&
        ierData.value.listas &&
        ierData.value.faltantes &&
        ieData.value.listas &&
        ieData.value.faltantes
    ) {
         sumalista.value =
            iscData.value.listas +
            iiData.value.listas +
            iemData.value.listas +
            ierData.value.listas +
            ieData.value.listas;

         divfalt.value =
            iscData.value.faltantes +
            iiData.value.faltantes +
            iemData.value.faltantes +
            ierData.value.faltantes +
            ieData.value.faltantes;

            const lista =
            iscData.value.listas +
            iiData.value.listas +
            iemData.value.listas +
            ierData.value.listas +
            ieData.value.listas;

            const falt =
            iscData.value.faltantes +
            iiData.value.faltantes +
            iemData.value.faltantes +
            ierData.value.faltantes +
            ieData.value.faltantes;

        const porcentaje = (lista / (lista + falt)) * 100;

        console.log(sumalista);

        return Math.round(porcentaje);
    } else {
        return 0;
    }
});



// console.log(barraprogreso);

</script>
  
<style>/* Agrega estilos según sea necesario */</style>
  