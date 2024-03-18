<script setup>
import { defineProps, defineEmits, ref } from 'vue';

const emit = defineEmits(['update:value']);
const props = defineProps({
    value: {
        type: String,
        default: ''
    },
    label: {
        type: String,
        required: true
    }
});

const formattedValue = ref(props.value);

const updateValue = () => {
    if (!formattedValue.value.startsWith('+7')) {
        formattedValue.value = '+7' + formattedValue.value; 
    }
    formattedValue.value = formattedValue.value.slice(0, 12);
    emit('update:value', formattedValue.value);
};

const allowOnlyNumbers = (event) => {
    const charCode = event.charCode;
    if (charCode < 48 || charCode > 57) {
        event.preventDefault();
    }
};
</script>

<template>
    <div class="item">
        <div class="entryarea">
            <input 
                class="some_input" 
                type="text"
                v-model="formattedValue"
                @input="updateValue"
                @keypress="allowOnlyNumbers"
                :placeholder="label"
                required>
        </div>
    </div>
</template>

<style lang="scss">
span {
    border:1px solid red;
    font-size: 15px;
    font-weight: 700;
    color: red;
    padding: 4px;
}

.container {
    .item {
    width: 200px;
        .entryarea {
            position: relative;
            height: 40px;
            input {
                position: absolute;
                width: 100%;
                transition: .1s ease;
                z-index: 1111;
                &:focus,
                &:valid {
                    color: rgb(23, 68, 56);
                }
            }
        }
    }
}
</style>