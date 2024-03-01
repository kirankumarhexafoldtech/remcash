<template>
  <div class="bank-account-added">
    <div class="added-bank-account-content">
      <div class="added-bank-account-header">
        <img class="icon-1" :src="addedBank" alt="image" />

        <div class="header-text">
          <img class="icon-2" :src="QIcon" alt="image" />
          <h1>Bank account added</h1>
          <p>your bank account has been successfully added!</p>
        </div>
  
      </div>
      <div class="Details-container">
        <table>
            <tr>
              <td class="bank-name">{{ bankName }} <span><img :src="bankIcon" alt="image"></span></td>
            </tr>
  
            <tr>
              <td class="acc-nbr">Account number <span>{{ accountNumber }}</span></td>
            </tr>
  
            <tr>
              <td class="acc-owner">Account owner <span>{{ accountOwner }}</span></td>
            </tr>
  
         
          </table>
          <div class="button-container">
            <button class="ok-btn">OK</button>
            <button class="add-btn">Add another account <span><i class="ri-arrow-right-s-line"></i></span>
            </button>
          </div>
        </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import addedBank from "@/assets/svg/added_bank.svg";
import QIcon from "@/assets/svg/Q_icon.svg";
import Ecobank from "@/assets/svg/ecobank.svg";

const bankName = ref("Ecobank");
const bankIcon = ref(Ecobank);
const accountNumber = ref("GH 8976 2231 0000 2110 0001");
const accountOwner = ref("Samuel Mudor");
</script>