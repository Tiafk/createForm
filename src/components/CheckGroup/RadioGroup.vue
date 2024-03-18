<script setup>
import RadioGroup from './Radio/Radio.vue';

const emits = defineEmits(['update:value'])
const props = defineProps({
    value:{
        type: Array,
        required: true
    },
    options: {
        type: Array,
        required: true,
        validator: (value) => {
            const hasNameKey = value.every((option) => Object.keys(option).includes('name'))
            const hasIdKey = value.every((option) => Object.keys(option).includes('id'))
            return hasNameKey && hasIdKey
        }
    },
    re: {
        type:Boolean,
        default:false
    }
})

const check = (params) => {
    let updateValue = [...props.value]
    if(params.checked) {
        updateValue.splice(updateValue.indexOf(params.optionId), 1)
        updateValue.push(params.optionId)
    }
    emits('update:value', updateValue)
}
</script>

<template>
    <div v-for="option in options" :key="option.id">
        <RadioGroup 
            :label="option.label"
            :id="option.id"
            :name="option.name"
            :value="option.label"
            :checked="value.includes(option.id)"
            :re="re"
            group
            @updateCheckboxGroup="check"
        />
    </div>
</template>

<style lang="scss" scoped>
</style>