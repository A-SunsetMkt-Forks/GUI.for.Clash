<script setup lang="ts">
import { useI18n } from 'vue-i18n'

import { StackOptions, TunConfigDefaults } from '@/constant'
import { type ProfileType } from '@/stores'

const fields = defineModel<ProfileType['tunConfig']>({ default: TunConfigDefaults() })

const { t } = useI18n()
</script>

<template>
  <div class="form-item">
    {{ t('kernel.tun.enable') }}
    <Switch v-model="fields.enable" />
  </div>
  <template v-if="fields.enable">
    <div class="form-item">
      {{ t('kernel.tun.stack') }}
      <Radio v-model="fields.stack" :options="StackOptions" />
    </div>
    <div class="form-item">
      {{ t('kernel.tun.auto-route') }}
      <Switch v-model="fields['auto-route']" />
    </div>
    <div
      v-show="fields['auto-route']"
      :class="{ 'flex-start': fields['route-address'].length !== 0 }"
      class="form-item"
    >
      {{ t('kernel.tun.route-address') }}
      <InputList v-model="fields['route-address']" placeholder="0.0.0.0/1 ::/1" />
    </div>
    <div class="form-item">
      {{ t('kernel.tun.auto-detect-interface') }}
      <Switch v-model="fields['auto-detect-interface']" />
    </div>
    <div class="form-item" :class="{ 'flex-start': fields['dns-hijack'].length !== 0 }">
      {{ t('kernel.tun.dns-hijack') }}
      <InputList v-model="fields['dns-hijack']" />
    </div>
    <div class="form-item">
      {{ t('kernel.tun.device') }}
      <Input v-model="fields['device']" editable />
    </div>
    <div class="form-item">
      {{ t('kernel.tun.mtu') }}
      <Input v-model="fields['mtu']" type="number" editable />
    </div>
    <div class="form-item">
      {{ t('kernel.tun.strict-route') }}
      <Switch v-model="fields['strict-route']" />
    </div>
    <div class="form-item">
      {{ t('kernel.tun.endpoint-independent-nat') }}
      <Switch v-model="fields['endpoint-independent-nat']" />
    </div>
  </template>
</template>

<style lang="less" scoped>
.flex-start {
  align-items: flex-start;
}
</style>
