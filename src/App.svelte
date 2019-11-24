<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "Rock";
  let title = "Taijitsu Expert";
  let image = "https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2F3.bp.blogspot.com%2F-RVdpptHzBFI%2FUSY7mjDMYtI%2FAAAAAAAADcg%2FJep1JJ1bB8Q%2Fs1600%2Fgaara%2Bvs%2Brock%2Blee.jpg&f=1&nofb=1";
	let description = "Rock vs Gaara";
	let formState = "empty";
	let createdContacts = [];

	function addContact() {
		if (name.trim().length == 0 || title.trim().length == 0 || image.trim().length == 0 || description.trim().length == 0) {
			formState = "invalid";
			return;
		}
		createdContacts = [
			...createdContacts,
			{
				id: Math.random(),
				name: name,
				jTitle: title,
				imgUrl: image,
				desc: description
			}
		];
		formState = "done";
	}

	function deleteFirst () {
		createdContacts = createdContacts.slice(1);
	}

	function deleteLast () {
		createdContacts = createdContacts.slice(0,-1);
	}
</script>

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>

<div id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={title} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={image} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
</div>

<button on:click="{addContact}">Add Contact Card</button>
<button on:click="{deleteFirst}">Delete First</button>
<button on:click="{deleteLast}">Delete Last</button>

{#if formState === "invalid"}
	<p>Invalid Input!</p>
{:else}
	<p>Please enter some data and click the button!</p>
{/if}
{#each createdContacts as contact, index (contact.id)}
	<h2>Card Number {index + 1}</h2>
	<ContactCard
		userName={contact.name}
		jobTitle={contact.jTitle}
		description={contact.desc}
		userImage={contact.imgUrl}
	/>
{:else}
	<p>Please start adding some contacts, there are none right now</p>
{/each}