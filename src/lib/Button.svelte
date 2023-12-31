<script>
    export let size = 'small';
    export let shadow = false;
    export let bgColor;
    export let textColor;
    let isLeftHovered;
</script>

<button
    class:size-lg={size === 'large'}
    class:size-sm={size === 'small'}
    style:background-color={bgColor}
    style:color={textColor}
    {...$$restProps}
>
    {#if $$slots.leftContent}
        <div
            class="left-content"
            on:mouseenter={() => (isLeftHovered = true)}
            on:mouseleave={() => (isLeftHovered = false)}
        >
            <slot name="leftContent" {isLeftHovered} />
        </div>
    {/if}
    <slot >Test</slot>
</button>

<style lang="scss">
    button {
        display: flex;
        align-items: center;
        border: none;
        background-color: #ff3e00;
        color: #ffffff;
        padding: 15px 20px;
        font-weight: bold;
        border-radius: 8px;
        cursor: pointer;
        &.size-sm {
            padding: 15px 20px;
        }
        &:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }

        &.size-lg {
            padding: 20px 25px;
            font-size: 20px;
        }
    }
</style>
