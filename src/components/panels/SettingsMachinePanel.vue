<template>
	<v-card outlined>
		<v-card-title class="pb-0">
			{{ $t('panel.settingsMachine.caption') }}
		</v-card-title>

		<v-card-text>
			<v-row>
				<v-col cols="12" lg="6">
					<v-text-field v-model.number="babystepAmount" type="number" step="any" min="0.001" :label="$t('panel.settingsMachine.babystepAmount', ['mm'])" hide-details></v-text-field>
				</v-col>
				<v-col cols="12" lg="6">
					<v-text-field v-model.number="moveFeedrate" type="number" step="any" min="0.001" :label="$t('panel.settingsMachine.moveFeedrate', ['mm/min'])" hide-details></v-text-field>
				</v-col>
			</v-row>
		</v-card-text>
	</v-card>
</template>

<script>
'use strict'

import { mapState, mapMutations } from 'vuex'

export default {
	computed: {
		...mapState('machine', ['settings']),
		...mapState('machine/model', ['boards']),
		...mapState(['isLocal']),
		babystepAmount: {
			get() { return this.settings.babystepAmount; },
			set(value) { if (this.isNumber(value) && value > 0) { this.update({ babystepAmount: value }); } }
		},
		moveFeedrate: {
			get() { return this.settings.moveFeedrate; },
			set(value) { if (this.isNumber(value) && value > 0) { this.update({ moveFeedrate: value }); } }
		}
	},
	methods: mapMutations('machine/settings', ['update'])
}
</script>
