I am planning with you for app:api database structure

with this 3 roles, We gonna making 3 different app (For android and IOS)
App Names: 
1. AF Rider (role_id: 1)
2. AF Driver (role_id: 2)
3. AF Fleet  (role_id: 3)

I describing single focusing point(vechile assignment for driver):
First logics: 
- A ride can register as a driver/VehicleOwner with same phone number
- A driver can register as a rider/VehicleOwner with same phone number
- A VehicleOwner can register as a rider/driver with same phone number

1. Rider flow simple (no dissuccstion about this right now)
2. VehicleOwner will be add cars with cars related papers, and he will set rental price for each car(daily, weekly, and monthly). 
3. After complete driver registration and KYC(Know Your Customer), then he can be rent/tag one/multiple vehicle, thats alreay added by vehicleOwner's. After rent/tag if dirver want to cancel, cancel request will be send, and it will approve VehicleOwner




in app:admin er moddhe 
/settings/terms-and-conditions/rider 
/settings/terms-and-conditions/driver 

add kore dynamicly data add kore app a 





Screen	Status	Note
1. Dashboard (06)	⚠️ Partial	Toggle works, map done — but missing: real stats from API, socket joins drivers:available on online toggle, PATCH /driver-profiles/me/status API call, "View All" → Earnings nav, bottom sheet with stats row
2. Earnings (07b)	⚠️ Placeholder	Today/Week/Month tabs, real API data, trip list
3. Profile (07c)	⚠️ Partial	Missing stats card (rides/rating/earnings), KYC status dot, all menu items wired
Edit Profile (07d)	❌	Avatar picker + upload, name/email save
Notifications (07c-b)	❌	4 preference toggles
Help & Support (07c-c)	❌	FAQ accordion + contact buttons
Terms & Conditions (07c-d)	❌	Static scrollable content