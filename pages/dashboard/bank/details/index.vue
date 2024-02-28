<template>
  <div class="add-bank-account">
    <div class="bank-account-content">
      <div class="bank-account-header-container">
        <div class="bank-account-header-text">
          <h1>Add a bank account</h1>
          <p>To add a bank account, please provide the following information</p>
        </div>
        <div class="bank-account-header-selectInput">
          <i class="ri-bank-fill"></i>
          <input placeholder="Add your bank accounts" />
        </div>
      </div>
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
      </div>

      <div class="button-container">
        <button class="cancel-btn">Cancel</button>
        <button class="add-btn">
          Add bank account <span><i class="ri-arrow-right-s-line"></i></span>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup></script>
