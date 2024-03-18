<template>
    <h3 className="subtitle">Адресс:</h3>
    <Input label="Индекс"/>
    <div class="address">
        <Input label="Область"/>
        <Input label="Страна" :region="true"/>
    </div>
    <Input 
        label="Город*" :re="true"/>
    <div class="address">
        <Input label="Улица"/>
        <Input label="Дом" :home="true"/>
    </div>
</template>

<script setup>
import Input from './Input/input.vue';
const v = defineModel('v')
</script>

<style>
</style>