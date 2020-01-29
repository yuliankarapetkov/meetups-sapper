<script>
    import { writable } from 'svelte/store';

    import meetups from '../stores/meetups.js';
    
	import Button from '../components/shared/Button.svelte';
	
    import MeetupForm from '../components/Meetups/MeetupForm.svelte';
    import MeetupGrid from '../components/Meetups/MeetupGrid.svelte';

    let meetupFormVisible = false;

    const meetupInitialvalue = writable(null);
    let meetup = meetupInitialvalue;

    function saveMeetup(event) {
        const m = event.detail;

        if (m.id) {
            meetups.updateMeetup(m.id, m);
        } else {
            meetups.addMeetup(m);
        }

        closeMeetupFormModal();
    }

    function editMeetup(event) {
        const id = event.detail;
        meetup = meetups.getMeetup(id);

        toggleMeetupForm();
    }

    function deleteMeetup(event) {
        const id = event.detail;
        meetups.deleteMeetup(id);

        closeMeetupFormModal();
    }

    function toggleFavorite(event) {
        const id = event.detail;
        meetups.toggleFavorite(id);
    }

    function toggleMeetupForm() {
        meetupFormVisible = !meetupFormVisible;
    }

    function closeMeetupFormModal() {
        toggleMeetupForm();
        meetup = meetupInitialvalue;
    }
</script>

<style>
</style>

<svelte:head>
	<title>Meetups</title>
</svelte:head>

<Button on:click="{toggleMeetupForm}">
	Add Meetup
</Button>

<MeetupGrid
	meetups={$meetups}
	on:toggleFavorite="{toggleFavorite}"
	on:edit="{editMeetup}" />

{#if meetupFormVisible}
	<MeetupForm
		meetup={$meetup}
		on:save="{saveMeetup}"
		on:cancel="{closeMeetupFormModal}"
		on:delete="{deleteMeetup}" />
{/if}
