<template>
    <div class="mb-2 titleWords text-2xl">Your MILEZ </div>
    <div class="mb-2 words">Milez accrued: {{ reward.accruedReward/1000000 }}</div>
    <div class="mb-2 words">Milez paid: {{ reward.paidOutReward/1000000 }}</div>
    <div class="mb-2 words">
        Last updated: {{ parseDate(reward.fixedRate.lastUpdatedTs) }}
    </div>
    <div class="mb-2 words" v-if="gems>19">Accrual Rate: {{ rarities*1.25 }} MILEZ per Day</div>
    <div class="mb-2 words" v-else-if="gems>9">Accrual Rate: {{ rarities*1.2 }} MILEZ per Day</div>
    <div class="mb-2 words" v-else-if="gems>4">Accrual Rate: {{ rarities*1.1 }} MILEZ per Day</div>
    <div class="mb-2 words" v-else-if="gems>2">Accrual Rate: {{ rarities*1.05 }} MILEZ per Day</div>
    <div class="mb-2 words" v-else>Accrual Rate: {{ rarities }} MILEZ per Day</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import FixedScheduleDisplay from '@/components/gem-farm/FixedScheduleDisplay.vue';
import { parseDate } from '@/common/util';
import numeral from 'numeral';

export default defineComponent({
  components: { FixedScheduleDisplay },
  props: {
    reward: Object,
    farmReward: Object,
    title: String,
    rarities: Object,
    gems: Object
  },
  setup() {
    const parseRewardType = (reward: any): string => {
      //returns "variable" or "fixed"
      return Object.keys(reward.rewardType)[0];
    };

    return {
      parseRewardType,
      parseDate,
      numeral,
    };
  },
});
</script>

<style scoped></style>
