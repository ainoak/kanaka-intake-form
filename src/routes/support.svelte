<script lang="ts">
	import GedcomFileList from '$lib/components/GedcomFileList.svelte';
import { createKanakaIntake } from '$lib/graphql-access';
	// import { createGenealogy } from '$lib/graphql-access';
	// import { isSignedIn, jwt_token, nhost, user } from '$lib/nhost';

	let message = '';

	let fileinput;

	function onFileSelected(e) {
		console.log('onFileSelected(e)');
		// let filepathToUpload = e.target.files[0];
		// let reader = new FileReader();
		// reader.readAsDataURL(filepathToUpload);
		// reader.onload = e => {
		// };
	}
	async function requestFormSubmit(e) {
		console.log('requestFormSubmit()');
		const formData = new FormData(e.target);
		const submitData = {};
		for (let field of formData) {
			const [key, value] = field;
			submitData[key] = value;
		}
		console.log('submitData: ', submitData);

		try {
			// insert kanakaintake record 
			let rv = await createKanakaIntake(submitData, 'public', '');
			console.log("rv: ", rv);
		} catch (error) {
			console.log('error: ', error);
			message = message + '; ' + error?.message;
		}
	}

	
</script>

<head>
	<link href="https://unpkg.com/material-components-web@latest/dist/material-components-web.min.css" rel="stylesheet">
	<script src="https://unpkg.com/material-components-web@latest/dist/material-components-web.min.js"></script>
	<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
</head>

<div style="color:red">{message}</div>
	<form on:submit|preventDefault={requestFormSubmit}>
		<h2>Kanaka Request Intake Form</h2>
		<h2>Step 1 Individual Info</h2>
		<div class="form-item-wrapper">
			<label for="family_name" class="form-label">Family Name</label>
			<input id="family_name" name="family_name" type="text" placeholder="Family Name" class="form-field" /><br />
			<label for="given_name" class="form-label">Given Name</label>
			<input id="given_name" name="given_name" type="text" placeholder="Given Name" class="form-field" /><br />
			<label for="birth_place" class="form-label">Birthplace</label>
			<input id="birth_place" name="birth_place" type="text" placeholder="Birthplace" class="form-field" /><br />
			<label for="birth_date" class="form-label">Birthdate</label>
			<input id="birth_date" name="birth_date" type="text" placeholder="Birthdate" class="form-field" /><br />
		</div>
		<h2>Step 2 Relationships Here</h2>
		<h3>Mother</h3>
		<div class="form-item-wrapper">
			<label for="mom_family_name" class="form-label">Mothers Family Name</label>
			<input id="mom_family_name" name="mom_family_name" type="text" placeholder="Mothers Family Name" class="form-field" /><br />
			<label for="mom_given_name" class="form-label">Mothers Given Name</label>
			<input id="mom_given_name" name="mom_given_name" type="text" placeholder="Mothers Given Name" class="form-field" /><br />
			<label for="mom_birth_place" class="form-label">Mothers Birthplace</label>
			<input id="mom_birth_place" name="mom_birth_place" type="text" placeholder="Mothers Birthplace" class="form-field" /><br />
			<label for="mom_birth_date" class="form-label">Mothers Birthdate</label>
			<input id="mom_birth_date" name="mom_birth_date" type="text" placeholder="Mothers Birthdate" class="form-field" /><br />
		</div>
		<h3>Father</h3>
		<div class="form-item-wrapper">
			<label for="dad_family_name" class="form-label">Fathers Family Name</label>
			<input id="dad_family_name" name="dad_family_name" type="text" placeholder="Fathers Family Name" class="form-field" /><br />
			<label for="dad_given_name" class="form-label">Fathers Given Name</label>
			<input id="dad_given_name" name="dad_given_name" type="text" placeholder="Fathers Given Name" class="form-field" /><br />
			<label for="dad_birth_place" class="form-label">Fathers Birthplace</label>
			<input id="dad_birth_place" name="dad_birth_place" type="text" placeholder="Fathers Birthdate" class="form-field" /><br />
			<label for="dad_birth_date" class="form-label">Fathers Birthdate</label>
			<input id="dad_birth_date" name="dad_birth_date" type="text" placeholder="Fathers Birthdate" class="form-field" /><br />
		</div>
		<h2>Step 3 Upload Documents</h2>
		<!-- <form action="/action_page.php">
			<label for="img">Select Document:</label>
			<input type="file" id="img" name="img" accept="image/*">
		</form> -->
		  
		<input type="hidden" name="" bind:this={fileinput} />
<!-- 
		<img
			class="upload"
			src="https://static.thenounproject.com/png/625182-200.png"
			alt=""
			on:click={() => {
				fileinput.click();
			}}
		/>
		<div
			class="chan"
			on:click={() => {
				fileinput.click();
			}}
		>
			Choose GEDCOM file
		</div>
		<input
			name="gedcomfile"
			type="file"
			accept=".ged, .gedcom"
			on:change={(e) => onFileSelected(e)}
			bind:this={fileinput}
		/> -->
		<!-- <input type="submit" value="Submit/Upload" /> -->
		<button class="mdc-button mdc-button--raised">
			<span class="mdc-button__label">Submit</span>
		</button>
	</form>





<style>
	.upload {
		display: flex;
		height: 50px;
		width: 50px;
		cursor: pointer;
	}
</style>
