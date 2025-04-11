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

  <div v-if="currentForm === 'digilockerconfirmation'">
    <PANCONFIRMATION @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'addresscommunication'">
    <ADDRESSLIST @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'failedstatus'">
    <FAILEDSTATUS @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'manualfields'">
    <MANUALFIELDS @updateDiv="handleUpdateDiv" />
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

  <div v-if="currentForm === 'signupload'">
    <SIGNUPLOAD :data="data" @updateDiv="handleUpdateDiv" />
  </div>

  <div v-if="currentForm === 'signdraw'">
    <SIGNDRAWING :data="data" @updateDiv="handleUpdateDiv" />
  </div>
 
  <div v-if="currentForm === 'thankyou'">
    <THANKINGYOU @updateDiv="handleUpdateDiv" />
  </div>
</template>

<script setup>
import NKYCList from '~/components/NKYC_Forms/nkyclist.vue'
import PAN_d from '~/components/NKYC_Forms/pandetails/pandetails.vue'
import EKYC from '~/components/NKYC_Forms/pandetails/e-kyc.vue'
import DIGILOCKSUBMISSION from '~/components/NKYC_Forms/pandetails/digilock_submission.vue'
import PANCONFIRMATION from '~/components/NKYC_Forms/pandetails/panconfirmation.vue'
import ADDRESSLIST from '~/components/NKYC_Forms/pandetails/addresslist.vue'
import FAILEDSTATUS from '~/components/NKYC_Forms/pandetails/faildstatus.vue'
import MANUALFIELDS from '~/components/NKYC_Forms/pandetails/manualfields.vue'

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
import PHOTOSIGN1 from '~/components/NKYC_Forms/photo&sign/photosign.vue'
import TAKEPHOTO from '~/components/NKYC_Forms/photo&sign/takephoto.vue'
import PHOTOPROCEED from '~/components/NKYC_Forms/photo&sign/pictureproceed.vue'
import SIGNATURE from '~/components/NKYC_Forms/photo&sign/signature.vue'
import SIGNUPLOAD from '~/components/NKYC_Forms/photo&sign/signuploaded.vue'
import SIGNDRAWING from '~/components/NKYC_Forms/photo&sign/signdraw.vue'
import THANKINGYOU from '~/components/thankyou.vue'

const currentDiv = ref('');
const currentForm = ref('nkyclist'); 
const data = ref({});

const handleUpdateDiv = (value,  newData={}) => {
currentDiv.value = value;
currentForm.value=currentDiv.value
data.value = newData;
};

</script>

<style >

</style>