<script setup>
import { Head, Link, useForm, usePage } from '@inertiajs/vue3';
//import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import AppLayout from '@/Layouts/AppLayout.vue';
import DangerButton from '@/Components/DangerButton.vue';
import PrimaryLink from '@/Components/PrimaryLink.vue';
import Pagination from '@/Components/Pagination.vue';
import TextInput from '@/Components/TextInput.vue';
import Dropdown from '@/Components/Dropdown.vue';

import SearchBarSideBar from '@/Components/SearchBarSideBar.vue';
import Calendar from '@/Components/Calendar.vue';
import RecentJobs from '@/Components/RecentJobs.vue';
import JobsLastSevenDays from '@/Components/JobsLastSevenDays.vue';
import UpcomingJobs from '@/Components/UpcomingJobs.vue';

const props = defineProps({
    liquijobs : Object,
    job_assets: Object,
    filters : Object,
    message : String
});

const liquijobsCreate = '/liquijobs/create';

const liquiassetsurl = "/liquiassets/create?jobid=" + props.liquijobs.id;

// import { useRoute } from 'vue-router';

// const route = useRoute()
// console.log(route.query)

// const filters = {
//     filter: props.filters.filter,
// }
// const form = useForm(filters);

const deleteTrade = (id) => {
    if (confirm("Are you sure you want to move this to trash")) {
	   form.delete(route('liquijobs.destroy',{id:id}), {
		  preserveScroll: true,
	   });
    }
};
</script>

