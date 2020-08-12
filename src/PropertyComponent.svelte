<script lang="ts">
    export let property;
    export let photoType: string;

    /**
     * Create a string that represents the neighborhood, like "PARK SLOPE, BROOKLYN"
     * @returns {string}
     */
    function buildNeighborhood(): string {
        const addressCopy = [...property.unit.building.region.address_parts];
        addressCopy.pop();
        return addressCopy.join(", ");
    }

    /**
     * Simple formatter to turn the price into a US dollar formatted value with commas
     * @returns {string}
     */
    function formatPrice(): string {
        const converted = parseInt(property.price, 10);
        if (isNaN(converted)) {
            return "";
        }

        return `\$${converted.toLocaleString("en-US")}`
    }

    /**
     * Build a summary string of the rooms/square footage/type
     * @returns {string}
     */
    function buildRoomsSummary(): string {
        const roomSummaryList: string[] = [];
        roomSummaryList.push(`${property.unit.bedrooms} bd`);
        roomSummaryList.push(`${property.unit.bathrooms} ba`);
        if (property.unit.surface) {
            roomSummaryList.push(`${property.unit.surface} sf`);
        }
        roomSummaryList.push(property.unit.building.type);
        return roomSummaryList.join(", ");
    }

    /**
     * Build the image source for the selected photo type. If no floor plan entry exists, falls back to the primary photo
     * @param photoType
     * @returns {string}
     */
    function buildPhotoSource(photoType): string {
        let imageKey = property.unit.dyn_images[0].key;
        let imageExtension = property.unit.dyn_images[0].extension;
        if (photoType === "floor" && property.unit.dyn_floorplans && property.unit.dyn_floorplans.length) {
            imageKey = property.unit.dyn_floorplans[0].key;
            imageExtension = property.unit.dyn_floorplans[0].extension;
        }
        // URL backward engineered from the Triplemint site
        return `https://dyn-images.triplemint.com/production/images/unit/${property.unit.id}/x486/${imageKey}.${imageExtension}`;
    }
</script>

<div class="property-card">
    <div class="property-photo-container">
        <img src={buildPhotoSource(photoType)} alt="Nope" class="property-photo">
    </div>
    <div class="property-detail-container">
        <div class="property-detail">
            <div class="property-address">
                <div class="property-street">{property.address}</div>
                <div class="property-neighborhood">{buildNeighborhood()}</div>
            </div>
            <div class="property-price">{formatPrice()}</div>
            <div class="property-rooms">{buildRoomsSummary()}</div>
        </div>
    </div>
</div>

<style type="text/scss">
    @import "./_globals";

    .property-card {
        border: thin solid $border-color;

        .property-photo-container {
            width: 100%;
            height: 70%;
            background-color: aliceblue;

            .property-photo {
                width: inherit;
                height: 100%
            }
        }

        .property-detail-container {
            padding: 5px;
            text-transform: uppercase;
            color: #404040;
            height: calc(30% - 10px);
            display: flex;
            flex-direction: column;
            justify-content: center;

            .property-detail {

                .property-address {
                    .property-street {
                        font-size: larger;
                    }

                    .property-neighborhood {
                        font-size: x-small;
                    }
                }

                .property-price {
                    margin-top: 5px;
                    font-size: smaller;
                }

                .property-rooms {
                    font-size: x-small;
                }
            }
        }
    }
</style>
