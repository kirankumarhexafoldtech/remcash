<template>
  <div class="main_auth">
    <div class="main_auth_left">
      <div class="main_auth_left-top">
        <img :src="leftScrollContent[leftScrollContentPosition].img" alt="" ref="imageRef" class="leftImage" />
      </div>
      <div class="main_auth_left-bottom">
        <h2>
          {{ leftScrollContent[leftScrollContentPosition].heading }}
        </h2>
        <p>
          {{
            leftScrollContent[leftScrollContentPosition]
              .description
          }}
        </p>
      </div>
    </div>
    <div class="main_auth_right">
      <div class="main_auth_form">
        <div class="register-bar-container">
          <div class="register-bar">
            <div :class="barDetails.register ?  'register-bar-point register-bar-point-active' : current == 'register' ? 'register-bar-point register-bar-point-blink' : 'register-bar-point'"></div>
            <div :class="barDetails.otp ?  'register-bar-point register-bar-point-active' : current == 'otp' ? 'register-bar-point register-bar-point-blink' : 'register-bar-point'"></div>
            <div  :class="barDetails.identityConfirmation ?  'register-bar-point register-bar-point-active' : current == 'identity' ? 'register-bar-point register-bar-point-blink' : 'register-bar-point'"></div>
            <div class="register-bar-point"></div>
            <div class="register-bar-point"></div>
          </div>
        </div>
        <div class="main_auth_logo">
          <img :src="RamecashLogo" alt="" />
          <p>Remcash</p>
        </div>
        <Register @registerDetails="handleRegistration" v-if="current == 'register'" :data="registrationProcess.register"/>
        <OtpVerification v-if="current == 'otp'" @goback="handleGoBack" @otpverified="handleOtpVerified"/>
        <IdentityConfirmation v-if="current == 'identity'"
        @goback="handleGoBack"
        />
      </div>
      <div class="main_auth_background">
        <img :src="BackgroundImage" alt="" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import Wallet from "@/assets/svg/wallet.svg";
import PayBills from "@/assets/svg/pay_bills.svg";
import MoneyTransfer from "@/assets/svg/instant_money_tranfer.svg";
import BackgroundImage from "@/assets/svg/bg_glob.svg";
import RamecashLogo from "@/assets/svg/logo01.svg";
import Register from "@/components/registration/Register.vue";
import OtpVerification from "@/components/registration/OtpVerification.vue";
import IdentityConfirmation from "@/components/registration/IdentityConfirmation.vue";

const leftScrollContent = reactive([
  {
    img: Wallet,
    heading: "Secure digital wallet",
    description:
      "Remcash provides a fully secure digital wallet to ease everyday transactions",
  },
  {
    img: PayBills,
    heading: "Instant money transfer",
    description:
      "Remcash provides fast, secure and instant money transfers across the globe",
  },
  {
    img: MoneyTransfer,
    heading: "Pay the bills easily",
    description:
      "With Remcash, paying bills is quick and easy, fully secure and convenient",
  },
]);
// current bar value
const current = ref("");
// carosel conttent reference variable
const leftScrollContentPosition = ref(0);
// carousel content method
const leftScroll = () => {
  // Add data attribute to trigger transition
  leftScrollContentPosition.value =
    (leftScrollContentPosition.value + 1) % leftScrollContent.length;
};
// functions
const handleRegisterView = (data: boolean) => {
  //    showForm.value = "register"
};
// select different id

interface Register {
  first_name:string,
  last_name:string,
  phone:string,
  email:string
};
const registrationProcess = reactive({
  register: {
    first_name: '',
    last_name: "",
    phone: "",
    email: ""
  } as Register,
});
const barDetails = reactive({
  register: false,
  otp: false,
  identityConfirmation:false
});

let intervalId:any;
// registration process
const handleRegistration = (data:Register) =>{
   registrationProcess.register = data;
   barDetails.register = true;
   current.value = "otp";
   const sessionData = JSON.stringify(registrationProcess)
   sessionStorage.setItem("r_data",sessionData);
};
function handleGoBack(data:string){
  barDetails.otp = false;
  barDetails.register = false;
  barDetails.identityConfirmation = false;
  current.value = "register";
}
function handleOtpVerified(data:boolean){
  if(data){
    barDetails.otp = true;
    current.value = "identity";
  }
}
// life cycle hooks
onMounted(async() => {
  const storedData = sessionStorage.getItem("r_data");
  if(storedData){
    const unPackData =await JSON.parse(storedData);
    registrationProcess.register = unPackData.register;
    console.log("registration process register",registrationProcess.register)
  };
  // set current value to register
  current.value = "register";
  intervalId = setInterval(leftScroll, 5000); // Change image every 5000 milliseconds (5 seconds)
  // Clear the interval when the component is unmounted
});
onBeforeUnmount(() => {
  clearInterval(intervalId);
});
definePageMeta({
  layout: false
})
</script>   