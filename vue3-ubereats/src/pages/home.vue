<template>
	<div class="home">
		<RestaurantRow />
	</div>
</template>

<script>
//IMPORTS
import BDD from "../BDD.js";

//COMPONENETS
import RestaurantRow from "../components/RestaurantRow.vue";
export default {
	name: "Home",
	components: {
		RestaurantRow,
	},
	setup() {
		class Restaurant {
			constructor(name, note, image, drive_time) {
				this.name = name;
				this.note = note;
				this.image = image;
				this.drive_time = drive_time;
			}
		}
		let dataRestaurant = [];

		const makeDataRestaurant = () => {
			let three_restaurant = [];

			for (const restaurant of BDD) {
				const new_restaurant = new Restaurant(
					restaurant.name,
					restaurant.note,
					restaurant.image,
					restaurant.drive_time
				);

				if (three_restaurant.length === 2) {
					three_restaurant.push(new_restaurant);
					dataRestaurant.push(three_restaurant);
					three_restaurant = [];
				} else {
					three_restaurant.push(new_restaurant);
				}
			}
			console.log(dataRestaurant);
		};

		makeDataRestaurant();
	},
};
</script>

<style></style>
