<template>
    <div class="pin" ref="container">
        <input type="text" v-for="n in length" :key="n" 
        @keyup="(e) => handleEnter(e, n-1)"
        maxLength="1" v-model="pinArray[n-1]" :class="error ? 'pin-input pin-red' : 'pin-input'"/>
    </div>
</template>

<script setup lang="ts">
const pinProps = defineProps({
    length:{
        type:Number,
        default:4
    },
    error:{
        type:Boolean,
        default:false
    }
});
const container = ref()
const pinArray = ref(['']);
const pinEmit = defineEmits(['pin','error'])
function handleEnter(e, i){
    const children = container.value.children;
    const keyPressed = e.key;
    pinEmit('error',false)
    if(i>=0 && (keyPressed == 'Backspace' || keyPressed == 'Delete')){
        pinArray.value[i] = null;
        if(i != 0){
            children[i-1].focus();
            setTimeout(()=>{
            },100)
        }
    }else{
        const matched = keyPressed.match(/^[0-9]$/);
        if(pinArray.value[i] == ''){
            return
        }
        if(!matched){
            pinArray.value[i] = '';
            return
        }else if( i < pinProps.length-1){
            children[i+1].focus();
            setTimeout(() => {
                }, 100);
        }else{
            pinEmit("pin",pinArray.value.join(""));
        }
    }

    
};
onMounted(()=>{
    const children = container.value.children;
    children[0].focus();
    pinArray.value = ['']
})
</script>