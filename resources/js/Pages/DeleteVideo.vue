<script setup>
    import { Head, Link } from '@inertiajs/vue3';
    import NavLayout from '@/Layouts/NavLayout.vue';


    defineProps ({ videos: Array })
</script>

<template>
    <Head title="Mastery Craft" />
    <NavLayout>
        <div class="max-w-2xl p-4 mx-auto">
            <table class="min-w-full">
                <thead class="border-b">
                    <tr class="flex justify-between text-white">
                        <th scope="col" class="px-6 py-4 text-sm font-medium text-left">Videos</th>
                        <th scope="col" class="px-6 py-4 text-sm font-medium text-left">Option</th>
                    </tr>
                </thead>
                <tbody>
                    <div v-for="video in videos" :key="video">
                        <tr class="flex justify-between border-b">
                        <td class="w-7/12 px-6 py-4 text-sm font-medium text-gray-900">
                            <video width="320" :src="video.video || ''" type="video/mp4" controls ></video>
                        </td>
                        <td class="relative w-5/12 px-6 py-4 text-sm font-medium text-gray-900">
                            <div class="mb-4 font-extrabold text-white">
                                {{ video.title }}
                            </div>
                            <div class="w-full">
                                <Link
                                        as="button"
                                        method="delete"
                                        :href="route('videos.destroy', { id: video.id })"
                                    class="absolute float-right px-1 py-1 text-xs font-bold text-white bg-red-600 rounded cursor-pointer bottom-4 right-4 hover:bg-red-700"
                                >
                                Delete
                                </Link>
                            </div>
                        </td>
                    </tr>
                    </div>
                </tbody>
            </table>
        </div>
    </NavLayout>

</template>
