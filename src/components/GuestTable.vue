<template>
    <div>
      <div class="grid-wrapper padding-10">
        <h2>Guest Email</h2>
        <h2># of Tickets</h2>
        <h2>Edit Guest</h2>
        <h2>Delete Guest</h2>
      </div>
      <div 
        class="grid-wrapper padding-10"
        v-for="(guest, index) in guests" :key="index"
      >
        <div>{{ guest.email}}</div>
        <div>{{ guest.tickets}}</div>
        <div v-on:click="openEditGuestModal(guest, index)">
          <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 576 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M402.6 83.2l90.2 90.2c3.8 3.8 3.8 10 0 13.8L274.4 405.6l-92.8 10.3c-12.4 1.4-22.9-9.1-21.5-21.5l10.3-92.8L388.8 83.2c3.8-3.8 10-3.8 13.8 0zm162-22.9l-48.8-48.8c-15.2-15.2-39.9-15.2-55.2 0l-35.4 35.4c-3.8 3.8-3.8 10 0 13.8l90.2 90.2c3.8 3.8 10 3.8 13.8 0l35.4-35.4c15.2-15.3 15.2-40 0-55.2zM384 346.2V448H64V128h229.8c3.2 0 6.2-1.3 8.5-3.5l40-40c7.6-7.6 2.2-20.5-8.5-20.5H48C21.5 64 0 85.5 0 112v352c0 26.5 21.5 48 48 48h352c26.5 0 48-21.5 48-48V306.2c0-10.7-12.9-16-20.5-8.5l-40 40c-2.2 2.3-3.5 5.3-3.5 8.5z"/></svg>
        </div>
        <div v-on:click="deleteGuest(index)">
          <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 448 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M432 32H312l-9.4-18.7A24 24 0 0 0 281.1 0H166.8a23.72 23.72 0 0 0-21.4 13.3L136 32H16A16 16 0 0 0 0 48v32a16 16 0 0 0 16 16h416a16 16 0 0 0 16-16V48a16 16 0 0 0-16-16zM53.2 467a48 48 0 0 0 47.9 45h245.8a48 48 0 0 0 47.9-45L416 128H32z"/></svg>
        </div>
      </div>
      <div>
      <div class="flex-space-between">
      <div 
        class="flex-wrapper padding-10 add-guest"
        v-on:click="openAddGuestModal"
      >
        <h2>Add Guest</h2>
        <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M96 128a128 128 0 1 1 256 0A128 128 0 1 1 96 128zM0 482.3C0 383.8 79.8 304 178.3 304h91.4C368.2 304 448 383.8 448 482.3c0 16.4-13.3 29.7-29.7 29.7H29.7C13.3 512 0 498.7 0 482.3zM504 312V248H440c-13.3 0-24-10.7-24-24s10.7-24 24-24h64V136c0-13.3 10.7-24 24-24s24 10.7 24 24v64h64c13.3 0 24 10.7 24 24s-10.7 24-24 24H552v64c0 13.3-10.7 24-24 24s-24-10.7-24-24z"/></svg>
      </div>
      <h2>{{"Total Tickets: " + currentTotalOfTickets + "/" + maxTotalOfTickets }}</h2>
    </div>
    </div>
    <EditGuestModal
      v-if="showEditGuestModal"
      :current-total-of-tickets="currentTotalOfTickets"
      :max-total-of-tickets="maxTotalOfTickets"
      :current-guest="editGuest"
      :guest-index="editGuestIndex"
      @edit="updateGuest"
      @close="closeEditGuestModal"
    />
    <AddGuestModal 
      v-if="showAddGuestModal"
      :current-total-of-tickets="currentTotalOfTickets"
      :max-total-of-tickets="maxTotalOfTickets"
      @close="closeAddGuestModal"
      @add="addNewGuest"
    />
    </div>
  </template>
  
  <script>
    import AddGuestModal from './AddGuestModal.vue';
    import EditGuestModal from './EditGuestModal.vue';
    // eslint-disable-next-line no-unused-vars
    const GuestRepository = require('../guest-repository');
  
    export default {
      components: {
    AddGuestModal,
    EditGuestModal
},
      data: () => {
        return { 
            guests: [],
            maxTotalOfTickets: 20,
						currentTotalOfTickets: 0,
            showAddGuestModal: false,
            showEditGuestModal: false,
            editGuestIndex: 0,
            editGuest: null
        };
      },
			methods: {
        calcTotalTickets(){
          if(this.guests.length > 0){
            var totalTickets = 0
            this.guests.forEach(guest => {
              totalTickets += parseInt(guest.tickets)
            })
            this.currentTotalOfTickets = totalTickets
          }
        },
				getGuests(){
					const guestRepo = new GuestRepository()
					guestRepo.load()
        .then((data) => {
          this.guests = data
        }).then(() => {
          this.calcTotalTickets()
        })
				},
        openAddGuestModal(){
          this.showAddGuestModal = true
        },
        closeAddGuestModal(){
          this.showAddGuestModal = false
        },
        deleteGuest(index){
          this.guests.splice(index, 1)
          const guestRepo = new GuestRepository()
					guestRepo.save(this.guests)
          this.calcTotalTickets()
        },
        addNewGuest(guest){
          if(this.currentTotalOfTickets + parseInt(guest.tickets) > this.maxTotalOfTickets){
            alert('Not have more than 20 Guests')
            return
          }
          if(guest.email === '' || guest.email === undefined){
            alert('Email can not be blank')
            return
          }
          else{
          this.guests.push(guest)
          const guestRepo = new GuestRepository()
					guestRepo.save(this.guests)
          this.calcTotalTickets()
          }

        },
        updateGuest(guest, index){
          if(this.currentTotalOfTickets + parseInt(guest.tickets) - this.editGuest.tickets > this.maxTotalOfTickets){
            alert('Not have more than 20 Guests')
            return
          }
          if(guest.email === '' || guest.email === undefined){
            alert('Email can not be blank')
            return
          }
          this.guests.splice(index, 1, guest)
          const guestRepo = new GuestRepository()
					guestRepo.save(this.guests)
          this.calcTotalTickets()
        },
        openEditGuestModal(guest, index){
          this.editGuest = {...guest}
          this.editGuestIndex = index
          this.showEditGuestModal = true
        },
        closeEditGuestModal(){
          this.showEditGuestModal = false
        }
			},
      created() {
        this.getGuests()
      }
    }

  </script>
<style>
  .flex-wrapper {
    display: flex;
    gap: 2rem;
    align-items: center;
    justify-content: center;
  }
  .grid-wrapper {
    display: grid;
    gap: 1rem;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    width: 1000px;
  }
  .padding-10{
    padding: 10px;
  }
  div {
    text-align: center;
  }
  .add-guest {
    background-color: darkcyan;
    border-radius: 10px;
    width: 30%;
    &:hover {
      background-color: rgb(5, 114, 114);
    }
  }
  .flex-space-between {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>