<script setup>
    import { Head, Link } from '@inertiajs/vue3';
    import NavLayout from '@/Layouts/NavLayout.vue';
    import CheckCircle from 'vue-material-design-icons/CheckCircle.vue'
    import ThumbUpOutline from 'vue-material-design-icons/ThumbUpOutline.vue'
    import ThumbDownOutline from 'vue-material-design-icons/ThumbDownOutline.vue'
    import RecommendedVideos from '@/Components/RecommendedVideos.vue';

    defineProps({
        video: Object,
        comments: Array,
        recommendedVideos: Array
    })
</script>

<template>

    <Head title="Youtube" />

    <NavLayout>
        <div class="xl:flex">
            <div class="p-3">
                <video @mouseover="show = true" :src="video.video || ''" controls autoplay/>
                <div class="mt-4 text-2xl font-extrabold text-white">{{ video.title }}</div>
                <div class="flex items-center mb-4">
                    <img
                        class="flex items-baseline w-12 h-12 mt-2 rounded-full"
                        :src="`https://picsum.photos/id/${(Math.random() * 100).toFixed(0)}/100` || ''"
                    >
                    <div class="pl-2 mt-1">
                        <div class="flex items-center text-lg font-extrabold text-white">
                            {{ video.user }} <CheckCircle class="pl-2" fillColor="#888888" :size="17"/>
                        </div>
                        <div class="text-sm font-extrabold text-gray-400">{{ video.views }}</div>
                    </div>
                </div>

                <!-- Videos suggested MOBILE VIEW -->
                <div class="w-[500px] p-3 block sm:hidden">
                    <div v-for="vid in recommendedVideos" :key="vid">
                        <Link class="flex mb-3"  :href="route('videos.show', { id: vid.id })">
                            <RecommendedVideos :vid="vid" />
                        </Link>
                    </div>
                </div>
                <!-- Videos suggested MOBILE VIEW End -->

                <div class="bg-[#3F3F3F] rounded-lg w-full p-3 text-white">
                    <div class="text-lg font-extrabold text-white">{{ video.views }}</div>
                    <div class="mb-6 text-sm font-extrabold">
                        Lorem ipsum dolor sit amet consectetur adipisicing elit.
                    </div>
                    <div class="text-sm font-extrabold">
                        Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.
                    </div>
                </div>


                <div class="mt-6">
                    <div class="text-lg font-extrabold text-white">{{ comments.length }} Comments</div>
                    <div v-for="comment in comments" :key="comment">
                        <div class="flex mt-2 mb-4 items-flex">
                            <img
                                class="w-12 h-12 mt-2 rounded-full"
                                :src="`https://picsum.photos/id/${(Math.random() * 100).toFixed(0)}/100` || ''"
                            >
                            <div class="pl-6 mt-1">
                                <div class="flex items-baseline font-extrabold text-white">
                                    <div>{{ comment.user }}</div>
                                    <div class="pl-3 text-gray-400">{{ comment.time }}</div>
                                </div>
                                <div class="text-sm font-extrabold text-gray-200">
                                    {{ comment.text }}
                                </div>
                                <div class="flex items-center mt-4">
                                    <ThumbUpOutline fillColor="#FFFFFF" :size="20" class="pr-2"/>
                                    <div class="pr-10 text-sm font-extrabold text-gray-400">{{ (Math.random() * 100).toFixed(0) }}</div>
                                    <ThumbDownOutline fillColor="#FFFFFF" :size="20"/>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Videos suggested Larger VIEW -->
            <div class="w-[500px] p-3 sm:block hidden">
                <div v-for="vid in recommendedVideos" :key="vid">
                    <Link class="flex mb-3"  :href="route('videos.show', { id: vid.id })">
                        <RecommendedVideos :vid="vid" />
                    </Link>
                </div>
            </div>
            <!-- Videos suggested Larger VIEW End -->
        </div>
    </NavLayout>
</template>
