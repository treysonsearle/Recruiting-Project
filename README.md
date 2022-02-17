# iScout Recruiting Project

This is a small coding project for KPA EHS software developer candidates. It is
a pre-configured website using [Vue](https://vuejs.org/v2/guide/).
You'll create a simple page then submit a pull-request when you're ready.


## Getting Started

First, make sure you can run this on your machine. Node 12.X or later
is recommended.

```
git clone git@github.com:HazardScout/iScout-Recruiting-Project.git iscout
cd iscout
npm install
npm run dev
```

You should now be able to view the application at: http://localhost:8080

The project should automatically hot-reload as you make changes.


## What Matters?

Styles/colors are not important. Here's what is:

 * Well-organized code
 * Well-named variables, functions, arguments, etc
 * Clean & easy user-interfaces


## Project Requirements

Nyan Cat will be performing at your house. You can only fit 20 people
so this app will keep track of who is coming.

Here are the features:

   * For each guest, you'll track email address and number of tickets
   * You don't need to track anything else (like name, etc)
   * Show a table of all the guests
   * There should be a way to add, edit, and delete guests
   * When editing a guest, the user should be able to cancel
   * Show the total number of guests somewhere

For your convenience, use the Guest Repository to load/save data. For
simplicity, do not worry about error handling:

    const GuestRepository = require('../guest-repository');
    const repo = new GuestRepository();

    // Fetch guests
    const guests = await repo.load();
    > [ { email: 'foo@bar.com', tickets: 3 }, ...]

    // Save guests
    guests.splice(0, 1);
    await repo.save(guests);

    // Reset (if desired)
    await repo.reset();


## Extras

Don't spend a ton of time on this project, but here are some bonus
elements if you're feeling crazy.

   * Feel free to pull in libraries like Bootstrap or Vuetify. But
     don't spend too much time on styles.
   * Try using a modal dialog for the new/edit functionality.



## Submitting Your Project

Once you're ready, submit a pull request of your code:

https://github.com/HazardScout/iScout-Recruiting-Project/pulls

We should automatically get a notification from GitHub, but feel
free to message us when you've submitted the PR.
