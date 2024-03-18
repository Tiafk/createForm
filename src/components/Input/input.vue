<script setup>
const emit = defineEmits(['update:value'])
const props = defineProps({
    error: {
        type: Array,
        required: false
    },
    value:{
        type: String,
        default:''
    },
    name:{
        type:String,
        default: ''
    },
    type:{
        type:String,
        default:'text'
    },
    label:{
        type:String,
        required: true
    },
    re: {
        type: Boolean,
        default:false
    }
})

const updateValue = (e) => {
    emit('update:value', e.target.value)
}
</script>


<template>
    <div class="item">
        <div className="entryarea">
            <input 
                className="some_input" 
                :type="type" 
                :name="name"
                :value="value"
                :required="re"
                @input="updateValue"
                :placeholder="label">
        </div>
        <span 
            className="error" 
            v-for="element of error" 
            :key="element.$uid">{{ element.$message }}</span>
    </div>
</template>

<style lang="scss" scoped>
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