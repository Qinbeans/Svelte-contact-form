<script lang="ts">
    import "$lib/styles/app.css";
    // Your selected Skeleton theme:
    import '@skeletonlabs/skeleton/themes/theme-skeleton.css';

    // This contains the bulk of Skeletons required styles:
    // NOTE: this will be renamed skeleton.css in the v2.x release.
    import '@skeletonlabs/skeleton/styles/skeleton.css';
                            
</script>

<main class="w-screen h-screen grid place-content-center bg-slate-700">
    <slot></slot>
</main>