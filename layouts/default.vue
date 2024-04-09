<template>
  <div class="p-4 max-w-[1300px] mx-auto">
    <header class="p-4 flex justify-between border rounded-full">
      <a href="/">
        <img src="~/assets/images/logo.png" alt="" />
      </a>
      <ul class="md:flex hidden md:visible items-center gap-4 uppercase text-gray-400 font-bold">
        <li class="border-b-4 border-orange-500 text-gray-900 transition-all">
          <a href="#">Home</a>
        </li>
        <li
          class="border-b-4 border-transparent transition-all hover:border-orange-500 hover:text-gray-900"
        >
          <a href="#">recipes</a>
        </li>
        <li
          class="border-b-4 border-transparent transition-all hover:border-orange-500 hover:text-gray-900"
        >
          <a href="#">cooking tips</a>
        </li>
        <li
          class="border-b-4 border-transparent transition-all hover:border-orange-500 hover:text-gray-900"
        >
          <a href="#">about us</a>
        </li>
      </ul>
      <div class="md:flex hidden md:visible items-center gap-4">
        <button class="bg-gray-100 w-8 h-8 rounded-full">
          <i class="fa fa-search"></i>
        </button>
        <button class="text-white bg-gray-900 h-8 px-6 rounded-full uppercase">
          subscribe
        </button>
      </div>
    </header>
    <slot></slot>
    <footer class="rounded-2xl bg-gray-900 p-6">
      <div class="text-white text-center text-sm">Copyright: © 2024 Cooks Delight.</div>
    </footer>
  </div>
</template>