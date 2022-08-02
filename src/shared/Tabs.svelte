<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    export let items;
    export let activeItem;

</script>

<div class="tabs">
    <ul>
        {#each items as item}
            <li on:click={() => {dispatch('tabChange', item)}}>
                <div class:active={item === activeItem}>{item}</div>
            </li>
        {/each}

    </ul>
</div>

<style lang="scss">
    $base-color: #3890ce;
    $select-color: #7cb8e3;

    .tabs {
        user-select: none;
        margin-bottom: 40px;
        ul {
            display: flex;
            justify-content: center;
            padding: 0;
            list-style: none;
            li {
                margin: 0 16px;
                font-size: 1.25rem;
                color: 555;
                cursor: pointer;
            }
            li:hover {
                color: $select-color;
            }
        }
    }
    .active {
        color: $base-color;
        border-bottom: 2px solid $base-color;
        padding-bottom: 8px;
    }
</style>