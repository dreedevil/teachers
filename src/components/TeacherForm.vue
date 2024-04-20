<template>
<section class="form">
    <h3>Añadir profesores</h3>
    <div><label>Nombre:</label><input type="text" v-model="teacher.teacherName"/></div>
    <div><label>Apellidos:</label><input type="text" v-model="teacher.surname"/></div>
    <div><label>DNI / NIF:</label><input type="text" v-model="teacher.dni"/></div>
    <div><label>Materias:</label><input type="text" v-model="subject"/> <button @click="handleSubject()">Agregar</button></div>
    <div>
        <ul>
            <li v-for="(sub,index) in teacher.subjects" :key="index">{{sub}}</li>
        </ul>
    </div>
    <div><input type="checkbox" v-model="teacher.doc"/> Dcumentacion entregada</div>
    <button @click="handleAddTeacher()">Agregar</button>
</section>
<section>Listado de  Profesores
    <table>
        <tr>
            <th>Nombre</th>
            <th>Apellidos</th>
            <th>DNI</th>
            <th>Materias</th>
            <th>Documentacion entregada</th>
        </tr>
        <tr v-for="teach in teachers" :key="teach.dni">
            <th>{{teach.teacherName}}</th>
            <th>{{teach.surname}}</th>
            <th>{{teach.dni}}</th>
            <th>
                <ul>
                    <li v-for="(item, index) in teach.subjects" :key="index">{{item}}</li> 
                </ul>
            </th>
            <th v-if="teach.doc"> Entregada</th>
            <th v-else> No Entregada</th>
        </tr>

    </table>

</section>
</template>

<script lang="ts" setup>
import {Ref, ref} from 'vue';

interface ITeacher {
    teacherName: string,
    surname: string,
    dni: string,
    subjects: Array<string>,
    doc:boolean
}

let teacher:Ref<ITeacher> = ref({
    teacherName: '',
    surname: '',
    dni: '',
    subjects: [],
    doc: false
})

let teachers:Ref<Array<ITeacher>> = ref([])
let subject:Ref<string> = ref('')
const handleSubject = () => {
    teacher.value.subjects.push(subject.value)
}

const handleAddTeacher = () => {
    teachers.value.push({
        teacherName: teacher.value.teacherName,
        surname: teacher.value.surname,
        dni:  teacher.value.dni,
        subjects:  teacher.value.subjects,
        doc: teacher.value.doc
    }) 
    teacher.value.teacherName = ""
    teacher.value.surname = ""
    teacher.value.dni =""
    teacher.value.subjects = []
    teacher.value.doc = false
}
</script>

<style scoped>
.form input{
    margin-top: 10px;
    margin-left:5px;
    margin-bottom: 4px;

}
.form ul {
    list-style: none;
    
}

.form table{
    align-content: center;
    margin-left: auto;
    margin-right: auto;

}
</style>
