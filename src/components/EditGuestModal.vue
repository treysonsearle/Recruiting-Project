<template>
    <div class="overlay">
      <div class="modal padding-20">
        <div class="flex-space-between">
          <h2>Edit Guest</h2>
          <svg v-on:click="closeModal()" xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 384 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M342.6 150.6c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0L192 210.7 86.6 105.4c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L146.7 256 41.4 361.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0L192 301.3 297.4 406.6c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3L237.3 256 342.6 150.6z"/></svg>
        </div>
        <form class="flex-space-between">
          <div class="flex-column">
            <label>Email</label>
            <input v-model="guest.email"/>
          </div>
          <div class="flex-column">
            <label>Tickets</label>
            <input 
              type="number"
              :max="maxTotalOfTickets - currentTotalOfTickets"
              min="0"
              v-model="guest.tickets"
            /> 
          </div>
        </form>
        <div 
          class="flex-space-between padding-20 add"
          v-on:click="editGuest()"
        >
          <h2>Edit Guest</h2>
          <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M96 128a128 128 0 1 1 256 0A128 128 0 1 1 96 128zM0 482.3C0 383.8 79.8 304 178.3 304h91.4C368.2 304 448 383.8 448 482.3c0 16.4-13.3 29.7-29.7 29.7H29.7C13.3 512 0 498.7 0 482.3zM504 312V248H440c-13.3 0-24-10.7-24-24s10.7-24 24-24h64V136c0-13.3 10.7-24 24-24s24 10.7 24 24v64h64c13.3 0 24 10.7 24 24s-10.7 24-24 24H552v64c0 13.3-10.7 24-24 24s-24-10.7-24-24z"/></svg>
      </div>
    </div>
  </div>

  </template>
  
  <script>
    export default {
      props: {
        currentTotalOfTickets: {
          type: Number,
          require: true
        },
        maxTotalOfTickets: {
          type: Number,
          required: true
        },
        currentGuest: {
          type: Object,
          required: true
        },
        guestIndex: {
          type: Number,
          required: true
        }
      },
      emits: ['close', 'edit'],
      methods: {
        closeModal() {
          this.$emit('close')
        },
        editGuest() {
          this.$emit('edit', {...this.guest}, this.guestIndex)
          this.$emit('close')
        }
      },
      data: () => {
        return {
          guest: {
            email: '',
            tickets: null
          }
        };
      },
      created() {
        this.guest = { ...this.currentGuest }
      }
    }
  </script>
  <style>
  .flex-space-between {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(.4, .4, .4, .2);
  }
  .modal {
    z-index: 1;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 450px;
    background-color: white;
    border-radius: 10px;
  }
  .padding-20{
    padding: 20px;
  }
  .flex-column {
    display: flex;
    gap: .5rem;
    flex-direction: column;
    align-items: flex-start;
  }
  .padding-10{
    padding: 10px;
  }
  input {
    height: 20px;
  }
  div {
    text-align: center;
  }
  .add {
    margin: 20px auto auto;
    background-color: darkcyan;
    border-radius: 10px;
    width: 90%;
    &:hover {
      background-color: rgb(5, 114, 114);
    }
  }
</style>