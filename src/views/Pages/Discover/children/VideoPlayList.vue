<script setup>
import { ref, watch, onUpdated } from "vue"
import { Icon } from "@iconify/vue";

const props = defineProps({
  data: {},
});
// console.log(props.data);

const emit = defineEmits(["transmitePlaylistId", "transmiteSongId", "transmiteVideoId"])
const isChecked = (id) => {
  console.log(id);
};
</script>

<template>
  <div class="flex m-auto p-2 justify-between items-center w-[100vw] h-[6vh]">
    <div class="flex justify-center items-center">
      <div class="text-[#707070] text-[14px] font-bold">
        {{ props.data.name }}
      </div>
      <Icon icon="weui:arrow-filled" width="1.2rem" height="1.2rem" style="color: #666666" />
    </div>
    <Icon icon="material-symbols:more-vert" class="text-[1.2rem] mr-1 text-[#707070]" />
  </div>
  <div class="w-[100vw] flex justify-center items-center">
    <van-swipe :width="150" :height="220" :stop-propagation="false" :loop="false" :show-indicators="false">
      <van-swipe-item class="p-2" v-for="(item, index) in props.data.children" :key="item.resourceId">
        <div @click="isChecked(item.resourceId)" class=" h-[100%] flex flex-col justify-around items-center">
          <div
            class="w-[4rem] h-[2rem] absolute flex justify-center items-center top-[10%] left-[50%] z-1 bg-[#5555556c] rounded-[3rem] font-bold text-[#ffffff] text-[0.6rem]">
            <Icon icon="iconoir:play-solid" width="1rem" style="color: #ffffff" />
            <div v-if="props.data.resourceExtInfo[index].playCount > 100000000">
              {{
              `${(
              props.data.resourceExtInfo[index].playCount / 100000000
              ).toFixed(1)}亿`
              }}
            </div>
            <div v-else-if="props.data.resourceExtInfo[index].playCount > 10000">
              {{
              `${(
              props.data.resourceExtInfo[index].playCount / 10000
              ).toFixed(2)}万`
              }}
            </div>
            <div v-else>
              {{ props.data.resourceExtInfo[index].playCount }}
            </div>
          </div>
          <img class="rounded-[20px] w-[10rem] h-[8.8rem]" :src="item.imageUrl" />
          <van-text-ellipsis class="w-[90%] h-[2.2rem] overflow-hidden text-[12px] text-[#583c3c]" :content="item.title"
            rows="2" />
        </div>
      </van-swipe-item>
    </van-swipe>
  </div>
</template>
<style scoped></style>