<template>
	<v-app dark>
		<v-navigation-drawer
			v-model="drawer"
			fixed
			temporary
			right
		>
			<v-list>
				<v-list-item
					v-for="(item, i) in items"
					:key="i"
					:to="item.to"
					router
					exact
				>
				<v-list-item-action>
					<v-icon>{{ item.icon }}</v-icon>
				</v-list-item-action>
				<v-list-item-content>
					<v-list-item-title v-text="item.title" />
				</v-list-item-content>
				</v-list-item>
			</v-list>

			<span>&copy; {{ new Date().getFullYear() }}</span>
		</v-navigation-drawer>

		<v-app-bar
			fixed
			app
			:height="45"
			color="#5e3206"
			dark
		>
			<v-app-bar-nav-icon />
			<v-spacer></v-spacer>
			<v-btn
				icon
				@click.stop="drawer = !drawer"
			>
				<v-icon>mdi-account-circle</v-icon>
			</v-btn>
		</v-app-bar>
		<v-main class="main">
			<nuxt />
		</v-main>
		<!-- <v-footer
			app
		>
			<span>&copy; {{ new Date().getFullYear() }}</span>
		</v-footer> -->
	</v-app>
</template>

<script>
export default {
  data () {
    return {
      drawer: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        }
      ],
      title: 'Vuetify.js'
    }
  }
}
</script>

<style>
	.main {
		background-color: #ffebd6;
	}
</style>