<script>
  import { page } from '$app/stores';
  import { goto } from '$app/navigation';

  // Sample data for dropdown menus (replace with your actual data)
  const dropdownOptions1 = ['Percentage Based', 'Amount Based', 'Interest Based','Capability Based','Others'];
  const dropdownOptions2 = ['Annually', 'Biannually', 'Quarterly','Monthly','Weekly','Daily','On Wish'];

  // State to manage additional text inputs
  let additionalInputs = [];

  function handleCreateContract() {
    goto('/slider');
  }
</script>

<style>
  .form-box {
    background-color: rgba(255, 255, 255, 0.8); /* Semi-transparent box */
    /* box-shadow: 0 0 10px rgba(0, 0, 255, 0.5); Blue shadow */
    padding: 2rem;
    border-radius: 8px;
    margin-top: 40px;
    margin-bottom: 30px;
    width: 100%;
    max-width: 600px; /* Increase the size of the box */
  }
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 200vh;
    /* background-color: #f0f4f8; */
  }
  .full-width-button {
    width: 100%;
  }
  .button-group {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  .shadow-input {
    box-shadow: 0 2px 4px rgba(9, 70, 168, 0.473); /* Light shadow */
    padding: 0.5rem;
    border-radius: 4px;
    border: 1px solid #ccc;
    width: 100%;
  }
  .shadow-input:focus {
    box-shadow: 0 2px 4px rgba(0, 0, 255, 0.3); /* Blue shadow on focus */
    border-color: #00f;
    outline: none;
  }
  .contact-box {
    background-color: #fff;
    padding: 1rem;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 1.5rem; /* Add space below the contact box */
  }
  .mb-4 {
    margin-bottom: 1rem; /* Adjust the margin for consistent spacing */
  }
  label {
    font-size: 1.25rem; /* Increase label size */
    display: block;
    margin-bottom: 0.5rem; /* Add space below labels */
  }
  .input-group {
    display: flex;
    align-items: center;
  }
  .input-group span {
    margin-right: 0.5rem;
    font-size: 1.25rem; /* Match the label size */
  }
  .header {
    text-align: center; /* Center the header text */
  }
  .milestone-container {
    display: flex;
    align-items: center;
    gap: 1rem;
  }
</style>

<div class="container">
  <div class="form-box">
    <h1 class="text-2xl font-bold mb-4 header">Contract Details</h1>
    <div class="contact-box">
      <h3 class="text-xl font-bold mb-2">Selected Contacts</h3>
      {#if $page.url.searchParams.has('options')}
        <ul>
          {#each $page.url.searchParams.get('options').split(',') as option}
            <li>{option}</li>
          {/each}
        </ul>
      {:else}
        <p>No options selected.</p>
      {/if}
    </div>

    <form on:submit|preventDefault={handleCreateContract}>
      <div class="mb-4">
        <label for="dropdown1">Type of Splits:</label>
        <select id="dropdown1" name="dropdown1" class="shadow-input">
          <option value="" disabled selected>Choose option</option>
          {#each dropdownOptions1 as option}
            <option value="{option}">{option}</option>
          {/each}
        </select>
      </div>

      <div class="mb-4">
        <label for="dropdown2">Payment Frequency:</label>
        <select id="dropdown2" name="dropdown2" class="shadow-input">
          <option value="" disabled selected>Choose option</option>
          {#each dropdownOptions2 as option}
            <option value="{option}">{option}</option>
          {/each}
        </select>
      </div>

      <div class="mb-4">
        <label for="textInput">Contribution Amount:</label>
        <div class="input-group">
          <span>₹</span>
          <input type="text" id="textInput" name="textInput" class="shadow-input" placeholder="Amount">
        </div>
      </div>

      <div class="mb-4">
        <label for="date1">Start Date:</label>
        <input type="date" id="date1" name="date1" class="shadow-input">
      </div>

      <div class="mb-4">
        <label for="date2">End Date:</label>
        <input type="date" id="date2" name="date2" class="shadow-input">
      </div>

      <div class="mb-4 milestone-container">
        <label for="milestone">Create Milestone</label>
        <button type="button" on:click={() => additionalInputs = [...additionalInputs, additionalInputs.length + 1]} class="px-2 py-1 bg-blue-900 text-blue-100 rounded hover:bg-blue-400 hover:text-white">+</button>
      </div>
      
      {#each additionalInputs as index}
        <div class="mb-4">
          <label>Milestone {index}</label><br>
          <label for="milestone-name">Milestone Title</label>
          <input type="text" placeholder="Milestone Title" class="shadow-input mb-2">
          <label for="milestone-desc">Description</label>
          <textarea placeholder="Description" class="shadow-input"></textarea>
        </div>
      {/each}

      <div class="button-group">
        <button type="submit" class="mt-4 px-4 py-2 bg-blue-900 text-blue-100 rounded hover:bg-blue-400 hover:text-white full-width-button">Create Contract</button>
      </div>
    </form>
  </div>
</div>