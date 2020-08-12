<script lang="ts">
    import HeaderSection from "./HeaderSection.svelte";

    // Ideally, all of this message handling behavior would be in the App component, but I couldn't
    // quickly determine how to make the HeaderSection component emit messages from the content in its slot
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();

    let photoType = "photo";
    let includeCoop = true;

    function dispatchMessage(name: string, value) {
        dispatch("updateEvent", {
            filterType: name,
            value
        });
    }

    $: dispatchMessage("photoType", photoType);
    $: dispatchMessage("includeCoop", includeCoop);
</script>

<div class="header">
    <HeaderSection>
        <label>
            <input type=radio bind:group={photoType} value="photo">
            Photo
        </label>

        <label>
            <input type=radio bind:group={photoType} value="floor">
            Floor Plan
        </label>
    </HeaderSection>
    <HeaderSection>
        <label>
            <input type=checkbox bind:checked={includeCoop}>
            Include Co-ops
        </label>
    </HeaderSection>
</div>

<style type="text/scss">
    @import "./_globals";

    .header {
        border: thin solid $border-color;
        margin-bottom: 5px;
        display: flex;

        label {
            display: inline;

            &:not(:last-child) {
                margin-right: 5px;
            }
        }
    }
</style>
