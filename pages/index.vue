<template>
	<div style="height: 100%">
		<v-list style="position: fixed; left: 0; top: 40%; width: 25%;" color="transparent">
			<v-list-item-group
				v-model="linkCurrent"
				mandatory
				color="#914c06"
			>
				<v-list-item
					v-for="(link, i) in links"
					:key="i"
				>
					<v-list-item-content>
						<v-list-item-title v-text="link.text" class="text-center" @click="$vuetify.goTo(link.target)"></v-list-item-title>
					</v-list-item-content>
				</v-list-item>
			</v-list-item-group>
		</v-list>

		<!-- Highlights, Your most recent and relevant news or reports in the organization, it's similar to Twitter Highlights  -->
		<v-row id="home-section" class="page-section" justify="center" align="center" no-gutters>
			<v-col class="content-wrapper d-flex" cols="12" sm="9" md="9" offset-sm="3" offset-md="3">

				<v-sheet
					height="100%"
					max-width="100%"
					color="transparent"
				>
					<v-slide-group
						v-model="mainContentCurrent"
						center-active
						show-arrows
						style="height: 100%;"
					>
						<div
							v-for="(content, i) in mainContent"
							:key="i"
							class="py-md-10"
						>
							<v-slide-item
								v-if="content.padding"
								disabled
							>
								<v-card
									color="transparent"
									elevation="0"
									class="d-flex flex-column mx-4"
									height="100%"
									width="55vh"
								>
								</v-card>
							</v-slide-item>
							<v-slide-item
								v-else
								v-slot="{ toggle }"
							>
								<v-card
									dark
									class="d-flex flex-column mx-4"
									height="100%"
									width="55vh"
									@click="toggle"
								>
									<v-img
										v-if="content.image && content.image !== ''"
										:src="content.image"
										class="white--text align-end"
										gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
										max-height="350"
									>
										<v-card-title v-text="content.title"></v-card-title>
									</v-img>

									<div v-if="content.report" style="width: 100%">
										<v-card-text>
											<v-sheet color="rgba(0, 0, 0, .12)" width="100%">
												<v-sparkline
													:value="content.report"
													color="rgba(255, 255, 255, .7)"
													height="100%"
													padding="24"
													stroke-linecap="round"
													smooth
												>
													<template v-slot:label="item">
														${{ item.value }}
													</template>
												</v-sparkline>
											</v-sheet>
										</v-card-text>
										<v-card-title v-text="content.title"></v-card-title>
									</div>

									<v-card-text v-if="content.text && (content.text !== '')">
										{{ content.text }}
									</v-card-text>

									<v-card-actions>
										<v-spacer></v-spacer>

										<v-btn icon>
											<v-icon>mdi-heart</v-icon>
										</v-btn>

										<v-btn icon>
											<v-icon>mdi-bookmark</v-icon>
										</v-btn>

										<v-btn icon>
											<v-icon>mdi-share-variant</v-icon>
										</v-btn>
									</v-card-actions>
								</v-card>
							</v-slide-item>
						</div>
					</v-slide-group>
				</v-sheet>

				<!-- <v-carousel
					v-model="mainContentCurrent"
					hide-delimiters
					:continuous="false"
					height="100%"
				> -->
					<!-- <v-text class="text-h5" style="position: absolute; top: 2%; left: 8%;">Highlights</v-text> -->
					<!-- <v-carousel-item
						v-for="(content, i) in mainContent"
						:key="i"
					>
						<v-sheet
							class="d-flex py-md-10"
							height="100%"
							tile
							color="transparent"
						>
							<v-card class="d-flex flex-column mx-auto" height="100%" max-width="400px">
								<v-img
									v-if="content.image && content.image !== ''"
									:src="content.image"
									class="white--text align-end"
									gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
									max-height="350"
								>
									<v-card-title v-text="content.title"></v-card-title>
								</v-img>

								<div v-if="content.report" style="width: 100%">
									<v-card-text>
										<v-sheet color="rgba(0, 0, 0, .12)" width="50vh">
											<v-sparkline
												:value="content.report"
												color="rgba(255, 255, 255, .7)"
												height="100%"
												padding="24"
												stroke-linecap="round"
												smooth
											>
												<template v-slot:label="item">
													${{ item.value }}
												</template>
											</v-sparkline>
										</v-sheet>
									</v-card-text>
									<v-card-title v-text="content.title"></v-card-title>
								</div>

								<v-card-text v-if="content.text && (content.text !== '')">
									{{ content.text }}
								</v-card-text>

								<v-card-actions>
									<v-spacer></v-spacer>

									<v-btn icon>
										<v-icon>mdi-heart</v-icon>
									</v-btn>

									<v-btn icon>
										<v-icon>mdi-bookmark</v-icon>
									</v-btn>

									<v-btn icon>
										<v-icon>mdi-share-variant</v-icon>
									</v-btn>
								</v-card-actions>
							</v-card>
						</v-sheet>
					</v-carousel-item>
				</v-carousel> -->

			</v-col>
		</v-row>
		<v-row id="accounting-section" class="page-section" justify="center" align="center" no-gutters>
			<v-col cols="12" sm="9" md="9" offset-sm="3" offset-md="3" class="content-wrapper">
				<v-sheet
					class="d-flex py-md-10"
					height="100%"
					tile
					color="transparent"
				>
					<v-card
						color="#1F7087"
						dark
						class="ma-auto pa-2 d-flex"
					>
						<div class="d-flex flex-no-wrap justify-space-between">
							<div class="d-flex flex-column align-start">
								<v-card-title
									class="headline"
								>
									Accounting
								</v-card-title>

								<v-card-subtitle>Journaling, Invoicing & Transactions</v-card-subtitle>

								<v-card-actions class="d-flex mt-auto">
									<v-btn
										outlined
										rounded
										small
									>
										Go To Accounting
									</v-btn>
								</v-card-actions>
							</div>

							<v-avatar
								class="ma-3"
								size="200"
								tile
							>
								<v-img src="https://cdn.vuetifyjs.com/images/cards/foster.jpg"></v-img>
							</v-avatar>
						</div>
					</v-card>
				</v-sheet>
			</v-col>
		</v-row>
		<v-row id="hr-section" class="page-section" justify="center" align="center" no-gutters>
			<v-col cols="12" sm="9" md="9" offset-sm="3" offset-md="3" class="content-wrapper">
				<v-sheet
					class="d-flex py-md-10"
					height="100%"
					tile
					color="transparent"
				>
					<v-card
						color="#952175"
						dark
						class="ma-auto pa-2 d-flex"
					>
						<div class="d-flex flex-no-wrap justify-space-between">
							<v-avatar
								class="ma-3"
								size="200"
								tile
							>
								<v-img src="https://cdn.vuetifyjs.com/images/cards/foster.jpg"></v-img>
							</v-avatar>

							<div class="d-flex flex-column align-end">
								<v-card-title
									class="headline"
								>
									HR & Payroll
								</v-card-title>

								<v-card-subtitle>Attendance, Payroll & Employees</v-card-subtitle>

								<v-card-actions class="d-flex mt-auto">
									<v-btn
										outlined
										rounded
										small
									>
										Go To HR & Payroll
									</v-btn>
								</v-card-actions>
							</div>
						</div>
					</v-card>
				</v-sheet>
			</v-col>
		</v-row>
	</div>
</template>

<script>

export default {
	data: () => ({
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
		mainContent: [
			{
				padding: true
			},
			{
				title: 'Bizzyness, all your business needs',
				text: 'Bizzyness is a new generation ERP. It has all the business receipes you need in your processes and work flow.',
				background: 'primary',
				image: 'https://cdn.vuetifyjs.com/images/cards/house.jpg'
			},
			{
				title: 'This is Highlights',
				text: 'While you were offline, this is the latest and relevant news and reports that has happened in the organization.',
				background: 'secondary',
				image: 'https://cdn.vuetifyjs.com/images/cards/road.jpg'
			},
			{
				title: 'Accounting Report',
				text: '',
				background: 'yellow darken-2',
				image: '',
				report: [
					423,
					446,
					675,
					510,
					590,
					610,
					760,
				]
			},
			{
				padding: true
			}
		],
		mainContentCurrent: 1
    })
}
</script>

<style scoped>
	.page-section {
		height:						100vh;
	}
	.page-section .content-wrapper {
		height:						100%;
		position:					relative;
	}
</style>