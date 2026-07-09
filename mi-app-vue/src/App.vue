<!-- Archivo: src/App.vue -->
<!-- Componente raiz: lista de cursos con Vue 3 Composition API -->


<script setup>
// En Vue 3 con <script setup>, no necesitas exportar nada.
// Todo lo que declares aqui es accesible directamente en el <template>.
// ref() crea una variable reactiva.
// Cuando cambia su valor, Vue actualiza automaticamente el HTML.
// Equivalente a useState() en React.
import { ref } from 'vue'
// Lista de cursos (equivalente a const [cursos] = useState([...]) en React)
const cursos = ref([
{ id: 1, nombre: 'JavaScript Avanzado', activo: true },
{ id: 2, nombre: 'Base de Datos', activo: true },
{ id: 3, nombre: 'Arquitectura de Computadoras',activo: false },
{ id: 4, nombre: 'Vue.js y Next.js', activo: true },
])

// Variable reactiva para el contador de cursos activos
// .value es necesario para leer o modificar un ref() desde JavaScript.
// En el <template>, Vue lo hace automaticamente (no necesitas .value ahi).
const totalActivos = ref(
cursos.value.filter(c => c.activo).length
)
// Funcion para alternar el estado activo de un curso
// (equivalente a un handler de evento onClick en React)
function toggleActivo(id) {
const curso = cursos.value.find(c => c.id === id)
if (curso) {
curso.activo = !curso.activo // Vue detecta el cambio y re-renderiza
totalActivos.value = cursos.value.filter(c => c.activo).length
}
}
</script>



<template>
<div class="contenedor">
<h1>Cursos UTP 2026-I</h1>
<p class="subtitulo">Framework: Vue.js 3 con Composition API</p>
<!-- v-for: equivalente a cursos.map(curso => <li>...) en React -->
<!-- :key es obligatorio en v-for, igual que key= en React -->


<ul>
<li
v-for="curso in cursos"
:key="curso.id"
:class="curso.activo ? 'activo' : 'inactivo'"
>
<!-- v-if: renderizado condicional (equivalente a && en React) -->
<span class="badge" v-if="curso.activo">Activo</span>
<span class="badge inactivo-badge" v-else>Inactivo</span>
<strong>{{ curso.nombre }}</strong>
<!-- @click: evento de clic (equivalente a onClick en React) -->
<button @click="toggleActivo(curso.id)">Cambiar estado</button>
</li>
</ul>


<p class="resumen">
Cursos activos: <strong>{{ totalActivos }}</strong> de {{ cursos.length }}
</p>
</div>
</template>



<style scoped>
/* scoped: estos estilos solo aplican a este componente App.vue */
* { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: Arial, sans-serif; background: #f5f5f5; }
.contenedor {
max-width: 700px;
margin: 2rem auto;
background: white;
padding: 1.5rem;
border-radius: 8px;
box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
h1 { color: #7B0000; border-bottom: 3px solid #C0392B; padding-bottom: 0.4rem; }
.subtitulo { color: #888; font-size: 0.85rem; margin: 0.3rem 0 1.2rem; }
ul { list-style: none; padding: 0; }
li {
display: flex;
align-items: center;
gap: 0.6rem;
padding: 0.6rem 1rem;
margin-bottom: 0.5rem;
border-radius: 4px;
}
li.activo { background: #e8f5e9; border-left: 4px solid #2e7d32; }
li.inactivo { background: #fce4ec; border-left: 4px solid #c62828; }
.badge {font-size: 0.72rem; padding: 0.15rem 0.5rem;
border-radius: 10px; background: #2e7d32; color: white;
}
.inactivo-badge { background: #c62828; }
button {
margin-left: auto;
background: #C0392B; color: white;
border: none; padding: 0.3rem 0.8rem;
border-radius: 4px; cursor: pointer; font-size: 0.8rem;
}
button:hover { background: #7B0000; }
.resumen {
margin-top: 1rem; padding: 0.6rem 1rem;
background: #f5f5f5; border-radius: 4px;
}
</style>
