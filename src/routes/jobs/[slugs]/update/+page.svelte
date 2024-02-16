<script>
    // AKU RASA KAN AKU KENA REVIEW BALIK LAH CODE DIA
import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
import { goto } from '$app/navigation';
import { getUserId, getTokenFromLocalStorage } from  './../../../utils/auth.js';

// I have to export data for what
export let data;

//wait what this clicked for idk 
let clicked = false;

// jap kenapa kena ada ni eh aku tak ingat
let formErrors = {};

async function updateJob(){
    goto(`/jobs/${data.job.id}`)
}

// prevent event occuring if there is a default 
async function editJob(evt) {
  evt.preventDefault();

  const getLocalData = getUserId()
  const getToken = getTokenFromLocalStorage();



// THE NAME MUST FOLLOW THE API PIPELINES
// CAN REFER TO THE WEBSITE
const jobData = {
    user : getLocalData,
    title : evt.target['title'].value,
    minAnnualCompensation : evt.target['minAnnualCompensation'].value,
    maxAnnualCompensation : evt.target['maxAnnualCompensation'].value,
    description : evt.target['description'].value,
    requirements : evt.target['requirements'].value,
    applicationInstructions : evt.target['applicationInstructions'].value,
    location :  evt.target['location'].value,
    employer :  evt.target['employer'].value,

  };

  // STATUS OF THE USERS
  const resp = await fetch(PUBLIC_BACKEND_BASE_URL + `/api/collections/jobs/records ${data.job.id}`, {
    method: 'PATCH',
    mode: 'cors',
    headers: {
      'Content-Type': 'application/json',
      Authorization: getToken
    },
    body: JSON.stringify(jobData)
  });

  if (resp.status == 200) {
    updateJob();

} else {
  const res = await resp.json();
  formErrors = res.data;
  clicked = false;
}
}


</script>



<h1 class="text-center text-xl font-bold">Update Job Details</h1>
<div class="container mx-auto px-2 lg:px-0"> 
    <form on:submit={editJob}>
<div class="alert-warning alert-info alert-error alert-success hidden"></div> 
<form>
    <div class="form-control w-full">
        <label class="label" for="title">
            <span class="label-text">Job Title</span>
        </label> 
        <input value= {data.job.title} type="text" name="title" placeholder="Software Engineer" class="input input-bordered w-full"> 
    </div> 
    <div class="form-control w-full">
        <label class="label" for="title">
            <span class="label-text">Min Annual Compensation</span>
        </label> 
        <input value= {data.job.minAnnualCompensation} type="number" name="minAnnualCompensation" placeholder="40000" class="input input-bordered w-full">  
        <label class="label" for="salary">
            <span class="label-text-alt">USD</span> 
            <span class="label-text-alt">per annum</span>
        </label>
    </div> 
    <div class="form-control w-full">
        <label class="label" for="title">
            <span class="label-text">Max Annual Compensation</span>
        </label>
         <input value={data.job.maxAnnualCompensation} type="number" name="maxAnnualCompensation" placeholder="250000" class="input input-bordered w-full"> 
          <label class="label" for="salary">
            <span class="label-text-alt">USD</span> 
            <span class="label-text-alt">per annum</span>
        </label>
    </div> 
    <div class="form-control w-full">
        <label class="label" for="salary">
            <span class="label-text">Company Name</span>
        </label> 
        <input value={data.job.employer} type="text" name="employer" placeholder="e.g. Facebook" class="input input-bordered w-full"> 
    </div>
     <div class="form-control w-full">
        <label class="label" for="salary">
            <span class="label-text">Job Location</span>
        </label> 
        <input value={data.job.location} type="text" name="location" placeholder="e.g. Singapore" class="input input-bordered w-full"> 
    </div> 
    <div class="form-control">
        <label class="label" for="description">
            <span class="label-text">Description</span>
        </label> 
        <textarea value={data.job.description} class="textarea textarea-bordered h-64" name="description" placeholder=""></textarea> 
    </div> 
    <div class="form-control">
        <label class="label" for="requirements">
            <span class="label-text">Requirements</span>
        </label> 
        <textarea value={data.job.requirements} class="textarea textarea-bordered h-64" name="requirements" placeholder=""></textarea> 
    </div> 
    <div class="form-control">
        <label class="label" for="application-instruction">
            <span class="label-text">Application Instructions</span>
        </label> 
        <textarea value={data.job.applicationInstructions} class="textarea textarea-bordered h-24" name="applicationInstructions" placeholder=""></textarea>
     </div> 
     <div class="form-control w-full mt-8">
        <button class="btn btn-md">"Post a Job"</button>
    </div>


    {#if clicked}
    <button class="btn btn-secondary w-full mt-8">
        <span class="loading loading-spinner"></span>
        loading...
    </button> 
    {:else}
    <button class="btn btn-secondary w-full mt-8" type="submit"> Post Job </button> 
    {/if}
    </form>
</div>

<div class="mt-28"></div>
