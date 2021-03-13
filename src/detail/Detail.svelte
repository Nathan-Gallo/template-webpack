<script>
    import { onMount } from 'svelte';

    import { httpGet } from '../common/api';

    export let id;

    let book = {}
    onMount(async () => {
        const { data } = await httpGet('/' + id)
        book = data
    });
</script>

<div>Detail Page - {book.title}</div>