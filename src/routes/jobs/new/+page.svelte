<script>
        // AKU RASA KAN AKU KENA REVIEW BALIK LAH CODE DIA AAAAAAAAAA
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { goto } from '$app/navigation';
    import { getUserId } from  '../../../utils/auth.js'

    // jap kenapa kena ada ni eh aku tak ingat
    let formErrors = {};

    // prevent event occuring if there is a default 
    async function createJob(evt) {
      evt.preventDefault();
      const getLocalData = getUserId()

    

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
      const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/api/collections/jobs/records', {
        method: 'POST',
        mode: 'cors',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(jobData)
      });
  
      if (resp.status == 200) {
        goto('/')
    } else {
      const res = await resp.json();
      formErrors = res.data;
    }
}
  

  </script>


<div class="container mx-auto px-2 lg:px-0"> 
    <form on:submit={createJob}>
    <div class="alert-warning alert-info alert-error alert-success hidden"></div> 
    <form>
        <div class="form-control w-full">
            <label class="label" for="title">
                <span class="label-text">Job Title</span>
            </label> 
            <input type="text" name="title" placeholder="Software Engineer" class="input input-bordered w-full"> 
        </div> 
        <div class="form-control w-full">
            <label class="label" for="title">
                <span class="label-text">Min Annual Compensation</span>
            </label> 
            <input type="number" name="minAnnualCompensation" placeholder="40000" class="input input-bordered w-full">  
            <label class="label" for="salary">
                <span class="label-text-alt">USD</span> 
                <span class="label-text-alt">per annum</span>
            </label>
        </div> 
        <div class="form-control w-full">
            <label class="label" for="title">
                <span class="label-text">Max Annual Compensation</span>
            </label>
             <input type="number" name="maxAnnualCompensation" placeholder="250000" class="input input-bordered w-full"> 
              <label class="label" for="salary">
                <span class="label-text-alt">USD</span> 
                <span class="label-text-alt">per annum</span>
            </label>
        </div> 
        <div class="form-control w-full">
            <label class="label" for="salary">
                <span class="label-text">Company Name</span>
            </label> 
            <input type="text" name="employer" placeholder="e.g. Facebook" class="input input-bordered w-full"> 
        </div>
         <div class="form-control w-full">
            <label class="label" for="salary">
                <span class="label-text">Job Location</span>
            </label> 
            <input type="text" name="location" placeholder="e.g. Singapore" class="input input-bordered w-full"> 
        </div> 
        <div class="form-control">
            <label class="label" for="description">
                <span class="label-text">Description</span>
            </label> 
            <textarea class="textarea textarea-bordered h-64" name="description" placeholder=""></textarea> 
        </div> 
        <div class="form-control">
            <label class="label" for="requirements">
                <span class="label-text">Requirements</span>
            </label> 
            <textarea class="textarea textarea-bordered h-64" name="requirements" placeholder=""></textarea> 
        </div> 
        <div class="form-control">
            <label class="label" for="application-instruction">
                <span class="label-text">Application Instructions</span>
            </label> 
            <textarea class="textarea textarea-bordered h-24" name="applicationInstructions" placeholder=""></textarea>
         </div> 
         <div class="form-control w-full mt-8">
            <button class="btn btn-md">"Post a Job"</button>
        </div>
    </form>
    </div>
    