<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">
                Dashboard
            </h2>
        </template>

        <div class="py-2">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-xl sm:rounded-lg">
                    <div>

				        <div class="grid gap-6 lg:grid-cols-3 md:grid-cols-1 lg:gap-8">
				            
				            <!-- LEFT PART -->
				            <!-- Container for Left Sidebar (search and quick add job) -->
				            <div id="left-side" class="mx-auto flex flex-col items-start gap-6 overflow-hidden rounded-lg bg-white p-6 shadow-[0px_14px_34px_0px_rgba(0,0,0,0.08)] ring-1 ring-white/[0.05] transition duration-300 hover:text-black/70 hover:ring-black/20 focus:outline-none focus-visible:ring-[#FF2D20] md:row-span-3 lg:p-10 lg:pb-10 dark:bg-zinc-900 dark:ring-zinc-800 dark:hover:text-white/70 dark:hover:ring-zinc-700 dark:focus-visible:ring-[#FF2D20]" style="padding-left: 1em; padding-right: 1.5em;">
				                
				                <!-- AVATAR -->
				                <div class="mx-auto relative flex items-center gap-6 lg:items-end">
				                    <div class="relative flex items-center gap-6 lg:items-end">
				                        <img id="avatarButton" type="button" data-dropdown-toggle="userDropdown" data-dropdown-placement="bottom-start" class="max-w-2xl max-h-2xl rounded-full cursor-pointer" src="https://www.gravatar.com/avatar/2c7d99fe281ecd3bcd65ab915bac6dd5?s=250" alt="User dropdown">
				                    </div>

				                    <!-- <div class="relative flex items-center gap-6 lg:items-end">
				                        <h1>My Account</h1>
				                    </div> -->
				                    <!-- Dropdown menu -->
				                    <div id="userDropdown" class="z-10 hidden bg-white divide-y divide-gray-100 rounded-lg shadow-sm w-44 dark:bg-gray-700 dark:divide-gray-600">
				                        <div class="px-4 py-3 text-sm text-gray-900 dark:text-white">
				                          <div>Chi Rilo</div>
				                          <div class="font-medium truncate">name@flowbite.com</div>
				                        </div>
				                        <ul class="py-2 text-sm text-gray-700 dark:text-gray-200" aria-labelledby="avatarButton">
				                          <li>
				                            <a href="#" class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Dashboard</a>
				                          </li>
				                          <li>
				                            <a href="#" class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Settings</a>
				                          </li>
				                          <li>
				                            <a href="#" class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Earnings</a>
				                          </li>
				                        </ul>
				                        <div class="py-1">
				                          <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:hover:bg-gray-600 dark:text-gray-200 dark:hover:text-white">Sign out</a>
				                        </div>
				                    </div>
				                </div>
				                <!-- END OF AVATAR -->
				                <!-- MY ACCOUNT -->
				                <div class="mx-auto relative flex items-center gap-6 lg:items-end">
				                
				                    <!-- <div class="relative flex items-center gap-6 lg:items-end">
				                        <h1>MY ACCOUNT 	&dArr;</h1>
				                    </div> -->
				                    <Dropdown align="right" width="48">
	                                    <template #trigger>
	                                        <button v-if="$page.props.jetstream.managesProfilePhotos" class="flex text-sm border-2 border-transparent rounded-full focus:outline-none focus:border-gray-300 transition">
	                                            <img class="size-8 rounded-full object-cover" :src="$page.props.auth.user.profile_photo_url" :alt="$page.props.auth.user.name">
	                                        </button>

	                                        <span v-else class="inline-flex rounded-md">
	                                            <button type="button" class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md text-gray-500 dark:text-gray-400 bg-white dark:bg-gray-800 hover:text-gray-700 dark:hover:text-gray-300 focus:outline-none focus:bg-gray-50 dark:focus:bg-gray-700 active:bg-gray-50 dark:active:bg-gray-700 transition ease-in-out duration-150">
	                                                {{ $page.props.auth.user.name }}

	                                                <svg class="ms-2 -me-0.5 size-4" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
	                                                    <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
	                                                </svg>
	                                            </button>
	                                        </span>
	                                    </template>

	                                    <template #content>
	                                        <!-- Account Management -->
	                                        <div class="block px-4 py-2 text-xs text-gray-400">
	                                            Manage Account
	                                        </div>

	                                        <DropdownLink :href="route('profile.show')">
	                                            Profile
	                                        </DropdownLink>

	                                        <!-- <DropdownLink v-if="$page.props.jetstream.hasApiFeatures" :href="route('api-tokens.index')">
	                                            API Tokens
	                                        </DropdownLink> -->

	                                        <div class="border-t border-gray-200 dark:border-gray-600" />

	                                        <!-- Authentication -->
	                                        <form @submit.prevent="logout">
	                                            <DropdownLink as="button">
	                                                Log Out
	                                            </DropdownLink>
	                                        </form>
	                                    </template>
	                                </Dropdown>
				                    
				                </div>
				                <!-- END OF: MY ACCOUNT -->

				                

				                <!-- <div id="screenshot-container" class="relative flex w-full flex-1 items-stretch">
				                    <input type="search" name="search" placeholder="Search anything" />
				                </div> -->

				                <SearchBarSideBar/>

				                
				                <br/>


				                 <h2 class="block w-full text-center">FILTER JOBS BY</h2>
				                 <select class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500">
				                     <option value="state">State</option>
				                     <option value="building">Building</option>
				                 </select>
				                 <a href="/liquijobs" class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full" style="display: inline-block; width: 100% !important; text-align: center;"> GO <svg style="display: inline; float: inline-end;" class="size-6 shrink-0 stroke-[#FFFFFF]" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M4.5 12h15m0 0l-6.75-6.75M19.5 12l-6.75 6.75"/></svg> </a>

				                 <h2>QUICK ADD NEW JOB</h2>
				                <div class="relative flex items-center gap-6 lg:items-end">
				                    <div id="docs-card-content" class="flex items-start gap-6 lg:flex-col">
				                        <form class="w-full">
				                             <div class="flex flex-wrap -mx-3 mb-6">
				                                <div class="w-full py-1 px-3">
				                                    <label class="hidden block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-first-name">
				                                    Job Co Name
				                                    </label>
				                                    <input class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" placeholder="Job Co Name">
				                                    <p class="hidden text-red-500 text-xs italic">Please fill out this field.</p>
				                                </div>
				                                <div class="w-full py-1 px-3">
				                                    <label class="hidden block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-first-name">
				                                    Address
				                                    </label>
				                                    <input class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" placeholder="Address">
				                                    <p class="hidden text-red-500 text-xs italic">Please fill out this field.</p>
				                                </div>
				                                <div class="w-full py-1 px-3">
				                                    <label class="hidden block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-first-name">
				                                    Contact Name
				                                    </label>
				                                    <input class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" placeholder="Contact Name">
				                                    <p class="hidden text-red-500 text-xs italic">Please fill out this field.</p>
				                                </div>
				                                <div class="w-full py-1 px-3">
				                                    <label class="hidden block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-first-name">
				                                    Email
				                                    </label>
				                                    <input class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" placeholder="Email">
				                                    <p class="hidden text-red-500 text-xs italic">Please fill out this field.</p>
				                                </div>
				                                <div class="w-full py-1 px-3">
				                                    <label class="hidden block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-first-name">
				                                    Phone
				                                    </label>
				                                    <input class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" placeholder="Phone">
				                                    <p class="hidden text-red-500 text-xs italic">Please fill out this field.</p>
				                                </div>
				                                <div class="w-full py-1 px-3">
				                                    <label class="hidden block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-first-name">
				                                    Start Date
				                                    </label>
				                                    <input class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" type="text" placeholder="Start Date">
				                                    <p class="hidden text-red-500 text-xs italic">Please fill out this field.</p>
				                                </div>
				                            </div>
				                            
				                            <a v-bind:href="liquijobsCreate" class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full" style="display: inline-block; width: 100% !important; text-align: center;"> ADD NEW JOB <svg style="display: inline; float: inline-end;" class="size-6 shrink-0 stroke-[#FFFFFF]" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M4.5 12h15m0 0l-6.75-6.75M19.5 12l-6.75 6.75"/></svg> </a>
				                        </form>
				                    </div>

				                    
				                </div>
				            </div>

				            <!-- RIGHT PART -->
				            <div id="right-side" class="lg:col-span-2">
				                
				                <!-- curret job selected /recent jobs -->
				                <div id="recent-jobs" class="grid mb-2 items-start gap-4 rounded-lg bg-white p-6 shadow-[0px_14px_34px_0px_rgba(0,0,0,0.08)] ring-1 ring-white/[0.05] transition duration-300 hover:text-black/70 hover:ring-black/20 focus:outline-none focus-visible:ring-[#FF2D20] lg:pb-10 dark:bg-zinc-900 dark:ring-zinc-800 dark:hover:text-white/70 dark:hover:ring-zinc-700 dark:focus-visible:ring-[#FF2D20] lg\:pt-0 sm\:pt-0" style="padding-top: 0; padding-left: 0.5em;">

				                	<div class="mt-6 float-right">
					                	<a href="/liquijobs" class="w-half bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full" style="float: right;">Back to Jobs</a>
					                </div>

								    <div class="relative flex flex-col " style="width: 100%; text-align: center;">
								        <h1 class="text-center font-bold text-xl">{{props.liquijobs.building}}</h1>
								    </div>
								    <div class="relative flex flex-col rounded-lg bg-white shadow-sm border border-slate-200">
								      
								        <ul style="padding: 0 0.5rem 0 0.5rem;">
								            
								            <li>
								            	<!-- <h5 class="mb-2 text-slate-800 text-xl font-semibold">
								                      Building: {{props.liquijobs.so_number}}
								                    </h5> -->
								            	<div class="relative flex flex-col my-6 bg-white shadow-sm border border-slate-200 rounded-lg w-96" style="width: 100%;">
								                  	<div class="p-4">
								                    <p class="text-slate-600 leading-normal font-light">
								                      <b style="font-weight: bold;">Corporate Address: </b> {{props.liquijobs.corporate_address}}
								                    </p>
								                	</div>
								                    <div class="p-4">
								                    <p class="text-slate-600 leading-normal font-light">
								                      <b style="font-weight: bold;">Contact Name: </b> {{props.liquijobs.contact_name}}
								                    </p>
								                	</div>
								                    <div class="p-4">
								                    <p class="text-slate-600 leading-normal font-light">
								                      <b style="font-weight: bold;">Phone: </b> {{props.liquijobs.contact_telephone}}
								                    </p>
								                	</div>
								                    <div class="p-4">
								                    <p class="text-slate-600 leading-normal font-light">
								                      <b style="font-weight: bold;">Email: </b> {{props.liquijobs.contact_email}}
								                    </p>
								                	</div>
								                    <div class="p-4">
								                    <p class="text-slate-600 leading-normal font-light">
								                      <b style="font-weight: bold;">Location Name: </b> {{props.liquijobs.location_address}}
								                    </p>
								                	</div>
								                    <div class="p-4">
								                    <p class="text-slate-600 leading-normal font-light">
								                      <b style="font-weight: bold;">Start Date: </b> {{props.liquijobs.start_date}}
								                    </p>
								                	</div>
								                  </div>
								        	</li>
								            <li style="text-align: center;">
								            	<!-- <button class="w-half bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full"> VIEW ASSETS <svg style="display: inline; float: inline-end;" class="size-6 shrink-0 stroke-[#FFFFFF]" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M4.5 12h15m0 0l-6.75-6.75M19.5 12l-6.75 6.75"/></svg> </button> -->
								            	<a v-bind:href="liquiassetsurl" class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full" style="display: inline-block; width: 100% !important;"> ADD ASSETS </a>
								            </li>
								        </ul>
								        <!-- images -->
								        <ul style="padding: 0 0.5rem 0 0.5rem; display: inline; padding-bottom: 1em; min-height: 250px;">
								            
								        	
											  <li v-for="item in job_assets" :key="id" :value="id" style="vertical-align: top; display: inline; margin-left: 1em;">
								            	<!-- <img :src="'/uploads/images/' + item.job_asset" style="margin: 0 1em 0 1em;" width="300" height="300" onerror="https://lh3.googleusercontent.com/pw/AP1GczMGQYta83vV-qTtHVNR0Fz97llzvKe2OoGu6_OD-j6HSGe-eaTa7rcoshYfAUz4g75XPtnrA5aVzi2CC8MOHREyrIYJPYe0CzZy9D5AC0P_ffazpNPHRihvaGzKJ7IFkGwVroZM1-fqnmNZH1gIgHVabw=w1966-h1474-s-no-gm?authuser=0" /> -->
								            	<img style="vertical-align: top; display: inline; margin: 1em 1em 1em 1em; background-image: url('https://lh3.googleusercontent.com/pw/AP1GczMGQYta83vV-qTtHVNR0Fz97llzvKe2OoGu6_OD-j6HSGe-eaTa7rcoshYfAUz4g75XPtnrA5aVzi2CC8MOHREyrIYJPYe0CzZy9D5AC0P_ffazpNPHRihvaGzKJ7IFkGwVroZM1-fqnmNZH1gIgHVabw=w1966-h1474-s-no-gm?authuser=0');" width="300" height="300" :src="item.job_asset" />
								            </li>
											

								        </ul>
								    </div> 
								</div>
				                <!-- curret job selected / recent jobs -->
    
				                
				                <form id="manualform" @submit.prevent="submitaddasset" class=" mt-6 space-y-2"
										enctype="multipart/form-data">
										<!-- Asset Details Form Fields -->
										<div
											class="flex border-divider pb-2 items-end justify-start sm:justify-end sm:flex-row flex-col flex-wrap">
											<InputLabel for="asset_category" value="Category"
												class="w-full lg:w-[60%]" />
											<select ref="myBtn" @click="assetCategoryClickEvent" v-model="formasset.asset_category" id="typex"
												class="w-full lg:w-[40%] sm:mt-0 mt-2 appearance-none block w-full px-4 py-2 primary-dark-blue placeholder-[#8c8c97] font-rethinksansmedium border-[#f2f4f7] bg-[#f2f4f7] rounded-lg focus:outline-none"
												name="asset_category" required @change="openMenuSelect">
												<option class="text-base md:text-xs lg:text-base" disabled hidden value="">
													Select Category</option>
												<option class="text-base md:text-xs lg:text-base" value="it">IT</option>
												<option class="text-base md:text-xs lg:text-base"
													value="infrastructure">
													Infrastructure</option>
												<option class="text-base md:text-xs lg:text-base" value="furniture">
													Furniture
												</option>
											</select>
											<InputError class="mt-2 w-full lg:w-[40%]"
												:message="formasset.errors.asset_category" />
										</div>
										<div id="assettypediv"
											class="hidden flex border-divider pb-2 items-end justify-start sm:justify-end sm:flex-row flex-col flex-wrap">
											<InputLabel for="asset_type" value="Type" class="w-full lg:w-[60%]" />
											<select v-model="formasset.asset_type" id="furniture_asset_type"
												class="w-full lg:w-[40%] sm:mt-0 mt-2 appearance-none block w-full px-4 py-2 primary-dark-blue placeholder-[#8c8c97] font-rethinksansmedium border-[#f2f4f7] bg-[#f2f4f7] rounded-lg focus:outline-none"
												name="asset_type" :class="isOpenFurniture ? 'block' : 'hidden'" required>
												<optgroup class="text-base md:text-xs lg:text-base" label="Furniture">
													<option class="text-base md:text-xs lg:text-base" value="" selected
														disabled hidden>Select Furniture Type
													</option>
													<option class="text-base md:text-xs lg:text-base"
														value="furniture-cubicle">
														Cubicle</option>
													<option class="text-base md:text-xs lg:text-base"
														value="furniture-casegood">Case Good</option>
													<option class="text-base md:text-xs lg:text-base"
														value="furniture-chair">
														Chair</option>
													<option class="text-base md:text-xs lg:text-base"
														value="furniture-wallhanging">Wall Hanging</option>
													<option class="text-base md:text-xs lg:text-base"
														value="furniture-appliance">Appliance</option>
													<option class="text-base md:text-xs lg:text-base"
														value="furniture-others">
														Others</option>
												</optgroup>
											</select>
											<select v-model="formasset.asset_type" id="it_asset_type"
												class="w-full lg:w-[40%] sm:mt-0 mt-2 appearance-none block w-full px-4 py-2 primary-dark-blue placeholder-[#8c8c97] font-rethinksansmedium border-[#f2f4f7] bg-[#f2f4f7] rounded-lg focus:outline-none"
												name="asset_type" :class="isOpenIt ? 'block' : 'hidden'" required>
												<optgroup class="text-base md:text-xs lg:text-base" label="IT">
													<option class="text-base md:text-xs lg:text-base" value="" selected
														disabled hidden>Select IT Type</option>
													<option class="text-base md:text-xs lg:text-base"
														value="it-networkgear">
														Network Gear</option>
													<option class="text-base md:text-xs lg:text-base"
														value="it-servers">Servers
													</option>
													<option class="text-base md:text-xs lg:text-base" value="it-pcs">PCs
													</option>
													<option class="text-base md:text-xs lg:text-base"
														value="it-laptops">Laptops
													</option>
													<option class="text-base md:text-xs lg:text-base" value="it-rack">
														Rack
													</option>
													<option class="text-base md:text-xs lg:text-base"
														value="it-telecom">Telecom
													</option>
													<option class="text-base md:text-xs lg:text-base"
														value="it-monitors">
														Monitors</option>
													<option class="text-base md:text-xs lg:text-base" value="it-camera">
														Camera
													</option>
													<option class="text-base md:text-xs lg:text-base"
														value="it-printers">
														Printers</option>
													<option class="text-base md:text-xs lg:text-base" value="it-others">
														Others
													</option>
												</optgroup>
											</select>
											<select v-model="formasset.asset_type" id="infrastructure_asset_type"
												class="w-full lg:w-[40%] sm:mt-0 mt-2 appearance-none block w-full px-4 py-2 primary-dark-blue placeholder-[#8c8c97] font-rethinksansmedium border-[#f2f4f7] bg-[#f2f4f7] rounded-lg focus:outline-none"
												name="asset_type" :class="isOpenInfrastructure ? 'block' : 'hidden'" required>
												<optgroup class="text-base md:text-xs lg:text-base"
													label="Infrastructure">
													<option class="text-base md:text-xs lg:text-base" value="" selected
														disabled hidden>Select Infrastructure Type
													</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-generator">Generator</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-cracunit">CRAC Unit</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-ups">UPS</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-ats">ATS</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-bypass">Bypass</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-switchgear">Switchgear</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-batteries">Batteries</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-wiringlowvoltage">Wiring, Low-Voltage
													</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-wiringhighvoltage">Wiring,
														High-Voltage
													</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-firesuppressant">Fire Suppressant
													</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-raisedflooring">Raised Flooring
													</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-paintchemical">Paint/Chemical</option>
													<option class="text-base md:text-xs lg:text-base"
														value="infrastructure-others">Others</option>
												</optgroup>
											</select>
											<InputError class="mt-2 w-full lg:w-[40%]"
												:message="formasset.errors.asset_type" />
											<div class="w-[40%]"></div>
										</div>
										<div
											class="flex border-divider pb-2 items-end justify-start sm:justify-end sm:flex-row flex-col flex-wrap">
											<InputLabel for="asset_quantity" value="Quantity"
												class="w-full lg:w-[60%]" />
											<TextInput class="w-full lg:w-[40%] px-4 py-2" id="asset_quantity"
												type="number" placeholder="Quantity" v-model="formasset.asset_quantity"
												required />
											<InputError class="mt-2 w-full lg:w-[40%]"
												:message="formasset.errors.asset_quantity" />
										</div>
										<div class="flex border-divider pb-2 items-start justify-start sm:justify-end sm:flex-row flex-col flex-wrap">
											<div class="w-full lg:w-[60%] lg:mt-1">
												<InputLabel for="asset_make" value="Make"/>
												<div class="flex items-center gap-2">
													<label class="switch">
														<input type="checkbox" :checked="checkMake" @change="toggleMakeUpload" />
														<span class="slider round"></span>
													</label>
													<span :class="checkMake ? 'block' : 'hidden'">Hide upload</span>
													<span :class="!checkMake ? 'block' : 'hidden'">Add Make via image upload</span>
												</div>
											</div>
											<div class="w-full lg:w-[40%] pb-2">
												<TextInput class="px-4 py-2" id="asset_make" name="asset_make" type="text" :placeholder="checkMake ? '' : 'ex. Simmons, Philips, Toshiba..'"
													v-model="formasset.asset_make" :class="checkMake ? 'placeholder-[#8c8c97]' : ''"/>
												<form v-if="checkMake" class="lg:block flex flex-col md:flex-row justify-between mt-2" @submit.prevent="processocrmake" enctype="multipart/form-data">
													<input class="w-full sm:w-[60%] lg:w-full" type="file" @input="formasset2.job_asset = $event.target.files[0]" name="job_asset">
													<PrimaryButton class="mt-2 md:mt-0 lg:mt-2 w-auto" :disabled="formasset2.processing">
														<span class="text-base">Process Image</span>
													</PrimaryButton>
												</form>
												<InputError class="mt-2 w-full"
														:message="formasset.errors.asset_make" />
											</div>
										</div>
										<div class="flex border-divider pb-2 items-start justify-start sm:justify-end sm:flex-row flex-col flex-wrap">
											<div class="w-full lg:w-[60%] lg:mt-1">
												<InputLabel for="asset_model" value=" Model" />
												<div class="flex items-center gap-2">
													<label class="switch">
														<input type="checkbox" :checked="checkModel" @change="toggleModelUpload" />
														<span class="slider round"></span>
													</label>
													<span :class="checkModel ? 'block' : 'hidden'">Hide upload</span>
													<span :class="!checkModel ? 'block' : 'hidden'">Add Model via image upload</span>
												</div>
											</div>
											<div class="w-full lg:w-[40%] pb-2">
												<TextInput class="px-4 py-2" id="asset_model" name="asset_model" type="text" :placeholder="checkModel ? '' : 'ex. SQ-12..'" 
												v-model="formasset.asset_model" :class="checkModel ? 'placeholder-[#8c8c97]' : ''" />
												<form v-if="checkModel" class="lg:block flex flex-col md:flex-row justify-between mt-2" @submit.prevent="processocrmodel" enctype="multipart/form-data">
													<input class="w-full sm:w-[60%] lg:w-full" type="file" @input="formasset3.job_asset = $event.target.files[0]" name="job_asset" >
													<PrimaryButton class="mt-2 md:mt-0 lg:mt-2 w-auto" :disabled="formasset3.processing">
														<span class="text-base">Process Image</span>
													</PrimaryButton>
												</form>
												<InputError class="mt-2 w-full"
													:message="formasset.errors.asset_model" />
											</div>
										</div>
										<div class="flex border-divider pb-2 items-start justify-start sm:justify-end sm:flex-row flex-col flex-wrap">
											<div class="w-full lg:w-[60%] lg:mt-1">
												<InputLabel for="asset_serial" value="Serial" />
												<div class="flex items-center gap-2">
													<label class="switch">
														<input type="checkbox" :checked="checkSerial" @change="toggleSerialUpload" />
														<span class="slider round"></span>
													</label>
													<span :class="checkSerial ? 'block' : 'hidden'">Hide upload</span>
													<span :class="!checkSerial ? 'block' : 'hidden'">Add Serial via image upload</span>
												</div>
											</div>
											<div class="w-full lg:w-[40%] pb-2">
												<TextInput class="px-4 py-2" id="asset_serial" name="asset_serial" type="text" :placeholder="checkSerial ? '' : 'ex. HFIOE18DHIN23-23..'" 
												v-model="formasset.asset_serial" :class="checkSerial ? 'placeholder-[#8c8c97]' : ''" />
												<form v-if="checkSerial" class="lg:block flex flex-col md:flex-row justify-between mt-2" @submit.prevent="processocrserial" enctype="multipart/form-data">
													<input class="w-full sm:w-[60%] lg:w-full" type="file" @input="formasset4.job_asset = $event.target.files[0]" name="job_asset" >
													<PrimaryButton class="mt-2 md:mt-0 lg:mt-2 w-auto" :disabled="formasset4.processing">
														<span class="text-base">Process Image</span>
													</PrimaryButton>
												</form>
												<InputError class="mt-2 w-full"
													:message="formasset.errors.asset_serial" />
											</div>
										</div>
										<div
											class="flex border-divider pb-2 items-end justify-start sm:justify-end sm:flex-row flex-col flex-wrap">
											<InputLabel for="asset_weight_each" value="Weight Each"
												class="w-full lg:w-[60%]" />
											<TextInput class="w-full lg:w-[40%] px-4 py-2" id="asset_weight_each"
												type="text" placeholder="ex. 12 lbs"
												v-model="formasset.asset_weight_each" />
											<InputError class="mt-2 w-full lg:w-[40%]"
												:message="formasset.errors.asset_weight_each" />
										</div>
										<div
											class="flex border-divider pb-2 items-end justify-start sm:justify-end sm:flex-row flex-col flex-wrap">
											<InputLabel for="asset_description" value="Description"
												class="w-full lg:w-[60%]" />
											<TextInput class="w-full lg:w-[40%] px-4 py-2" id="asset_description"
												type="text" placeholder="Description"
												v-model="formasset.asset_description" />
											<InputError class="mt-2 w-full lg:w-[40%]"
												:message="formasset.errors.asset_description" />
										</div>
										<div
											class="flex border-divider pb-2 items-end justify-start sm:justify-end sm:flex-row flex-col flex-wrap">
											<InputLabel for="asset_status" value="Status" class="w-full lg:w-[60%]" />
											<select v-model="formasset.asset_status" id="asset_status"
												class="w-full lg:w-[40%] px-4 py-2 sm:mt-0 mt-2 appearance-none block w-full p-4 primary-dark-blue placeholder-[#8c8c97] font-rethinksansmedium border-[#f2f4f7] bg-[#f2f4f7] rounded-lg focus:outline-none"
												name="asset_status" @change="openStatusMenuSelect">
												<option class="text-base md:text-xs lg:text-base" value=""
													disabled hidden>Select Status</option>
												<option class="text-base md:text-xs lg:text-base" value="originalstate">
													Original
													State</option>
												<option class="text-base md:text-xs lg:text-base"
													value="workinprogress">Work In
													Progress</option>
												<option class="text-base md:text-xs lg:text-base" value="completed">
													Completed
												</option>
											</select>
										</div>

										<div id="assetdispositiondiv"
											class="hidden flex border-divider pb-2 items-end justify-start sm:justify-end sm:flex-row flex-col flex-wrap">
											<InputLabel for="asset_disposition" value="Asset Disposition"
												class="w-full lg:w-[60%]" />

											<select v-model="formasset.asset_disposition" id="asset_status"
												class="w-full lg:w-[40%] px-4 py-2 sm:mt-0 mt-2 appearance-none block w-full p-4 primary-dark-blue placeholder-[#8c8c97] font-rethinksansmedium border-[#f2f4f7] bg-[#f2f4f7] rounded-lg focus:outline-none"
												name="asset_status" @change="openAssetStatusMiniForm">
												<option class="text-base md:text-xs lg:text-base" value="" selected
													disabled hidden>Select Disposition</option>
												<option class="text-base md:text-xs lg:text-base" value="resold">Resold
												</option>
												<option class="text-base md:text-xs lg:text-base" value="recycled">
													Recycled
												</option>
												<option class="text-base md:text-xs lg:text-base" value="disposed">
													Disposed
												</option>
												<option class="text-base md:text-xs lg:text-base" value="returned">
													Returned
												</option>
											</select>


											<div class="w-full lg:w-[70%] float-none md:float-right mt-3">
												<div id="resold"
													class="hidden flex sm:flex-row flex-col justify-end gap-1">
													<input v-model="formasset.assetdisdate"
														class="p-2 w-full lg:w-[25%] md:w-[33.3%] text-sm primary-dark-blue placeholder-[#8c8c97] font-rethinksansmedium border-[#323581] bg-[#f2f4f7] rounded-lg focus:outline-none"
														type="date" name="assetdisdate" placeholder="Date" />
													<input v-model="formasset.assetdiswho"
														class="p-2 w-full lg:w-[25%] md:w-[33.3%] text-sm primary-dark-blue placeholder-[#8c8c97] font-rethinksansmedium border-[#323581] bg-[#f2f4f7] rounded-lg focus:outline-none"
														type="text" name="assetdiswho" placeholder="Who" />
													<input v-model="formasset.assetdisticketshippinginfo"
														class="p-2 w-full lg:w-[40%] md:w-[33.3%] text-sm primary-dark-blue placeholder-[#8c8c97] font-rethinksansmedium border-[#323581] bg-[#f2f4f7] rounded-lg focus:outline-none"
														type="text" name="assetdisticketshippinginfo"
														placeholder="Shipping/Ticket Info" />
												</div>
												
											</div>

											<InputError class="mt-2 w-full lg:w-[40%]"
												:message="formasset.errors.asset_status" />
										</div>
										<!-- END OF : Asset Details Form Fields -->
										<div
											class="flex items-end justify-start sm:justify-end sm:flex-row flex-col flex-wrap">
											<div class="mt-6 sm:w-[60%] w-full flex flex-col">
												<InputLabel for="job_asset" value="Job Asset"
													class="w-full lg:w-[60%]" />
												<!-- <input type="file" @input="form.avatar = $event.target.files[0]" name="job_asset" class="mt-1 block w-full" v-on:change="onImageChange" > -->
												<input required type="file"
													@input="formasset.job_asset = $event.target.files[0]"
													name="job_asset" class="mt-1 block w-full">
												<input type="hidden" name="job_id" v-model="formasset.jobid">
												<InputError class="mt-2 w-full lg:w-[40%]"
													:message="formasset.errors.job_asset" />
											</div>

											<div class="mt-6 sm:w-[40%] w-full flex flex-col">
												<InputLabel for="job_asset_additional_images" value="Additional Images"
													class="w-full lg:w-[60%]" />
												<!-- <input type="file" @input="form.avatar = $event.target.files[0]" name="job_asset" class="mt-1 block w-full" v-on:change="onImageChange" > -->
												<input type="file"
													@input="formasset.job_asset_additional_images = $event.target.files"
													name="job_asset_additional_images[]" class="mt-1 block w-full" multiple>
												<input type="hidden" name="job_id" v-model="formasset.jobid">
												<InputError class="mt-2 w-full lg:w-[40%]"
													:message="formasset.errors.job_asset_additional_images" />
											</div>
											<div
												class="sm:w-[40%] w-full flex sm:justify-end justify-start sm:mt-0 mt-6">
												<PrimaryButton :disabled="form.processing"
													class="py-3 px-4 sm:w-auto w-full">
													<span class="text-base">Go</span> <svg
														class="size-6 shrink-0 stroke-[#FFFFFF]"
														xmlns="http://www.w3.org/2000/svg" fill="none"
														viewBox="0 0 24 24" stroke-width="1.5"
														style="display: inline; float: inline-end; margin-left: 5px;">
														<path stroke-linecap="round" stroke-linejoin="round"
															d="M4.5 12h15m0 0l-6.75-6.75M19.5 12l-6.75 6.75"></path>
													</svg>
												</PrimaryButton>
												<Transition enter-active-class="transition ease-in-out"
													enter-from-class="opacity-0"
													leave-active-class="transition ease-in-out"
													leave-to-class="opacity-0">
													<p v-if="formasset.recentlySuccessful"
														class="text-sm text-gray-600">Saved.
													</p>
												</Transition>
											</div>
										</div>
									</form>
				                
				            </div>

				            

				        </div>


				        <!-- CALENDAR -->
				        <div class="grid gap-6 lg:grid-cols-1 lg:gap-8" style="margin-top: 2em;">
				            <!-- Container for CALENDAR -->
				            <div id="calendar-container" class="flex flex-col items-start gap-12 overflow-hidden rounded-lg bg-white shadow-[0px_14px_34px_0px_rgba(0,0,0,0.08)] ring-1 ring-white/[0.05] transition duration-300 hover:text-black/70 hover:ring-black/20 focus:outline-none focus-visible:ring-[#FF2D20] md:row-span-3 lg:p-12 lg:pb-10 dark:bg-zinc-900 dark:ring-zinc-800 dark:hover:text-white/70 dark:hover:ring-zinc-700 dark:focus-visible:ring-[#FF2D20]">
				                <Calendar />
				            </div>
				        </div>
				        
				    </div> <!-- end of unlabeled div -->
                </div>
            </div>
        </div>
        <!-- -->
        <!-- <h1>VIEW VUE PAGE</h1> -->
		<div class="py-12" style="display: none;">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 space-y-6">
                <h1 class="text-2xl">{{props.liquijobs.so_number}}</h1>
                <div>
                    {{props.liquijobs.so_number}}
                </div>
            </div>
        </div>
        <!-- -->
    </AppLayout>
    	
</template>