<template>
    <div class="card">
        <div class="card-content">
          <div class="content-header-container">
            <div class="card-header-text">
                <h1>Add a card</h1>
                <p>To add a new card, please provide the following information</p>
            </div>
            <div class="card-selectInput">
          <i class="ri-bank-fill"></i>
          <input placeholder="Add your cards" />
        </div>
       
          </div>  
          <div class="card-details-container">
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
        Card owner <br>
        <input placeholder="Samuel Mudor">
        </label>
     </div>
     <div class="card-details">
       <label>
        Provide card number<br>
        <input id="card-number" placeholder="2231 0000 2110 0001">
       </label>
       <label>
        CVV<br>
        <input id="cvv-nbr" placeholder="140">
       </label>
       <label>
        Expiry date<br>
        <input id="card-expiry" placeholder="12/22">
       </label>
     </div>
     <div class="button-container">
              <button class="cancel-btn">Cancel</button>
              <button class="add-btn" @click="handleAddNewCard">Add new card<span><i class="ri-arrow-right-s-line"></i></span>
              </button>
            </div>
      </div>
        </div>
        
    </div>
</template>


<script setup>
import {useRouter} from "vue-router"

const router = useRouter();

function handleAddNewCard() {
      router.push("/dashboard/add/card_added");
    };

</script>