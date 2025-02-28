<!--
Copyright (c) 2023 Contributors to the  Eclipse Foundation.
This program and the accompanying materials are made
available under the terms of the Eclipse Public License 2.0
which is available at https://www.eclipse.org/legal/epl-2.0/
SPDX-License-Identifier: EPL-2.0

Contributors: Smart City Jena

-->
<script setup lang="ts">
import Navbar from "./NavBar.vue";
import { useAppSettingsStore } from "@/stores/AppSettings";

const appSettings = useAppSettingsStore();
const layout = "vertical";

const getLeftWidth = () => {
  return layout === "default" ? "600px" : "400px";
};
</script>

<template>
  <div class="app-layout-container bg grey overflow-hidden">
    <navbar></navbar>
    <div v-if="appSettings.cubeOpened" class="split-container">
      <va-split
        class="split"
        :model-value="0"
        :limits="[
          [getLeftWidth(), 'any'],
          ['500px', 'any'],
        ]"
      >
        <template #start>
          <div class="section-block">
            <slot name="left_container" />
          </div>
        </template>
        <template #end>
          <div class="section-block">
            <slot name="right_container" />
          </div>
        </template>
      </va-split>
    </div>
    <div v-else class="helper">
      <h2>Connect to the cube</h2>
    </div>
    <va-modal v-model="appSettings.loading" no-dismiss>
      <template #content>
        <div class="my-2 mx-4">
          <div class="mb-4">Loading</div>
          <va-progress-circle indeterminate />
        </div>
      </template>
    </va-modal>
  </div>
</template>

<style lang="scss" scoped>
.app-layout-container {
  height: 100%;
  display: flex;
  flex-direction: column;
}

.split-container {
  height: 100%;
  overflow: hidden;
}

.split {
  height: 100%;
  width: 100%;

  & .section-block {
    position: relative;
    height: 100%;
    overflow-x: hidden;
    overflow-y: auto;
    user-select: none;
  }
}

.helper {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
