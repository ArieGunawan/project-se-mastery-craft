<script setup>
import { ref, onMounted } from 'vue';
import { usePage, Link } from '@inertiajs/vue3';
import SideNavItem from '../Components/SideNavItem.vue'
import MenuIcon from 'vue-material-design-icons/Menu.vue';
import MagnifyIcon from 'vue-material-design-icons/Magnify.vue';

let openSideNav = ref(true);
let openSideNavOverlay = ref(false);
let SideNavOverlay = ref(null);
let width = ref(document.documentElement.clientWidth);

onMounted(() => {
    resize()
    SideNavOverlay.value.classList.value = SideNavOverlay.value.classList.value += ' hidden'
    window.addEventListener('resize', () => {
        width.value = document.documentElement.clientWidth;
        resize()
    });
})

const resize = () => {
    if (width.value < 1280 && openSideNav.value){
        openSideNav.value = false
    }
    if (width.value > 1279 && !openSideNav.value){
        openSideNav.value = true
    }
}

const isNavOverlay = () => {
    if(usePage().url === '/') openSideNav.value = !openSideNav.value
    if(usePage().url === '/add-video') openSideNavOverlay.value = !openSideNavOverlay.value
    if(usePage().url === '/delete-video') openSideNavOverlay.value = !openSideNavOverlay.value
    if(width.value < 640) openSideNavOverlay.value = !openSideNavOverlay.value
    if(usePage().url !== '/' && width.value < 640) openSideNavOverlay.value = !openSideNavOverlay.value
    if(usePage().props.video) openSideNavOverlay.value = !openSideNavOverlay.value

}

</script>

