<script setup>
import { ref, computed } from 'vue'

import group from './Group/Group.vue'
import Input from './Input/input.vue'
import RadioGroup from './CheckGroup/RadioGroup.vue'
import InputPhone from './Input/InputPhone.vue';

const props = defineProps({
  options: {
    type: Array,
    required: true
  },
  showGroupError: {
    type: Boolean,
    required: true
  }
});

const options = defineModel('options')

const listGender = defineModel('listGender')
const selectGender = ref([])

const listDoc = defineModel('listDoc')
const selectDoc = ref([])

const v = defineModel('v')
</script>

<template>
    <Input 
        label="Фамилия*"
        type="text"
        :re="true"/>
    <Input 
        label="Имя*"
        :re="true"/>
    <Input 
        label="Отчество"
        />
    <div className="date item">
        <h3>Дата рождения*</h3>
        <input type="date" required>
    </div>
    <InputPhone 
        label="Номер телефона*" 
        type="tel"
        />
    <div className="select-wrapper item">
        <h3>Выберите пол:</h3>
        <div class="item-container">
            <RadioGroup v-model:value="selectGender" :options="listGender"/>
        </div>
    </div>
    <group :options="options":showGroupError="showGroupError"/>
    <div className="select-wrapper item">
        <h3>Лечащий врач:</h3>
        <div class="item-container doc">
            <RadioGroup v-model:value="selectDoc" :options="listDoc"/>
        </div>
    </div>
</template>

<style>
</style>