<script>
    import { fade, slide, scale } from 'svelte/transition';
    import { flip } from 'svelte/animate';
    import PollDetails from './PollDetails.svelte';
    import PollStore from '../stores/PollStore.js';
    // import { onDestroy, onMount } from 'svelte';

    // export let polls = [];

    // const unSub = PollStore.subscribe(data => {
    //     polls = data;
    // });

    // onDestroy(() => {
    //     unSub();
    // });
</script>

<div class="poll-list">
    {#each $PollStore as poll (poll.id)}
    <div in:fade out:scale|local animate:flip={{duration: 500}}>
        <PollDetails {poll} />
    </div>
    {/each}
</div>

<style lang="scss">
    .poll-list {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 20px;
    }
</style>