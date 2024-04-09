<template>
  <div
    class="bg-white rounded-2xl overflow-hidden flex-none flex flex-col min-w-80"
    :class="size"
  >
    <div class="h-60">
      <img :src="image" alt="" class="w-full h-full object-cover" />
    </div>
    <div class="p-4 grow">
      <div class="text-2xl font-bold mb-2">{{ title }}</div>
      <div class="line-clamp-2">{{ description }}</div>
    </div>
    <div class="flex p-4 justify-between items-center">
      <div class="uppercase font-bold">
        {{ category }} {{ area ? `- ${area}` : "" }}
      </div>
      <button
        class="uppercase border border-gray-900 h-7 px-4 rounded-full font-bold"
      >
        view recipe
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    id: String,
    size: String,
    image: String,
    title: String,
    category: String,
    area: String,
    description: {
      type: String,
      default:
        "Lorem ipsum dolor sit amet consectetur adipisicing elit. In quis cumque possimus optio consequatur dolores nisi corporis, quia illum",
    },
  },
};
</script>