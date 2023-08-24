<script>
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import SvelteMarkdown from 'svelte-markdown';
    import humanize from 'humanize-plus';
    import { goto } from "$app/navigation";
	import { getUserId } from '../../../utils/auth';
    let formErrors = {};
    
async function postCreateJob(){
goto("/");}

async function createJob(evt) {
  evt.preventDefault()
let userid = getUserId();

  const jobData = {
    user: userid,
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
        const resp = await fetch (PUBLIC_BACKEND_BASE_URL + '/api/collections/jobs/records', {
    method: 'POST',
    mode: 'cors',
    headers: {
        'Content-Type': 'application/json',
    },
    body: JSON.stringify(jobData),
    });
    if (resp.status === 200) {
        postCreateJob();
    } else {
      const res = await resp.json();
      formErrors = res.data;
    }
  } catch (error) {
    console.error('Error uploading job data:', error);
  }
}


</script>

<h1 class="text-center text-xl"> Post a job</h1>
<div class="flex justify-center items-center mt-8">
    <form on:submit={createJob} class="w-1/3">
        <div class="form-control w-full">
            <label class="label" for="title">
                <span class="label-text">Title</span>
            </label>
            <input
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
            <input
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
            <input
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
            <textarea
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
            <textarea
                type="requirements"
                name="requirements"
                placeholder="Enter requirements one per line"
                class="input input-bordered w-full"
                required
            />
            {#if 'quirements' in formErrors}
                <label class="label" for="requirements">
                    <span class="label-text-alt text-red-500">{formErrors['requirements'].message}</span>
                </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="applicationInstructions">
                <span class="label-text">Application instructions</span>
            </label>
            <input
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
            <input
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
            <input
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
            <button class="btn btn-md">Submit</button>
        </div>
    </form>
</div>
