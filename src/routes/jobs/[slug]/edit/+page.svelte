<script>
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { goto } from "$app/navigation";
	import { getTokenFromLocalStorage, getUserId } from '/Users/aleksandr/next-bootcamp/front-end/svelte-tailwind-app/myapp/src/utils/auth.js';
    export let data;
    let formErrors = {};
    
async function postEditJob(){
goto("/");}

async function editJob(evt) {
  evt.preventDefault()
let userId = getUserId();

  const jobData = {
    user: userId,
    title: evt.target['title'].value,
    employer: evt.target['employer'].value,
    location: evt.target['location'].value,
    applicationInstructions: evt.target['applicationInstructions'].value,
    minAnnualCompensation: evt.target['minAnnualCompensation'].value,
    maxAnnualCompensation: evt.target['maxAnnualCompensation'].value,
    description: evt.target['description'].value,
    requirements: evt.target['requirements'].value,
  };
  console.log(jobData);
//   jobData.requirementsFormatted = jobData.requirements
//     .split('\n')
//     .filter(line => line.trim() !== '')
//     .map(line => `- ${line}`)
//     .join('\n');

    try {
        const resp = await fetch (PUBLIC_BACKEND_BASE_URL + `/api/collections/jobs/records/${data.job.id}`, {
    method: 'PATCH',
    mode: 'cors',
    headers: {
        'Content-Type': 'application/json', 
        'Authorization': getTokenFromLocalStorage()
    },
    body: JSON.stringify(jobData),
    });
    if (resp.status === 200) {
        postEditJob();
    } else {
      const res = await resp.json();
      formErrors = res.data;
    }
  } catch (error) {
    console.error('Error uploading job data:', error);
  }
}


</script>

<h1 class="text-center text-xl"> Edit job</h1>
<div class="flex justify-center items-center mt-8">
    <form on:submit={editJob} class="w-1/3">
        <div class="form-control w-full">
            <label class="label" for="title">
                <span class="label-text">Title</span>
            </label>
            <input 
            value={data.job.title}
                type="text"
                name="title"
                placeholder="Manager"
                class="input input-bordered w-full"
                required
            />
            {#if 'title' in formErrors}
                <label class="label" for="title">
                    <span class="label-text-alt text-red-500">{formErrors['title'].message}</span>
                </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="employer">
                <span class="label-text">Employer</span>
            </label>
            <input value={data.job.employer}
                type="employer"
                name="employer"
                placeholder="Apple Inc."
                class="input input-bordered w-full"
                required
            />
        {#if 'employer' in formErrors}
                <label class="label" for="employer">
                    <span class="label-text-alt text-red-500">{formErrors['employer'].message}</span>
                </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="location">
                <span class="label-text">Location</span>
            </label>
            <input value={data.job.location}
                type="location"
                name="location"
                placeholder="New York"
                class="input input-bordered w-full"
                required
            />
            {#if 'location' in formErrors}
                <label class="label" for="location">
                    <span class="label-text-alt text-red-500">{formErrors['location'].message}</span>
                </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="description">
                <span class="label-text"> Description </span>
            </label>
            <textarea value={data.job.description}
                type="description"
                name="description"
                placeholder="Job description"
                class="input input-bordered w-full"
                required
            />
            {#if 'description' in formErrors}
                <label class="label" for="description">
                    <span class="label-text-alt text-red-500">{formErrors['description'].message}</span>
                </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="requirements">
                <span class="label-text">Requirements</span>
            </label>
            <textarea value={data.job.requirements}
                type="requirements"
                name="requirements"
                placeholder="Enter requirements one per line"
                class="input input-bordered w-full"
                required
            />
            {#if 'requirements' in formErrors}
                <label class="label" for="requirements">
                    <span class="label-text-alt text-red-500">{formErrors['requirements'].message}</span>
                </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="applicationInstructions">
                <span class="label-text">Application instructions</span>
            </label>
            <input value={data.job.applicationInstructions}
                type="applicationInstructions"
                name="applicationInstructions"
                placeholder="How to apply"
                class="input input-bordered w-full"
                required
            />
            {#if 'applicationInstructions' in formErrors}
                <label class="label" for="applicationInstructions">
                    <span class="label-text-alt text-red-500">{formErrors['applicationInstructions'].message}</span>
                </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="minAnnualCompensation">
                <span class="label-text">Minimum Annual compensation</span>
            </label>
            <input value={data.job.minAnnualCompensation}
                type="minAnnualCompensation"
                name="minAnnualCompensation"
                placeholder="100,000 USD"
                class="input input-bordered w-full"
                required
            />
            {#if 'minAnnualCompensation' in formErrors}
                <label class="label" for="minAnnualCompensation">
                    <span class="label-text-alt text-red-500">{formErrors['minAnnualCompensation'].message}</span>
                </label>
            {/if}
        </div>
        <div class="form-control w-full">
            <label class="label" for="maxAnnualCompensation">
                <span class="label-text">Maximum Annual compensation</span>
            </label>
            <input value={data.job.maxAnnualCompensation}
                type="maxAnnualCompensation"
                name="maxAnnualCompensation"
                placeholder="200,000 USD"
                class="input input-bordered w-full"
                required
            />
            {#if 'maxAnnualCompensation' in formErrors}
                <label class="label" for="maxAnnualCompensation">
                    <span class="label-text-alt text-red-500">{formErrors['maxAnnualCompensation'].message}</span>
                </label>
            {/if}
        </div>

        <div class="form-control w-full mt-4">
            <button class="btn btn-md">Update</button>
        </div>
    </form>
</div>
