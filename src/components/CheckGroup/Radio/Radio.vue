<script setup>
const emits = defineEmits(['update:checked', 'updateCheckboxGroup'])
const props = defineProps({
    name: {
        type: String,
        required: false
    },
    id: {
        type: String,
        default: ''
    },
    value: {
        type: String,
        default: ''
    },
    label: {
        type: String,
        default: ''
    },
    checked: {
        type: Boolean,
        default: false
    },
    group: {
        type: Boolean,
        default: false
    }, 
    re: {
        type:Boolean,
        default:false
    }
})

const handleClick = (event) => {
    if(props.group) {
        emits('updateCheckboxGroup', {optionId: props.id, checked: event.target.checked})
    } else {
        emits('update:checked', event.target.checked)
    }
}
</script>

<template>
    <div class="item">
        <input 
            type="radio" 
            :id="id"
            :name="name" 
            :value="value" 
            :checked="checked" 
            @input="handleClick($event)"
            :required="re"
        >
        <label :for="id" className="text">{{label}}</label>
    </div>
</template>