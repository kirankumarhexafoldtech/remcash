<template>
    <div>
       <div class="accounts">
        <div class="accounts-content">
<div class="content-header">
    <div class="content-header-text">
        <h1>Add accounts</h1>
        <p>Provide details for the following accounts</p>
    </div>
    <div class="user-options"> 
        <div class="bank-option">
            <h3 @click="handleUserBankAccount"> <span><i class="ri-bank-fill"></i></span > Add your bank accounts <span><i class="ri-arrow-right-s-line" ></i></span></h3>
        </div>
        <div class="card-option">
            <h3 @click="handleUserCards"><span><i class="ri-bank-card-fill"></i></span> Add your cards <span><i class="ri-arrow-right-s-line" ></i></span></h3>
        </div>
        
    </div>
</div>
<div class="bankAndCard-Added">
        <div class="bank-Details-container">
          <div class="bank-details">
            <label
              >Account owner <br />
              <input placeholder="Samuel Mudor" />
            </label>
            <br />
            <label
              >Choose bank from the list <br />
              <select name="bank_name">
                <option value="" disabled selected>Tap to choose...</option>
                <option value="Ecobank">Ecobank</option>
                <option value="Bank name">Bank name</option>
                <option value="Bank name">Bank name</option>
                <option value="Bank name">Bank name</option>
              </select>
            </label>
            <br />
            <label
              >Provide account number <br />
              <input placeholder="Ex: GH 8976 2231 0000 2110 0001" />
            </label>
            <div class="button">
              <button @click="handleAddbutton()">Add</button>
              <button>Cancel</button>
              <button @click="handleAddedBankAccounts()">View-added-bank-accounts</button>
            </div>
          </div>
        </div>
        <div class="card-Details-container">
          <div class="card-details">
            <div class="bankList-cardName">
              <label
                >Choose issuing bank from the list <br />
                <select name="bank_list">
                  <option value="" disabled selected>Tap to choose...</option>
                  <option value="Ecobank">Ecobank</option>
                </select>
              </label>
              <br />
              <label
                >Choose type of card <br />
                <select name="card_name">
                  <option value="" disabled selected>Tap to choose...</option>
                  <option value="Ecobank">VISA</option>
                </select>
              </label>
            </div>
            <div class="owner-name">
              <label>
                Card owner <br />
                <input placeholder="Samuel Mudor" />
              </label>
            </div>
            <div class="user-card-details">
                <div class="nbr-cvv">
                    <label>
                Provide card number<br />
                <input id="card-number" placeholder="2231 0000 2110 0001" />
              </label>
              <label>
                CVV<br />
                <input id="cvv-nbr" placeholder="140" />
              </label>
            
            </div>
              
              
            <div class="expiry-date"> 
                <label>
                Expiry date<br />
                <input id="card-expiry" placeholder="12/22" />
              </label>
            </div>
            
        </div>
        <div class="button-2">
          <button @click="handleAddbutton_2()">Add</button>
              <button>Cancel</button>
              <button @click="handleAddedCards()">View-added-cards</button>
            </div>
          </div>
        </div>
      </div>
        </div>
       </div>
    </div>
</template>

<script setup>
import {useRouter} from "vue-router"
import { ref } from "vue";

import addedBank from "@/assets/svg/added_bank.svg";
import QIcon from "@/assets/svg/Q_icon.svg";
import Ecobank from "@/assets/svg/ecobank.svg";


const router = useRouter();

function handleUserBankAccount() {
      router.push("/dashboard/bank/details");
    };

    function handleUserCards() {
      router.push("/dashboard/add/card");
    };

function handleAddedBankAccounts() {
      router.push("/dashboard/list/allBanks");
    };

    function handleAddedCards() {
      router.push("/dashboard/list/allCards");
    };

    function handleAddbutton() {
      router.push("/dashboard/bank/added");
    };

    function handleAddbutton_2() {
      router.push("/dashboard/add/card_added");
    };

const bankName = ref("Ecobank");
const bankIcon = ref(Ecobank);
const accountNumber = ref("GH 8976 2231 0000 2110 0001");
const accountOwner = ref("Samuel Mudor");




 

</script>