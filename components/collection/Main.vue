<template>
    <div>
       <CollectionList :detailsData="users" />
       <CollectionAdd></CollectionAdd>
    </div>
</template>

<script setup lang="ts">

const users = await useAuthLazyFetch("https://v1-orm-emc2-messaging.mars.hipso.cc/user-prefs/")
console.log("userrssss",users)

</script>