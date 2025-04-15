<template>
 
    <div v-if="currentForm === 'nkyclist'">
    <NKYCList @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'pandetails'">
    <PAN_d @updateDiv="handleUpdateDiv" />
  </div>
 
  <div v-if="currentForm === 'ekyc'">
    <EKYC @updateDiv="handleUpdateDiv" />
  </div>
  
  <div v-if="currentForm === 'digilockersubmission'">
    <DIGILOCKSUBMISSION @updateDiv="handleUpdateDiv" />
  </div>

  

  <div v-if="currentForm === 'parmanentaddress'">
    <PARMANENTADDRESS @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'failedstatus'">
    <FAILEDSTATUS @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'communicationaddress'">
    <COMMUNICATIONADDRESS @updateDiv="handleUpdateDiv" />
  </div>



  <div v-if="currentForm === 'submission'">
    <SUBMISSIONFORM :data="data" @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'info'">
    <MARRIEDSTATUS  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'clientinfo'">
    <CLIENTINFO  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'qualification'">
    <QUALIFICATION @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'occupation'">
    <OCCUPATION  @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'tradingexperience'">
    <TRADINGEXPERIENCE  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'income'">
    <INCOME  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'nominee'">
    <NOMINEE  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'bank1'">
    <BANK1  @updateDiv="handleUpdateDiv" />
  </div>


  <div v-if="currentForm === 'bank4'">
    <BANK4 :data="data"  @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'tradingsegment'">
    <TRADINGSEGMENT :data="data"  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'brokerage'">
    <BROKERAGE :data="data"  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'uploadproof'">
    <UPLOADPROOF :data="data"  @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'photosign1'">
    <PHOTOSIGN1  @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'takephoto'">
    <TAKEPHOTO  @updateDiv="handleUpdateDiv"  />
  </div>

  <div v-if="currentForm === 'photoproceed'">
    <PHOTOPROCEED :data="data"  @updateDiv="handleUpdateDiv" />
   
  </div>

  <div v-if="currentForm === 'signature'">
    <SIGNATURE   @updateDiv="handleUpdateDiv" />
  </div>

  

  <div v-if="currentForm === 'signdraw'">
    <SIGNDRAWING :data="data" @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'additionalinformation'">
    <ADDITIONALINFO :data="data" @updateDiv="handleUpdateDiv" />
  </div>
 
 
  <div v-if="currentForm === 'thankyou'">
    <THANKINGYOU @updateDiv="handleUpdateDiv" />
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

import NKYCList from '~/components/NKYC_Forms/nkyclist.vue'
import PAN_d from '~/components/NKYC_Forms/pandetails/pandetails.vue'
import EKYC from '~/components/NKYC_Forms/pandetails/e-kyc.vue'
import DIGILOCKSUBMISSION from '~/components/NKYC_Forms/pandetails/digilock_submission.vue'
import PARMANENTADDRESS from '~/components/NKYC_Forms/pandetails/parmanentaddress.vue'
import FAILEDSTATUS from '~/components/NKYC_Forms/pandetails/faildstatus.vue'
import COMMUNICATIONADDRESS from '~/components/NKYC_Forms/pandetails/communicationaddress.vue'

import SUBMISSIONFORM from '~/components/NKYC_Forms/submissionpage.vue'
import MARRIEDSTATUS from '~/components/NKYC_Forms/profiledetails/marridestatus.vue'
import CLIENTINFO from '~/components/NKYC_Forms/profiledetails/clientinfo.vue'
import QUALIFICATION from '~/components/NKYC_Forms/profiledetails/qualification.vue'
import OCCUPATION from '~/components/NKYC_Forms/profiledetails/occupationstatus.vue'
import TRADINGEXPERIENCE from '~/components/NKYC_Forms/profiledetails/tradingexperience.vue'

import INCOME from '~/components/NKYC_Forms/profiledetails/incomestatus.vue'
import NOMINEE from '~/components/NKYC_Forms/profiledetails/nominee.vue'
import BANK1 from '~/components/NKYC_Forms/bankdetails/bank1.vue'
import BANK4 from '~/components/NKYC_Forms/bankdetails/bank4.vue'
import TRADINGSEGMENT from '~/components/NKYC_Forms/account/tradingsegment.vue'
import BROKERAGE from '~/components/NKYC_Forms/account/brokerage.vue'
import UPLOADPROOF from '~/components/NKYC_Forms/account/uploadproof.vue'

import PHOTOSIGN1 from '~/components/NKYC_Forms/photo&sign/photosign.vue'
import TAKEPHOTO from '~/components/NKYC_Forms/photo&sign/takephoto.vue'
import PHOTOPROCEED from '~/components/NKYC_Forms/photo&sign/pictureproceed.vue'
import SIGNATURE from '~/components/NKYC_Forms/photo&sign/signature.vue'
import SIGNDRAWING from '~/components/NKYC_Forms/photo&sign/signdraw.vue'
import ADDITIONALINFO from '~/components/NKYC_Forms/photo&sign/documentconfirmation.vue'

import THANKINGYOU from '~/components/thankyou.vue'
const currentForm = ref('nkyclist') // default form
const data = ref({})
const formHistory = ref([{ form: 'nkyclist', formData: {} }]) // store form and its data

const handleUpdateDiv = (value, newData = {}) => {
  currentForm.value = value
  data.value = newData

  // Store both form and data
  formHistory.value.push({ form: value, formData: newData })
  history.pushState({ div: value, formData: newData }, '', '')
}

const handleBackButton = (event) => {
  if (formHistory.value.length > 1) {
    formHistory.value.pop()
    const previous = formHistory.value[formHistory.value.length - 1]

    currentForm.value = previous.form
    data.value = previous.formData || {}
  } else {
    history.back()
  }
}

onMounted(() => {
  history.replaceState({ div: 'nkyclist', formData: {} }, '', '')
  window.addEventListener('popstate', handleBackButton)
})

onBeforeUnmount(() => {
  window.removeEventListener('popstate', handleBackButton)
})
</script>


<style >

</style>