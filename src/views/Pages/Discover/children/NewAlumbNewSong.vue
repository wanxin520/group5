<script setup>
import { ref } from 'vue'
import { Icon } from '@iconify/vue';
import { useRoute, useRouter } from 'vue-router';
const route = useRoute()
const router = useRouter()
const props = defineProps({
    data: {},
})
// setTimeout(() => {
//     console.log(props.data.creatives)
// }, 1000)

const emit = defineEmits(["transmitePlaylistId", "transmiteSongId", "transmiteVideoId"])


const getResourceId = (resourceId) => {
    // console.log(resourceId)
    emit("transmiteSongId",resourceId)
}

</script>

<template>
    <div>
        <div class="flex m-auto p-2 justify-between items-center w-[100vw] h-[6vh] bg-[#ffffff]">
            <div class="flex justify-center items-center">
                <div class="text-[#707070] text-[14px] font-bold">{{ props.data.name }}</div>
                <Icon icon="weui:arrow-filled" width="1.2rem" height="1.2rem" style="color: #666666" />
            </div>
            <Icon icon="material-symbols:more-vert" class="text-[1.2rem] mr-1 text-[#707070]" />
        </div>
        <div class="w-[100vw] flex justify-center items-center bg-[#ffffff]">
            <van-swipe :width="350" :height="230" :stop-propagation="false" :loop="false" loop="false"
                :show-indicators="false">
                <van-swipe-item class="p-2" v-for="(item, index) in props.data.creatives" :key="item.id">
                    <div class="h-[1rem] m-1 flex justify-start items-center text-[#828282] text-[12px] font-extrabold">
                        {{ item.uiElement.mainTitle.title }}</div>
                    <div class="flex flex-col items-center">
                        <van-swipe :width="305" :height="65" :loop="false" :show-indicators="false" vertical>
                            <van-swipe-item @click="getResourceId(inItem.resourceExtInfo.songData.id)"
                                v-for="inItem in props.data.creatives[index].resources">
                                <div class="h-[100%] flex justify-center items-start">
                                    <div class="h-[100%] flex justify-center items-center">
                                        <img class="rounded-[20px] w-[4rem] p-1" :src="inItem.uiElement.image.imageUrl"
                                            alt="">
                                    </div>
                                    <div class=" w-[80%] h-[100%] p-3 flex flex-col justify-center items-start">
                                        <div
                                            class=" w-[100%] flex justify-start items-center text-[#4d4c4c] text-[12px] font-bold">
                                            {{ inItem.uiElement.mainTitle.title }}
                                        </div>
                                        <div class=" flex p-1 justify-start items-center">
                                            <div v-if="inItem.uiElement.subTitle.title"
                                                class=" h-[1rem] flex justify-start p-1 items-center rounded-[6px] bg-[#fff1f1] text-[#ff5c5c] text-[8px]">
                                                <span>{{ inItem.uiElement.subTitle.title }}</span>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="h-[100%] flex justify-center items-center">
                                        <Icon class="text-[#acacac]" icon="typcn:media-play" width="1.4rem" />
                                    </div>
                                </div>
                            </van-swipe-item>
                        </van-swipe>
                    </div>
                </van-swipe-item>
            </van-swipe>
        </div>
    </div>
</template>
<style scoped></style>