<script setup>
import {reactive, computed} from 'vue';
import Alerta from './Alerta.vue'

const alerta = reactive({
	tipo:"",
	mensaje:""
})

const paciente = reactive({
	nombre: '',
	propietario: '',
	email: '',
	alta: '',
	sintomas: '',

})

const emit = defineEmits(['update:nombre','update:propietario','update:email','update:alta','update:sintomas', 'guardar-paciente'])

const props = defineProps({
	id:{
 type: [String, null],
 required: true
	},
	nombre:{
		type:String,
		required: true
	},
	propietario:{
		type:String,
		required: true
	},
	email:{
		type:String,
		required: true
	},
	alta:{
		type:String,
		required: true
	},
	sintomas:{
		type:String,
		required: true
	}
})

const validar = ()=>{
if(Object.values(props).includes('')){
alerta.mensaje = "todos los campos son obligatorios"
alerta.tipo = "error"
return
}
emit('guardar-paciente')
alerta.mensaje = 'Paciente agregado con exito';
alerta.tipo = 'exito'
setTimeout(() => {
	Object.assign(alerta, {
		mensaje : '',
tipo : ''
	})
}, 3000);

}

const editando = computed( () =>{
	return props.id
}) 

</script>


<template>
	<div class="md:w-1/2">
		<h2 class="font-black text-3xl text-center">Seguimiento pacientes</h2>
		<p class="text-lg mt-5 text-center mb-10">Añade pacientes <span
				class="text-indigo-600 font-bold">Adminístralos</span>
		</p>
		<Alerta v-if="alerta.mensaje" 
		:alerta="alerta"/>
		<form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10" @submit.prevent="validar">

			<div class="mb-5">
				<label for="mascotas" class="text-gray-700 uppercase font-bold">Nombre de mascota</label>
				<input type="text" id="mascotas" placeholder="Nombre de la mascotas"
					class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
					:value="nombre"
				@input="$emit('update:nombre',$event.target.value)"
					 />
			</div>
			<div class="mb-5">
				<label for="propietario" class="text-gray-700 uppercase font-bold">Nombre de Propietario</label>
				<input type="text" id="propietario" placeholder="Nombre del propietario"
					class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
					:value="propietario"
					@input="$emit('update:propietario',$event.target.value)"
 />
			</div>
			<div class="mb-5">
				<label for="email" class="text-gray-700 uppercase font-bold">Email</label>
				<input type="email" id="email" placeholder="Email"
					class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
					:value="email"
					@input="$emit('update:email',$event.target.value)"
				/>
			</div>
			<div class="mb-5">
				<label for="alta" class="text-gray-700 uppercase font-bold">Alta</label>
				<input type="date" id="alta" class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
				:value="alta"
				@input="$emit('update:alta',$event.target.value)"
				/>
			</div>
			<div class="mb-5">
				<label for="sintomas" class="text-gray-700 uppercase font-bold">Sintomas</label>
				<textarea id="sintomas" placeholder="Describe los sintomas"
					class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-48"
					:value="sintomas"
					@input="$emit('update:sintomas',$event.target.value)"  />
			</div>
			<input type="submit"
				class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
				:value="[editando? 'Guardar Cambios' : 'Registrar Pacientes']" />
		</form>
	</div>
</template>



<style ></style>