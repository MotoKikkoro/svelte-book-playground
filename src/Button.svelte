<script>
    export let label;
    export let disabled = false; // 初期値を追加
</script>

<button {disabled}>
    {label}
</button>