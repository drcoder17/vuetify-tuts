<template>
	<v-app>
		<v-navigation-drawer app v-model="drawer">
			<v-list-item>
				<v-list-item-content>
					<v-list-item-title class="text-h6">
						My todo
					</v-list-item-title>
					<v-list-item-subtitle>
						supported by Vuetify
					</v-list-item-subtitle>
				</v-list-item-content>
			</v-list-item>
			<v-divider></v-divider>
			<v-list nav>
				<v-list-item
					v-for="item in items"
					:key="item.title"
					:to="item.to"
					link
				>
					<v-list-item-icon>
						<v-icon>{{ item.icon }}</v-icon>
					</v-list-item-icon>

					<v-list-item-content>
						<v-list-item-title>{{ item.title }}</v-list-item-title>
					</v-list-item-content>
				</v-list-item>
			</v-list>
		</v-navigation-drawer>
		<v-app-bar app color="primary" dark prominent src="./assets/bg.jpg">
			<template v-slot:img="{ props }">
				<v-img
					v-bind="props"
					gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
				>
				</v-img>
			</template>
			<v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
			<v-app-bar-title>Super Todo App</v-app-bar-title>
			<v-spacer></v-spacer>
			<v-btn icon>
				<v-icon>mdi-dots-vertical</v-icon>
			</v-btn>
		</v-app-bar>
		<v-main>
			<v-container>
				<router-view></router-view>
			</v-container>
		</v-main>
	</v-app>
</template>

<script>
export default {
	name: 'Home',
	data() {
		return {
			drawer: false,
			items: [
				{ title: 'Todos', icon: 'mdi-format-list-checks', to: '/' },
				{ title: 'About', icon: 'mdi-pencil', to: '/about' },
			],
		};
	},
};
</script>
