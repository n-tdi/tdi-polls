<script>
    export let type = 'primary';
    export let flat = false;
    export let inverse = false;
</script>

<button class={type} on:click class:flat={flat} class:inverse={inverse}>
    <slot></slot>
</button>

<style lang="scss">
    button {
        border: 1px solid #ccc;
        cursor: pointer;
        border-radius: 6px;
        padding: 8px 12px;
        font-size: 1.1rem;
        font-weight: 300;
        box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
        &:active {
            outline: none;
            border: 1px solid #3890ce;
            top: -1px;
        }
    }

    .primary {
        background: #3890ce;
        color: #fff;
    }
    .secondary {
        background: #f5f5f5;
        color: #555;
    }
    .red {
        background: #d94444;
        color: rgb(255, 255, 255);
    }

    .flat {
        box-shadow: none;
        &:active {
            outline: none;
            border: 1px solid #3890ce;
        }
    }

    .inverse {
        background: rgb(90, 90, 90);
        color: #fff;
    }
</style>