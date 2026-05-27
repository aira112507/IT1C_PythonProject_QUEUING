# Queue System - Explained in Simple Terms

This document breaks down how the queue system works. It's basically like a ticket system at the bank or DMV—people join, get served, and then they're done!

---

## The Basics

Here are the three states a customer can be in:

- `WAITING_STATUS = "waiting"` — They're in line, waiting for their turn
- `SERVING_STATUS = "serving"` — They're being helped right now
- `DONE_STATUS = "done"` — They're finished and done
- `TICKET_PREFIX = "Q"` — All tickets start with the letter "Q" (like Q001, Q002, etc.)
- `TICKET_NUMBER_WIDTH = 3` — Tickets are padded to 3 digits

---

## What the Database Can Do

The system needs a way to store and retrieve customer info. Here are the things we ask the database to do:

- **Add a customer** to the queue with their name and status
- **Find the first person** waiting or being served
- **Check if anyone** is in a particular status
- **Change someone's status** (like from waiting to serving)
- **Show me** all the people waiting
- **Tell me** who's currently being served
- **Show me** the history of completed customers
- **Count how many** people are waiting
- **Get statistics** about all status groups
- **Find a customer** by their ticket number
- **Tell me** how many people are ahead in line
- **Look up** a customer's ticket and name
- **Remove** a customer record
- **Count everything** in the database
- **Wipe the slate clean** and delete all records
- **Check if** someone with the same name is already waiting

---

## Checking That Input Makes Sense

Before we do anything, we need to make sure the data is good:

```
When someone gives us a name:
    - Is it actually text? (not a number or something weird)
    - Remove any extra spaces from the start/end
    - Is it empty? Nope, not allowed!
    - If all checks pass, use the cleaned-up name

When someone gives us a ticket number:
    - Is it text?
    - Clean up any extra spaces
    - Can't be empty!
    - If good, we're ready to use it

When someone gives us a customer ID number:
    - Must actually be a whole number (not text, not true/false)
    - Can't be zero or negative—must be a real ID number
    - If it checks out, we're good to go
```

---

## Joining the Queue

Here's what happens when a new customer arrives:

```
When a customer wants to join the queue:
    1. Clean up their name (remove spaces, check it's valid)
    2. If we don't allow duplicates, check if they're already waiting
    3. If they are already there, tell them "sorry, you're already in line!"
    4. If not, give them a ticket number and mark them as "waiting"
    5. Give them their ticket so they know where they are in line
```

---

## Calling the Next Customer

Time to serve someone!

```
When we call the next customer:
    1. First, check if someone is already being served
    2. If yes, tell the staff member "finish with this customer first!"
    3. If no one is being served, find the first person waiting
    4. If no one's waiting either, say "the queue is empty"
    5. When you find them, change their status from "waiting" to "serving"
    6. Tell the staff who they are and their ticket number
```

---

## Marking a Customer as Done

When the service is finished:

```
When a customer is finished:
    1. Find whoever is currently being served
    2. If no one is being served, there's nothing to do—say "no one being served"
    3. When you find them, change their status from "serving" to "done"
    4. Log their info so we know they were here
```

---

## Looking Up Information

These are quick ways to check the queue:

```
Show me everyone waiting right now
Show me who's currently being served
Show me the history of everyone who was served today
Show me absolutely everyone (waiting, serving, and done)
Tell me the total number of people waiting
```

---

## Getting the Big Picture

Here's how we create a summary of what's happening:

```
When we want statistics:
    1. Create a counter that starts at 0 for each status
    2. Go through all the customers in the database
    3. Add them up by their status (waiting, serving, done)
    4. Calculate the total of everyone
    5. Return a nice summary showing all the numbers
```

---

## Where's My Spot in Line?

If a customer wants to know their position:

```
When someone asks "where am I in line?":
    1. Take their ticket number and look it up
    2. Find their customer ID
    3. If they're not in the system, they're not in line (position = 0)
    4. If they are there, count how many people are ahead of them
    5. Tell them their position
```

---

## Removing Someone from the Queue

Maybe they changed their mind or we need to remove a record:

```
When we need to delete a customer:
    1. Make sure the ID number is valid
    2. Look them up in the database
    3. If they don't exist, say "I can't find them"
    4. If they do exist, remove them
    5. Tell the staff what we removed
```

---

## Starting Fresh

When we need to clear everything out:

```
When we want to wipe the database clean:
    1. Count how many customers are in the system
    2. If there are any, delete them all
    3. Return how many we deleted (so staff knows something happened)
```

---

## What the System Exposes to Users

These are all the commands the staff can use:

- Join queue with a name
- Call the next customer
- Mark someone as done
- View waiting customers
- View current customer being served
- View completed customers
- View everyone (all statuses)
- Count how many are waiting
- Get statistics/summary
- Check position in line
- Delete a customer record
- Clear all records