<template>
    <div class="relative">
        <div id="TopNav" class="w-[100%] h-[60px] fixed bg-black z-20 flex items-center justify-between">
            <div class="flex items-center">
                <button @click="isNavOverlay()" class="inline-block p-2 ml-3 rounded-full cursor-pointer hover:bg-gray-800">
                    <MenuIcon fillColor="#FFFFFF" :size="26"/>
                </button>
                <div class="mx-2">
                    <Link :href="route('home')" class="flex items-center justify-center mr-10 text-white cursor-pointer">
                        <img width="62" src="/img/masterycraft.png" alt="">
                        Mastery Craft
                    </Link>
                </div>
            </div>

            <div class="w-[600px] md:block hidden">
                <div class="rounded-full flex items-center bg-[#222222]">
                    <input type="text" class="form-control block w-full px-5 py-1.5 text-base font-normal text-gray-200 bg-black placeholder-gray-400 bg-clip-padding border border-solid border-l-gray-700 border-y-gray-700 rounded-l-full transition ease-in-out m-0 border-transparent focus:ring-0" placeholder="Search" />
                    <MagnifyIcon class="mx-6" fillColor="#FFFFFF" :size="23"/>
                </div>
            </div>
            <div>
                <img src="https://yt3.ggpht.com/ytc/AIdro_n-OeK3zlCaTn2VSnwamnggtf_6LPw9yZ7yOULOYBgsenU=s48-c-k-c0x00ffffff-no-rj" class="mx-8 rounded-full" width="35">
            </div>
        </div>

        <div
            v-if="$page.url === '/'"
            id="SideNav"
            class="h-[100%] fixed z-0 bg-black "
            :class="[!openSideNav ? 'w-[70px]' : 'w-[240px]']"
        >
            <ul :class="[!openSideNav ? 'p-2' : 'px-5 pb-2 pt[7px]']" class="mt-[60px] w-full">

                <Link :href="route('home')">
                    <SideNavItem :openSideNav="openSideNav" iconString="Home"/>
                </Link>

                <Link :href="route('addVideo')">
                    <SideNavItem :openSideNav="openSideNav" iconString="Add Video"/>
                </Link>

                <Link :href="route('deleteVideo')">
                    <SideNavItem :openSideNav="openSideNav" iconString="Delete Video"/>
                </Link>
                <div class="border-b border-b-gray-700 my-2.5"></div>
                <SideNavItem :openSideNav="openSideNav" iconString="Subscriptions"/>
                <SideNavItem :openSideNav="openSideNav" iconString="Library"/>
                <SideNavItem :openSideNav="openSideNav" iconString="Liked"/>
                <SideNavItem :openSideNav="openSideNav" iconString="History"/>
                <SideNavItem :openSideNav="openSideNav" iconString="Watch Later"/>
                <div v-if="openSideNav">
                    <div class="border-b border-b-gray-700 my-2.5"/>
                    <div class="text-gray-400 text-[14px] text-extrabold">
                        Copy Right By Kelompok 10
                        <div></div>
                    </div>
                </div>
            </ul>
        </div>

        <div v-if="width > 639">
            <div
            v-if="$page.url === '/'"
            id="SideNav"
            class="h-[100%] fixed z-0 bg-black "
            :class="[!openSideNav ? 'w-[70px]' : 'w-[240px]']"
        >
            <ul :class="[!openSideNav ? 'p-2' : 'px-5 pb-2 pt[7px]']" class="mt-[60px] w-full">
                <Link :href="route('home')">
                        <SideNavItem :openSideNav="openSideNav" iconString="Home"/>
                    </Link>
                    <Link :href="route('addVideo')">
                        <SideNavItem :openSideNav="openSideNav" iconString="Add Video"/>
                    </Link>
                    <Link :href="route('deleteVideo')">
                        <SideNavItem :openSideNav="openSideNav" iconString="Delete Video"/>
                    </Link>
                <div class="border-b border-b-gray-700 my-2.5"></div>
                <SideNavItem :openSideNav="openSideNav" iconString="Subscriptions"/>
                <SideNavItem :openSideNav="openSideNav" iconString="Library"/>
                <SideNavItem :openSideNav="openSideNav" iconString="Liked"/>
                <SideNavItem :openSideNav="openSideNav" iconString="History"/>
                <SideNavItem :openSideNav="openSideNav" iconString="Watch Later"/>
                <div v-if="openSideNav">
                    <div class="border-b border-b-gray-700 my-2.5"/>
                    <div class="text-gray-400 text-[14px] text-extrabold">
                        Copy Right By Kelompok 10
                        <div></div>
                    </div>
                </div>
            </ul>
        </div>
        </div>

        <div
            @click="openSideNavOverlay = false"
            class="fixed z-50 w-full h-screen bg-black bg-opacity-70"
            :class=" openSideNavOverlay ? 'animate__animated animate__fadeIn animate__faster' : 'hidden z-[-1]'"
        />

        <div>
            <div
            id="SideNavOverlay"
            ref="SideNavOverlay"
            class="h-[100%] fixed z-50 bg-black mt-[9px] w-[240px]"
            :class="[
                openSideNavOverlay
                ? 'animate__animated animate__slideInLeft animate__faster'
                : 'animate__animated animate__slideOutLeft animate__faste'
            ]"
        >
        <div class="flex items-center">
                <button @click="isNavOverlay()" class="p-2 ml-3 rounded-full cursor-pointer hover:bg-gray-800">
                    <MenuIcon fillColor="#FFFFFF" :size="26"/>
                </button>
                <div class="mx-2">
                    <Link :href="route('home')" class="flex items-center justify-center mr-10 text-white cursor-pointer">
                        <img width="62" src="/img/masterycraft.png" alt="">
                        Mastery Craft
                    </Link>
                </div>
            </div>
            <ul class="w-full p-2 px-5 py-2 mt-2">
                <Link :href="route('home')">
                    <SideNavItem :openSideNav="true" iconString="Home"/>
                </Link>

                <Link :href="route('addVideo')">
                    <SideNavItem :openSideNav="true" iconString="Add Video"/>
                </Link>

                <Link :href="route('deleteVideo')">
                    <SideNavItem :openSideNav="true" iconString="Delete Video"/>
                </Link>
                <div class="border-b border-b-gray-700 my-2.5"></div>
                <SideNavItem :openSideNav="true" iconString="Subscriptions"/>
                <SideNavItem :openSideNav="true" iconString="Library"/>
                <SideNavItem :openSideNav="true" iconString="Liked"/>
                <SideNavItem :openSideNav="true" iconString="History"/>
                <SideNavItem :openSideNav="true" iconString="Watch Later"/>
                <div v-if="openSideNav">
                    <div class="border-b border-b-gray-700 my-2.5"/>
                    <div class="text-gray-400 text-[14px] text-extrabold">
                        Copy Right By Kelompok 10
                        <div></div>
                    </div>
                </div>
            </ul>
        </div>
        </div>
        <div
            class="w-[100%] h-[calc(100vh-60px)] absolute right-0 top-[60px]"
            :class="{
                'w-[calc(100%-70px)]': !openSideNav,
                'w-[calc(100%-240px)]': openSideNav,
                'w-[100vw] xl:w-[calc(100%-80px)]': $page.url !== '/',
                'w-[100vw]': width < 639
            }"
        >
            <slot />
        </div>
    </div>
</template>

<style>

body {
    background-color: black;
}

</style>
