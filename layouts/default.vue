<template>
	<v-app dark>
		<v-navigation-drawer
			v-if="$nuxt.$route.path === '/'"
			v-model="homeDrawer"
			app
			clipped
			color="#ffebd6"
		>
		<v-list-item-group
				v-model="linkCurrent"
				mandatory
				color="#914c06"
			>
			<v-list>
				<v-list-item
					v-for="(link, i) in links"
					:key="i"
				>
					<v-list-item-content>
						<v-list-item-title v-text="link.text" class="text-center" @click="$vuetify.goTo(link.target)"></v-list-item-title>
					</v-list-item-content>
				</v-list-item>
			</v-list>
			</v-list-item-group>
		</v-navigation-drawer>

		<v-app-bar
			fixed
			app
			:height="45"
			color="#5e3206"
			dark
			clipped-left
		>
			<v-app-bar-nav-icon v-if="$nuxt.$route.path === '/'" @click.stop="homeDrawer = !homeDrawer" />
			<v-toolbar-title v-text="title" />
			<v-spacer></v-spacer>
			<v-btn
				icon
				@click.stop="mainDrawer = !mainDrawer"
			>
				<v-icon>mdi-account-circle</v-icon>
			</v-btn>
		</v-app-bar>
		<v-main class="main">
			
			<!-- <v-container> -->
			<nuxt />
			<!-- </v-container> -->
		</v-main>
		
		<v-navigation-drawer
			v-model="mainDrawer"
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
				<v-list-item>
					<v-btn
						color="primary"
						class="mr-4"
						@click="signOut"
					>
						Sign Out
					</v-btn>
				</v-list-item>

				<v-spacer></v-spacer>

				<v-list-item>
					<v-list-item-content>
						<span>&copy; {{ new Date().getFullYear() }}</span>
					</v-list-item-content>
				</v-list-item>
			</v-list>
		</v-navigation-drawer>
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
			mainDrawer: false,
			homeDrawer: true,
			items: [
				{
					icon: 'mdi-apps',
					title: 'Welcome',
					to: '/'
				},
				{
					icon: 'mdi-apps',
					title: 'About',
					to: '/about'
				}
			],
			links: [
				{
					text: 'Home',
					target: '#home-section'
				},
				{
					text: 'Accounting',
					target: '#accounting-section'
				},
				{
					text: 'HR & Payroll',
					target: '#hr-section'
				}
			],
			linkCurrent: 0,
			title: 'Bizzyness'
		}
	},
	methods: {
        signOut: function(err) {
			this.$store.dispatch('auth/signOut')
				.then(() => {
					this.$router.replace({ path: '/login' });
				})
				.catch(err => {
					alert(err.message);
				});
        }
	}
}
</script>

<style>
	.main {
		background-color: #ffebd6;
	}
	.v-slide-group__prev {
		position:					absolute;
		height:						100%;
		left:						0;
		z-index:					1;
	}
	.v-slide-group__next {
		position:					absolute;
		height:						100%;
		right:						0;
		z-index:					1;
	}
</style>