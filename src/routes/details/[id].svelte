<script context="module">
    export function preload({ params }) {
        const { id } = params;
        return { id };
    }
</script>

<script>
    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';

    import MeetupDetail from '../../components/Meetups/MeetupDetail.svelte';
    import meetups from '../../stores/meetups.js';

    export let id;

    let meetup;

    onMount(() => {
        meetup = meetups.getMeetup(id);
    });
</script>

{#if $meetup} 
    <MeetupDetail meetup={$meetup} />
{:else}
    Loading..
{/if}