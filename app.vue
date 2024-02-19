<template>
  <div>
  </div>
</template>

<script setup lang="ts">

useSeoMeta({
  title: 'shortRinth',
  ogTitle: 'shortRinth',
  description: 'Modrinth, but shorter.',
  ogDescription: 'Modrinth, but shorter.',
  ogImage: 'https://www.worldwidepixel.ca/icon.ico',
})

const route = useRoute();

console.log(route.fullPath);

if (route.fullPath.includes("@")) {

  await navigateTo(`https://modrinth.com/user${route.fullPath.replace("@", "")}`, { external: true })

} else if (route.fullPath.includes("/o/")) {

  await navigateTo(`https://modrinth.com/organization${route.fullPath.replace("/o", "")}`, { external: true })

} else if (route.fullPath.includes("/u/")) {

  await navigateTo(`https://modrinth.com/user${route.fullPath.replace("/u", "")}`, { external: true })

} else if (route.fullPath.includes("/p/")) {

  await navigateTo(`https://modrinth.com/project${route.fullPath.replace("/p", "")}`, { external: true })

} else if (route.fullPath.includes("/l/")) {

  await navigateTo(`https://modrinth.com/legal${route.fullPath.replace("/l", "")}`, { external: true })

} else if (route.fullPath.includes("/b/")) {

  await navigateTo(`https://blog.modrinth.com/p${route.fullPath.replace("/b", "")}`, { external: true })

} else if (route.fullPath.includes("/status")) {

  await navigateTo(`https://status.modrinth.com/`, { external: true })

} else if (route.fullPath.includes("/")) {

    try {
      const { data, pending, status, error } = await useFetch(`https://modrinth.com/project${route.fullPath}`);
      if (status.value === "success") {
        await navigateTo(`https://modrinth.com/project${route.fullPath}`, { external: true })
      } else {
        await navigateTo(`https://modrinth.com/`, { external: true })
      }
    } catch (error) {
      //await console.error('Error fetching data:', error);
      await navigateTo(`https://modrinth.com/`, { external: true })
    }

} else {

  await navigateTo(`https://modrinth.com/`, { external: true })

}

</script>