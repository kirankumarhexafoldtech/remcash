<template>
    <div class="card-added">
       <div class="card-added-content">
<div class="card-content-header">
    <img class="icon-1" :src="bankCards" alt="image" />
  
  <div class="header-text">
    <img class="icon-2" :src="QIcon" alt="image" />
    <h1>New card added</h1>
    <p>your card has been successfully added!</p>
  </div>
</div>

<div class="card-container">
    <img class="card-img" :src="card5" alt="image" />
</div>

<div class="button-container">
              <button class="ok-btn">OK</button>
              <button class="add-btn" @click="handleAddAnotherAccount()">Add another account<span><i class="ri-arrow-right-s-line"></i></span>
              </button>
            </div>
       </div>
    </div>
</template>

<script setup>
  import bankCards from "@/assets/svg/bank_cards.svg";
  import QIcon from "@/assets/svg/Q_icon.svg";
  import card5 from "@/assets/svg/card5.svg";
  import { useRouter } from "vue-router";

  const router = useRouter();

function handleAddAnotherAccount() {
      router.push("/dashboard/accounts");
    };

</script>