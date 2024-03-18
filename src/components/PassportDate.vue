<script setup>
import {ref} from 'vue'
import Input from './Input/input.vue';
import RadioGroup from './CheckGroup/RadioGroup.vue';

const listDocs = ref([
    {name:'certificate', id:'passport', label:'Паспорт'},
    {name:'certificate', id:'Birth certificate', label:'Свидетельство о рождении'},
    {name:'certificate', id:'Driver`s license', label:'Вод. удостоверение'}
])

const selectDocs = ref([])
</script>

<template>
    <h3 className="subtitle">Паспорт:</h3>
    <div className="select-wrapper item docs">
        <h3>Тип документа: *</h3>
        <div class="item-container">
            <RadioGroup v-model:value="selectDocs" :options="listDocs" :re="true"/>
        </div>
    </div>
    <div class="passport">
        <Input label="Серия"/>
        <Input label="Номер"/>
    </div>
    <Input label="Кем выдан"/>
    <Input label="Дата выдачи*"/>
</template>

<style>
</style>