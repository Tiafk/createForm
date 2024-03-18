
<template>
    <div class="wrapper">
      <form class="form" @submit.prevent="submitForm()">
        <h3 class="title">Создание клиента</h3>
        <div class="container">
          <Attribute 
            :options="options" 
            :listGender="listGender"
            :listDoc="listDoc"
            :v="v"
            :showGroupError="showGroupError"
          />
          <Address/>
          <PassportDate/>
          <label class="sms-wrapper">
            <p class="text_item">Не отправлять СМС</p>
            <input type="checkbox" class="real-checkbox" />
            <span class="custom-checkbox"></span>
          </label>
        </div>
        <button type="submit" class="btn active">Создать</button>
      </form>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue'
  import { minLength, helpers } from '@vuelidate/validators'

  import useVuelidate from '@vuelidate/core'
  import Attribute from './components/Attribute.vue';
  import Address from './components/Address.vue';
  import PassportDate from './components/PassportDate.vue';
  
  const options = ref(['VIP', 'Проблемные', 'ОМС'])
  const listGender = ref([
    {name:'gender', id:'men', label:'Мужчина'},
    {name:'gender', id:'women', label:'Женщина'}
  ])

  const listDoc = ref([
    {name:'doctor', id:'ivanov', label:'Иванов'},
    {name:'doctor', id:'zaharov', label:'Захаров'},
    {name:'doctor', id:'chernsheva', label:'Чернышева'}
  ])

  //Phone number
  const phoneField = ref('')
  const rules = computed(() => ({
    phoneField: {
      minLength: helpers.withMessage('Некорректно заполненное поле',minLength(1)),
    }
  }))
  const v = useVuelidate(rules, {phoneField})
  

  //Group false
  const showGroupError = ref(false);
  
  //Form validate
  const submitForm = () => {
    if (!isGroupValid()) {
      showGroupError.value = true;
      return;
    }
    alert("Форма отправлена");
  }
  
  const isGroupValid = () => {
    return true;
  }
  </script>