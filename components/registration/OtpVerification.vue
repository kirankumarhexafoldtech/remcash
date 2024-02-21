<template>
    <div class="register-otp">
       <h2 class="register-otp-heading">Enter the code from SMS</h2>
       <p class="register-otp-description">A 6-digit code has been sent to you. Enter the code to verify your number</p>
       <div class="register-otp-container">
        <p class="register-otp-container-text">Enter code</p>
        <div class="register-otp-container-box">
            <Pin :length="6" @pin="handleOtp" :error="error" @error="clearPinError"/>
        </div>
    </div>
    <div class="register-otp-timer">
        <div>
            <p>
                Resend in
            </p>
        </div>
        <p class="register-otp-timerlink" v-if="resend" @click="handleResend">Resend</p>
        <p class="register-otp-time" v-if="!resend">
          {{ `${timer.minutes} : ${timer.seconds < 10 ? '0' : ''}${timer.seconds}` }}
        </p>
    </div >
       <p class="register-otp-back" @click="handleGoBack"><i class="ri-arrow-left-s-fill"></i>Go back</p>
    </div>
</template>

<script setup lang="ts">
import Pin from "@/components/pin/pin.vue";

const error = ref(false);
const resend = ref(false);

const timer = reactive({
  minutes:2,
  seconds:0
});



let timerId:any;

const otpEmit = defineEmits(['goback','otpverified']);

watch(timer,()=>{
  if(timer.minutes == 0 && timer.seconds == 0){
    resend.value = true;
  }
})

const startTimer = () => {
  timerId = setInterval(() => {
    if (timer.minutes === 0 && timer.seconds === 0) {
      clearInterval(timerId);
      // Timer has reached zero, perform any actions you need
      console.log('Timer reached zero!');
    } else {
      if (timer.seconds === 0) {
        timer.minutes -= 1;
        timer.seconds = 59;
      } else {
        timer.seconds-= 1;
      }
    }
  }, 1000);
};

// Call startTimer when the component is mounted
startTimer();

function handleResend(){
  startTimer();
  resend.value = false;
}

function handleOtp(data:string){
    console.log(data);
    if(data != '123456'){
        error.value = true;
        return
    };
    otpEmit('otpverified',true)
};
function clearPinError(data:boolean){
    error.value = false;
};
function handleGoBack(){
    otpEmit('goback','otp')
}
onUnmounted(() => {
      clearInterval(timerId);
});
</script>