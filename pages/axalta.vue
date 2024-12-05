<template>
  <form @submit.prevent="submitForm" class="max-w-md mx-auto mt-8">
    <input type="hidden" name="oid" value="00D50000000dGxN">
    <input type="hidden" name="retURL" value="http://www.google.com">
    <input type="hidden" name="recordType" value="01250000000ELu3">
    <input type="hidden" name="Lead_Queue__c" value="LA Leads Distributor">
    <input type="hidden" name="Origin_URL__c" value="/pruebaContacto">

    <div class="mb-4">
      <label for="first_name" class="block text-sm font-medium text-gray-700">First Name</label>
      <input v-model="formData.first_name" id="first_name" maxlength="40" name="first_name" type="text" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50">
    </div>

    <div class="mb-4">
      <label for="last_name" class="block text-sm font-medium text-gray-700">Last Name</label>
      <input v-model="formData.last_name" id="last_name" maxlength="80" name="last_name" type="text" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50">
    </div>

    <div class="mb-4">
      <label for="company" class="block text-sm font-medium text-gray-700">Company</label>
      <input v-model="formData.company" id="company" maxlength="40" name="company" type="text" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50">
    </div>

    <div class="mb-4">
      <label for="country_code" class="block text-sm font-medium text-gray-700">Country</label>
      <select v-model="formData.country_code" id="country_code" name="country_code" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50">
        <option value="MX">México</option>
        <option value="AR">Argentina</option>
        <option value="BR">Brasil</option>
        <option value="CL">Chile</option>
        <option value="CO">Colombia</option>
        <option value="CR">Costa Rica</option>
        <option value="SV">El Salvador</option>
        <option value="GT">Guatemala</option>
        <option value="HN">Honduras</option>
        <option value="NI">Nicaragua</option>
        <option value="PA">Panamá</option>
        <option value="PE">Perú</option>
        <option value="DO">República Dominicana</option>
        <option value="VE">Venezuela</option>
      </select>
    </div>

    <div class="mb-4">
      <label for="city" class="block text-sm font-medium text-gray-700">City</label>
      <input v-model="formData.city" id="city" maxlength="40" name="city" type="text" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50">
    </div>

    <div class="mb-4">
      <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
      <input v-model="formData.email" id="email" maxlength="80" name="email" type="email" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50">
    </div>

    <div class="mb-4">
      <label for="phone" class="block text-sm font-medium text-gray-700">Phone</label>
      <input v-model="formData.phone" id="phone" maxlength="40" name="phone" type="tel" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50">
    </div>

    <div class="mb-4">
      <label for="Account_Comments__c" class="block text-sm font-medium text-gray-700">Account Comments</label>
      <textarea v-model="formData.Account_Comments__c" id="Account_Comments__c" name="Account_Comments__c" rows="3" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"></textarea>
    </div>

    <div class="mt-6">
      <button type="submit" class="w-full px-4 py-2 bg-indigo-600 text-white rounded-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
        Submit
      </button>
    </div>
  </form>
</template>

<script setup>
import { ref } from 'vue'

const formData = ref({
  first_name: '',
  last_name: '',
  company: '',
  country_code: '',
  city: '',
  email: '',
  phone: '',
  Account_Comments__c: ''
})

const submitForm = async () => {
  try {
    const response = await fetch('https://webto.salesforce.com/servlet/servlet.WebToLead?encoding=UTF-8&orgId=00D50000000dGxN', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded',
      },
      body: new URLSearchParams({
        ...formData.value,
        oid: '00D50000000dGxN',
        retURL: 'http://www.google.com',
        recordType: '01250000000ELu3',
        Lead_Queue__c: 'LA Leads Distributor',
        Origin_URL__c: '/pruebaContacto'
      })
    })

    if (response.ok) {
      console.log('Form submitted successfully')
      // Aquí puedes agregar lógica adicional después de enviar el formulario
    } else {
      console.error('Form submission failed')
    }
  } catch (error) {
    console.error('Error submitting form:', error)
  }
}
</script>