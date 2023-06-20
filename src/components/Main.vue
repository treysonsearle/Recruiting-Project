<template>
  <div>
    <GuestTable/>
  </div>
</template>

<script>
  import GuestTable from './GuestTable.vue'
  // eslint-disable-next-line no-unused-vars
  const GuestRepository = require('../guest-repository');

  export default {
    components: {
      GuestTable
    },
    data: () => {
      return { };
    },
  }
</script>
