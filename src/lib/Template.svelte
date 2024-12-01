<script>
  import Sidebar from './Sidebar.svelte';
  import { onMount } from 'svelte';
  import NavButton from './ui/NavButton.svelte';

  async function toggleSidebar(event) {
    event.preventDefault();
    const sideBarNav = document.getElementById("mobile-nav").classList;
    if (sideBarNav.contains("hidden")) {
      sideBarNav.remove("hidden");
    }
  }

  async function checkNavigation() {
    if (window.innerWidth > 1024) {
      const mobileSideBar = document.getElementById("mobile-nav");
      mobileSideBar.classList.add('hidden');
    }
  }

  onMount(() => {
    checkNavigation();
    window.addEventListener('resize', checkNavigation);

    return () => {
      window.removeEventListener('resize', checkNavigation);
    };
  });

  let isOpen = false;

  async function toggleMenu() {
    isOpen = !isOpen;
  }

  async function closeMenu(event) {
    if (event.target.closest('.menu-container')) return;
    isOpen = false;
  }

  onMount(() => {
    window.addEventListener('click', closeMenu);
    return () => window.removeEventListener('click', closeMenu);
  });

</script>

<main>

  <div>

    <Sidebar></Sidebar>

    <div class="lg:pl-72 ">
      <div class="sticky top-0 z-40 flex h-16 shrink-0 items-center gap-x-4 border-b border-gray-200 bg-white px-4 shadow-sm sm:gap-x-6 sm:px-6 lg:px-8">
        <button type="button" class="-m-2.5 p-2.5 text-gray-700 lg:hidden" on:click={toggleSidebar}>
          <span class="sr-only">Open sidebar</span>
          <svg class="size-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true" data-slot="icon">
            <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
          </svg>
        </button>

        <div class="flex flex-1 gap-x-4 lg:gap-x-6">
          <form class="relative flex flex-1 " action="#" method="GET">
            <label for="search-field" class="sr-only">Search</label>

            <input id="search-field" class="block size-full border-0 py-0 pl-8 pr-0 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm" placeholder="" type="search" name="search">
          </form>

          <div class="flex items-center gap-x-4 lg:gap-x-6">
            <NavButton icon="bell" label="View notifications" hoverColor="red" />

            <NavButton icon="db" label="View notifications" hoverColor="red" />

            <!-- Separator -->
            <div class="hidden lg:block lg:h-6 lg:w-px" aria-hidden="true"></div>

            <!-- Profile dropdown -->

            <div class="relative menu-container">
              <button type="button" class="-m-1.5 flex items-center p-1.5" on:click={toggleMenu}>
                <span class="sr-only">Open user menu</span>
                <img class="size-8 rounded-full bg-gray-50" src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80" alt="">
                <span class="hidden lg:flex lg:items-center">
                  <span class="ml-4 text-sm/6 font-semibold text-gray-900" aria-hidden="true">Tom Cook</span>
                  <svg class="ml-2 size-5 text-gray-400" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                    <path fill-rule="evenodd" d="M5.22 8.22a.75.75 0 0 1 1.06 0L10 11.94l3.72-3.72a.75.75 0 1 1 1.06 1.06l-4.25 4.25a.75.75 0 0 1-1.06 0L5.22 9.28a.75.75 0 0 1 0-1.06Z" clip-rule="evenodd" />
                  </svg>
                </span>
              </button>
            
              {#if isOpen}
                <div class="absolute right-0 z-10 mt-2.5 w-32 origin-top-right rounded-md bg-white py-2 shadow-lg ring-1 ring-gray-900/5" role="menu" aria-orientation="vertical" tabindex="-1">
                  <a href="#" class="block px-3 py-1 text-sm/6 text-gray-900" role="menuitem" tabindex="-1">Your profile</a>
                  <a href="#" class="block px-3 py-1 text-sm/6 text-gray-900" role="menuitem" tabindex="-1">Sign out</a>
                </div>
              {/if}
            </div>
          </div>
        </div>
      </div>

      <nav class="bg-white shadow" id="nav-shadow">
        <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
          <div class="flex h-16 justify-between">
            <div class="flex">
              <div class="-ml-2 mr-2 flex items-center md:hidden">
                <!-- Mobile menu button -->
                <button type="button" class="relative inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:bg-gray-100 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500" aria-controls="mobile-menu" aria-expanded="false">
                  <span class="absolute -inset-0.5"></span>
                  <span class="sr-only">Open main menu</span>
                  <!--
                    Icon when menu is closed.

                    Menu open: "hidden", Menu closed: "block"
                  -->
                  <svg class="block size-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true" data-slot="icon">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
                  </svg>

                  <!--
                    Icon when menu is open.

                    Menu open: "block", Menu closed: "hidden"
                  -->

                </button>
              </div>

              <div class="hidden md:ml-6 md:flex md:space-x-8">
                <!-- Current: "border-indigo-500 text-gray-900", Default: "border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700" -->
                <a href="#" class="inline-flex items-center border-b-2 border-indigo-500 px-1 pt-1 text-sm font-medium text-gray-900">Dashboard</a>
                <a href="#" class="inline-flex items-center border-b-2 border-transparent px-1 pt-1 text-sm font-medium text-gray-500 hover:border-gray-300 hover:text-gray-700">Team</a>
                <a href="#" class="inline-flex items-center border-b-2 border-transparent px-1 pt-1 text-sm font-medium text-gray-500 hover:border-gray-300 hover:text-gray-700">Projects</a>
                <a href="#" class="inline-flex items-center border-b-2 border-transparent px-1 pt-1 text-sm font-medium text-gray-500 hover:border-gray-300 hover:text-gray-700">Calendar</a>
              </div>
            </div>
            <div class="flex items-center">
              <div class="shrink-0  px-5">
                <button type="button" class="relative inline-flex items-center gap-x-1.5 rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
                    Edit
                </button>
              </div>
              <div class="shrink-0">
                <button type="button" class="relative inline-flex items-center gap-x-1.5 rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
                  <svg class="-ml-0.5 size-5" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true" data-slot="icon">
                    <path d="M10.75 4.75a.75.75 0 0 0-1.5 0v4.5h-4.5a.75.75 0 0 0 0 1.5h4.5v4.5a.75.75 0 0 0 1.5 0v-4.5h4.5a.75.75 0 0 0 0-1.5h-4.5v-4.5Z" />
                  </svg>
                  New Job
                </button>
              </div>
            </div>
          </div>
        </div>

        <!-- Mobile menu, show/hide based on menu state. -->
        <div class="md:hidden" id="mobile-menu">
          <div class="space-y-1 pb-3 pt-2">
            <!-- Current: "bg-indigo-50 border-indigo-500 text-indigo-700", Default: "border-transparent text-gray-500 hover:bg-gray-50 hover:border-gray-300 hover:text-gray-700" -->
            <a href="#" class="block border-l-4 border-indigo-500 bg-indigo-50 py-2 pl-3 pr-4 text-base font-medium text-indigo-700 sm:pl-5 sm:pr-6">Dashboard</a>
            <a href="#" class="block border-l-4 border-transparent py-2 pl-3 pr-4 text-base font-medium text-gray-500 hover:border-gray-300 hover:bg-gray-50 hover:text-gray-700 sm:pl-5 sm:pr-6">Team</a>
            <a href="#" class="block border-l-4 border-transparent py-2 pl-3 pr-4 text-base font-medium text-gray-500 hover:border-gray-300 hover:bg-gray-50 hover:text-gray-700 sm:pl-5 sm:pr-6">Projects</a>
            <a href="#" class="block border-l-4 border-transparent py-2 pl-3 pr-4 text-base font-medium text-gray-500 hover:border-gray-300 hover:bg-gray-50 hover:text-gray-700 sm:pl-5 sm:pr-6">Calendar</a>
          </div>

        </div>
      </nav>

      <div class="mx-auto max-w-7xl px-4 py-7 sm:px-6 lg:px-8 rounded-md">
        <div class="overflow-hidden rounded-lg bg-white shadow">
          <h2 class="sr-only" id="profile-overview-title">Profile Overview</h2>
          <div class="bg-white p-6">
            <div class="sm:flex sm:items-center sm:justify-between">
              <div class="sm:flex sm:space-x-5">
                <div class="shrink-0">
                  <img class="mx-auto size-20 rounded-full" src="https://i.pinimg.com/736x/16/01/4d/16014d4ba2c95438a77e1ad51fadda1e.jpg" alt="">
                </div>
                <div class="mt-4 text-center sm:mt-0 sm:pt-1 sm:text-left">
                  <p class="text-sm font-medium text-gray-600">Welcome back,</p>
                  <p class="text-xl font-bold text-gray-900 sm:text-2xl">Tennis</p>
                  <p class="text-sm font-medium text-gray-600">Customer</p>
                </div>
              </div>
              <div class="mt-5 flex justify-center sm:mt-0">
                <a href="#" class="flex items-center justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50">View profile</a>
              </div>
            </div>
          </div>
        </div>

        <div class="min-h-full py-6">

        </div>
      </div>
    </div>
  </div>
</main>