<script>
    let array=['Svelte', 'React', 'Vue', 'Angular'];
</script>

{#each array as e}
    <slot item = {e}>
    </slot>
{/each}