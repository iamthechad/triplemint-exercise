<script lang="ts">
	import Header from "./Header.svelte";
	import PropertyComponent from "./PropertyComponent.svelte";
	import data from "./data.json";

	let viewData = data.models;
	let photoType = "photo";

	/**
	 * Simple fake data change events. Supports filtering out co-ops and switching between photo and floor plan
	 * @param event
	 */
	function handleUpdateEvent(event) {
		console.log(event);
		const updateType = event.detail.filterType;
		if (updateType === "includeCoop") {
			if (event.detail.value) {
				viewData = data.models;
			} else {
				viewData = data.models.filter(model => model.unit.building.type !== "co-op");
			}
		} else if (updateType === "photoType") {
			photoType = event.detail.value;
		}
	}
</script>

<main>
	<Header on:updateEvent={handleUpdateEvent}/>
	<div class="property-container">
		{#each viewData as property (property.id)}
			<PropertyComponent {property} {photoType}/>
		{/each}
	</div>
</main>

<style type="text/scss">
	main {
	}

	.property-container {
		display: grid;
		grid-auto-rows: 360px;
		grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
		grid-gap: 10px;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
