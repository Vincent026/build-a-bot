<template>
  <div>
    <div class="top-row">
      <!-- <div class="top part">
        <img :src="availableParts.heads[selectedHeadIndex].imageUrl" alt="head" />
        <button @click="prevHead()" class="prev-selector">&#9668;</button>
        <button @click="nextHead()" class="next-selector">&#9658;</button>
      </div> -->
    </div>
    <div class="middle-row">
      <!-- <div class="left part">
        <img :src="availableParts.arms[0].imageUrl" alt="left arm" />
        <button @click="prevLeftArm()" class="prev-selector">&#9651;</button>
        <button @click="nextLeftArm()" class="next-selector">&#9661;</button>
      </div> -->
      <div class="center part">
        <img :src="availableParts.torsos[0].imageUrl" alt="torso" />
        <button class="prev-selector">&#9668;</button>
        <button class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img -bind:src="availableParts.arms[0].imageUrl" alt="right arm" />
        <button class="prev-selector">&#9651;</button>
        <button class="next-selector">&#9661;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img v-bind:src="availableParts.bases[0].imageUrl" alt="base" />
        <button class="prev-selector">&#9668;</button>
        <button class="next-selector">&#9658;</button>
      </div>
    </div>
  </div>
</template>

<script>
import parts from '../data/parts';

function getNextValidIndex(index, length) {
  const incrementedIndex = index + 1;
  return incrementedIndex > length - 1 ? 0 : incrementedIndex;
}

function getPreviousValidIndex(index, length) {
  const incrementedIndex = index - 1;
  return incrementedIndex < 0 ? length - 1 : incrementedIndex;
}

export default {
  name: 'RobotBuilder',
  data() {
    return {
      availableParts: parts,
      selectedHeadIndex: 0,
      selectedArmIndex: 0,
    };
  },
  methods:
  {
    prevHead() {
      this.selectedHeadIndex = getPreviousValidIndex(
        this.selectedHeadIndex,
        this.availableParts.heads.length,
      );
    },
    nextHead() {
      this.selectedHeadIndex = getNextValidIndex(
        this.selectedHeadIndex,
        this.availableParts.heads.length,
      );
    },
    prevLeftArm() {
      this.selectedArmIndex = getPreviousValidIndex(
        this.selectedArmIndex,
        this.availableParts.arms.length,
      );
    },
    nextLeftArm() {
      this.selectedArmIndex = getNextValidIndex(
        this.selectedArmIndex,
        this.availableParts.arms.length,
      );
    },
  },
};

</script>

<style>
.part {
  position: relative;
  width: 200px;
  height: 200px;
  border: 3px solid #aaa;
}

.part img {
  width: 200px;
}

.top-row {
  display: flex;
  justify-content: space-around;
}

.middle-row {
  display: flex;
  justify-content: center;
}

.bottom-row {
  display: flex;
  justify-content: space-around;
  border-top: none;
}

.top {
  border-bottom: none;
}

.left {
  border-right: none;
}

.right {
  border-left: none;
}

.left img {
  transform: rotate(-90deg);
}

.right img {
  transform: rotate(90deg);
}

.bottom {
  border-top: none;
}

.prev-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 206px;
}

.next-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 206px;
}

.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
}

.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 179px;
  height: 25px;
}

.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 179px;
  height: 25px;
}

.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 179px;
  height: 25px;
}

.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 179px;
  height: 25px;
}

.right .next-selector {
  right: -3px;
}
</style>
