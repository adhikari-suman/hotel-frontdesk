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
