# Project Setup

1. Clone the repository to your local machine.
2. Install the project dependencies using `npm install or yarn`.
3. Set up your environment variables by creating a `.env` file in the root directory(see env example).
4. Then you need your supabase url and key which you will find in supabase dashboard.
5. To you will need to create some tables run these SQL Command which are generated by supabase.

Bookings table should be ordered to last beacuse of foreign key constraint.

 Settings Table

```shell
create table
  public.settings (
    id bigint generated by default as identity,
    created_at timestamp with time zone not null default now(),
    "minBookingLength" smallint null,
    "maxBookingLength" smallint null,
    "maxGuestsPerBooking" smallint null,
    "breakfastPrice" real null,
    constraint settings_pkey primary key (id)
  ) tablespace pg_default;
```
 Guests Table

```shell
create table
  public.guests (
    id bigint generated by default as identity,
    created_at timestamp with time zone not null default now(),
    "fullName" text null,
    email text null,
    nationality text null,
    "countryFlag" text null,
    "nationalID" text null,
    constraint guests_pkey primary key (id)
  ) tablespace pg_default;
```
Cabins Table

```shell
create table
  public.cabins (
    id bigint generated by default as identity,
    created_at timestamp with time zone not null default now(),
    name text null,
    "maxCapacity" smallint null,
    "regularPrice" smallint null,
    discount smallint null,
    description text null,
    image text null,
    constraint tables_pkey primary key (id)
  ) tablespace pg_default;
```
Bookings Table

```shell
create table
  public.bookings (
    id bigint generated by default as identity,
    created_at timestamp with time zone not null default now(),
    "startDate" timestamp without time zone null,
    "endDate" timestamp without time zone null,
    "numNights" smallint null,
    "numGuests" smallint null,
    "cabinPrice" real null,
    "extraPrice" real null,
    "totalPrice" real null,
    status text null,
    "hasBreakfast" boolean null,
    "isPaid" boolean null,
    observations text null,
    "cabinId" bigint null,
    "guestId" bigint null,
    constraint bookings_pkey primary key (id),
    constraint bookings_cabinId_fkey foreign key ("cabinId") references cabins (id),
    constraint bookings_guestId_fkey foreign key ("guestId") references guests (id)
  ) tablespace pg_default;
```

   
6. After tables are succesfully created you can seed data using Uploader component which is available in data directory. 
