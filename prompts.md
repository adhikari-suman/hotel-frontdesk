## 1. Initial prompt

```
I want you to build me a 10 design for a hotel frontdesk SaaS app.

The web app is for a Hotel Frontdesk. It has the folowing features:

1. User mangement feature

We have two roles mainly: receptionist and admin.

- admin can create users and view call logs; also add, update and delete rooms. He/she can also add promotion codes.
- specialist can make a booking, rebook a booking, checkin, checkout a booking, and cancel a booking, or add extras like dinner, arrival pickup and breakfast to the booking as extra offer.

2. Rooms

Only admin can add update or delete a room.

Room has:

- a type: deluxe, twin double, family suite, queen.
- price
- count

3. Promotion code

- has an id
- a code type for identity like summer2020
- a name or title like "Summer 2020"
- a date range, mandatory.
- count if any.


Only admin can add a promotion code. Receptionist can only use it.


Follow this procedure:

Generate a long, random alphanumeric string using a shell script.

Define the creative direction (color scheme, layout, typography, etc.) based on the string. Look beyond the surface for subpatterns, special numbers, anything that inspires you.

Use your judgment to bring this direction to life and make it look great.

Don’t reveal the string in the design. It’s only for your inspiration.

Generate 6-10 designs based on images for me.
```

## 2. Change in prompts

```
I want you to build me 10 different designs for a hotel frontdesk SaaS app.

Each design should include these and incorporate the screens that it already mentions.

The web app is for a Hotel Frontdesk. It has the folowing features:

1. User mangement feature

We have two roles mainly: receptionist and admin.

- admin can create other users. also add, update and delete rooms. He/she can also add promotion codes.
- specialist can make a booking, rebook a booking, checkin, checkout a booking, and cancel a booking, or add extras like dinner, arrival pickup and breakfast to the booking as extra offer.

2. Rooms

Only admin can add update or delete a room.

Room has:

- a type: deluxe, twin double, family suite, queen.
- price
- count

3. Promotion code

- has an id
- a code type for identity like summer2020
- a name or title like "Summer 2020"
- a date range, mandatory.
- count if any.


Only admin can add a promotion code. Receptionist can only use it.


Follow this procedure:

Generate a long, random alphanumeric string using a shell script.

Define the creative direction (color scheme, layout, typography, etc.) based on the string. Look beyond the surface for subpatterns, special numbers, anything that inspires you.

Use your judgment to bring this direction to life and make it look great.

Don’t reveal the string in the design. It’s only for your inspiration.

Generate 6-10 DIFFERENT designs based on images for me. Keep the current design in design-1 as one of it and complete it if it is incomplete. And make the other 9 different design for us.
```
## 3. With unique keys for the prompts

### 3.1 Generate seed.json

Going to generate the seed string seprately first.

```
Generate long, random alphanumeric string using a shell script in individual agents totaling 15 and add it to seed.json each with key: [id] and value as seed value. Seed should be 256 characters long.
```

### 3.2 Design prompt

```
I want you to build me a 15 different designs for a hotel frontdesk SaaS app.

Each design should include these and incorporate the screens that it already mentions.

The web app is for a Hotel Frontdesk. It has the folowing features:

1. User mangement feature

We have two roles mainly: receptionist and admin.

- admin can create other users. also add, update and delete rooms. He/she can also add promotion codes.
- specialist can make a booking, rebook a booking, checkin, checkout a booking, and cancel a booking, or add extras like dinner, arrival pickup and breakfast to the booking as extra offer.

2. Rooms

Only admin can add update or delete a room.

Room has:

- a type: deluxe, twin double, family suite, queen.
- price
- count

3. Promotion code

- has an id
- a code type for identity like summer2020
- a name or title like "Summer 2020"
- a date range, mandatory.
- count if any.


Only admin can add a promotion code. Receptionist can only use it.


Follow this procedure:

1. Create 15 different design agents with its id ranging from 1-15.

2. For each design agent from 1-15 as id, use the corresponding alphanumeric seed string from seed.json. It has the corresponding id in it. 

3. Define the creative direction (color scheme, layout, typography, etc.) based on the string. Look beyond the surface for subpatterns, special numbers, anything that inspires you. Make sure you are using the correct id for the agent and using the corresponding seed from the agent.

4. Before working on it, validate no other agent is using the same seed id string.

5. Use your judgment to bring this direction to life and make it look great.

6. Don’t reveal the string in the design. It’s only for your inspiration.

```