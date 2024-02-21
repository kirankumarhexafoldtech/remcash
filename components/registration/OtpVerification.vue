<template>
    <div class="otp">
       <h2 class="otp-heading">Enter the code from SMS</h2>
       <p class="otp-description">A 6-digit code has been sent to you. Enter the code to verify your number</p>
       <div class="otp-container">
        <p class="otp-container-text">Enter code</p>
        <div class="otp-container-box">
            <div>
                <input type="text">
                <input type="text">
                <input type="text">
            </div>
            -
            <div>
                <input type="text">
                <input type="text">
                <input type="text">
            </div>
        </div>
    </div>
    <div>
        <p>time</p>
        <button>Resend code</button>
    </div>
       <p>Go back</p>
    </div>
</template>

<script setup lang="ts">

</script>