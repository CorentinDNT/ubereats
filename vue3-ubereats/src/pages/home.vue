<template>
	<div class="home">
		<div class="header">
			<img
				src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/ee037401cb5d31b23cf780808ee4ec1f.svg"
				alt=""
			/>
			<div class="wrapper--input">
				<input
					placeholder="de quoi avez-vous envie ?"
					type="text"
					v-model="search_restaurant"
					name=""
					id=""
				/>
				<div class="search">
					<div
						v-for="(restaurant, i) in test_array"
						:key="i"
						class="container--restaurant--search"
					>
						<div class="wrapper--img">
							<img :src="restaurant.image" alt="" />
						</div>
						<p>{{ restaurant.name }}</p>
					</div>
				</div>
			</div>
		</div>
		<div class="banniere"></div>
		<RestaurantRow
			v-for="(data, i) in dataRestaurant"
			:key="i"
			:three_restaurant="data"
		/>
	</div>
</template>

<script>
//IMPORTS
import BDD from "../BDD.js";
import { onMounted, ref, watch } from "vue";
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
		let dataRestaurant = ref([]);
		let allRestaurant = [];

		const makeDataRestaurant = () => {
			let three_restaurant = [];

			for (const restaurant of BDD) {
				const new_restaurant = new Restaurant(
					restaurant.name,
					restaurant.note,
					restaurant.image,
					restaurant.drive_time
				);

				allRestaurant.push(new_restaurant);

				if (three_restaurant.length === 2) {
					three_restaurant.push(new_restaurant);
					dataRestaurant.value.push(three_restaurant);
					three_restaurant = [];
				} else {
					three_restaurant.push(new_restaurant);
				}
			}
			console.log(dataRestaurant);
		};
		//SEARCH RESTAURANT
		let search_restaurant = ref("");
		let test_array = ref([]);

		watch(search_restaurant, (newValue) => {
			const regex = RegExp(newValue.toLowerCase());

			const new_test_array = allRestaurant.filter((restaurant) =>
				regex.test(restaurant.name.toLowerCase())
			);

			newValue == 0
				? (test_array.value = [])
				: (test_array.value = new_test_array);
		});
		//
		onMounted(makeDataRestaurant);

		//RETURN
		return {
			dataRestaurant,
			search_restaurant,
			test_array,
		};
	},
};
</script>

<style lang="scss">
.header {
	display: flex;
	align-items: center;
	justify-content: space-between;
	height: 120px;
	width: 100%;
	img {
		width: 200px;
	}
	.wrapper--input {
		position: relative;
		input {
			background-color: #f6f6f6;
			border: none;
			height: 60px;
			width: 400px;
			outline: none;
			padding-left: 20px;
		}
		.search {
			position: absolute;
			top: 100%;
			width: 100%;
			background: #fff;
			.container--restaurant--search {
				display: flex;
				align-items: center;
				padding: 10px;
				cursor: pointer;
				&:hover {
					background-color: #f6f6f6;
				}
				.wrapper--img {
					height: 60px;
					width: 60px;
					margin-right: 25px;
					border-radius: 50%;
					overflow: hidden;
					img {
						height: 100%;
						width: auto;
					}
				}
			}
		}
	}
}
.banniere {
	height: 200px;
	width: 100%;
	background-image: url("https://www.ubereats.com/restaurant/_static/7b308f7cbbf8e335ceda0447a8bd7c63.png");
	background-size: cover;
	background-position: center center;
}
</style>
