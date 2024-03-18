<template>
  <div class="group">
    <h3>Выберете группу: *</h3>
    <div class="drop-down-wrapper" @click="isDropDownVisible = true" ref="dropDown">
      <div class="dropdown-selected-option">
        <p>{{ selectedOption || 'Выберите группу' }}</p>
      </div>
    </div>
    <div class="wrapper-options" v-if="isDropDownVisible">
      <div class="option" v-for="(option, index) in options" :key="index" @click="toggleOptionSelect(option)">
        {{ option }}
      </div>
    </div>
    <p 
      v-if="!isOptionSelected && showGroupError"
      class="error-message">
      Пожалуйста, выберите группу
    </p>
    <input type="text" v-model="selectedOption" style="display: none" required>
  </div>
</template>

<script setup>
import { ref, defineProps, onMounted, onBeforeUnmount, computed } from 'vue';

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

const selectedOption = ref('');
const isDropDownVisible = ref(false);
const dropDown = ref(null);

const formSubmitted = ref(false);

const toggleOptionSelect = (option) => {
  selectedOption.value = option;
  isDropDownVisible.value = false;
}

const closeDropDown = (el) => {
  if (!dropDown.value.contains(el.target)) {
    isDropDownVisible.value = false;
  }
}

onMounted(() => {
  window.addEventListener('click', closeDropDown);
})

onBeforeUnmount(() => {
  window.removeEventListener('click', closeDropDown);
})

const isOptionSelected = computed(() => !!selectedOption.value);
</script>



<style lang="scss" scoped>
.error-message {
    color: red;
    font-size: 14px;
    font-weight: 500;
    margin-top: 5px;
}
.group {
  display: flex;
  width: 100%;
  flex-direction: column;
  align-self: start;

  h3 {
    display: flex;
    margin-bottom: 10px;
  }

  .drop-down-wrapper {
    cursor: pointer;
    display: flex;
    max-width: 200px;
    border: 1px solid #fff;
    border-radius: 6px;
    padding: 8px 12px;
    font-weight: 500;
  }

  .wrapper-options {
    max-width: 200px;
    border: 1px solid #fff;
    border-radius: 0 0 6px 6px;
    background-color: transparent;
    margin-top: 5px;

    .option {
      cursor: pointer;
      padding: 8px 12px;
      border: 1px solid #fff;

      &:last-child {
        border-radius: 0 0 6px 6px;
      }

      &:hover {
        background-color: #cac9c9;
      }
    }
  }
}
</style>