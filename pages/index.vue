<template>
	<div style="height: 100%">
		<v-row justify="center" align="center" no-gutters style="height: 100%">
			<v-list style="position: fixed; left: 0; top: 40%; width: 25%;" color="transparent">
				<v-list-item-group
					v-model="model"
					mandatory
					color="indigo"
				>
					<v-list-item
						v-for="(section, i) in sections"
						:key="i"
					>
						<v-list-item-content>
							<v-list-item-title v-text="section.text" class="text-center"></v-list-item-title>
						</v-list-item-content>
					</v-list-item>
				</v-list-item-group>
			</v-list>
			<v-col cols="12" sm="9" md="9" offset-sm="3" offset-md="3" class="" style="background: rgba(255, 0, 0, 0.2); height: 100%">

				

			</v-col>
		</v-row>
		<v-row justify="center" align="center" no-gutters style="height: 100%">
			<v-col cols="12" sm="9" md="9" offset-sm="3" offset-md="3" style="background: rgba(255, 0, 255, 0.2); height: 100%">
			</v-col>
		</v-row>
	</div>
</template>

<script>

export default {
	data: () => ({
		sections: [
			{
				text: 'Home',
			},
			{
				text: 'Accounting',
			},
			{
				text: 'HR & Payroll',
			}
		],
		model: 1,
    })
}
</script>

<style>
	.section {
		
	}
</style>