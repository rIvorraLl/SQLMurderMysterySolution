# SQLMurderMysterySolution
My solution to The SQL Murder Mystery

```sql
SELECT * from crime_scene_report
  WHERE date='20180115'
  AND type='murder'
  AND city ='SQL City';
```
date: 20180115

type: murder

description: Security footage shows that there were 2 witnesses. The first witness lives at the last house on "Northwestern Dr". The second witness, named Annabel, lives somewhere on "Franklin Ave".

city: SQL City

```sql
SELECT * from person
 	where address_street_name = "Northwestern Dr"
	order by address_number desc
	limit 1;
```
id	  name	          license_id	  address_number	 address_street_name	ssn

14887	Morty Schapiro	118009	      4919	           Northwestern Dr	    111564949

```sql
SELECT * from person
 	where name like'%Annabel%'
	and address_street_name='Franklin Ave';
```

id	  name	          license_id	address_number	address_street_name	 ssn

16371	Annabel Miller	490173	    103	            Franklin Ave	       318771143

```sql
SELECT transcript FROM interview
	WHERE person_id = 14887
	or person_id = 16371;
```
transcript

I heard a gunshot and then saw a man run out. He had a "Get Fit Now Gym" bag. The membership number on the bag started with "48Z". Only gold members have those bags. The man got into a car with a plate that included "H42W".

I saw the murder happen, and I recognized the killer from my gym when I was working out last week on January the 9th.

```sql
SELECT p.id,
  p.name,
  gfc.check_in_date,
  gfm.membership_status,
  d.plate_number
	FROM get_fit_now_member gfm,
    get_fit_now_check_in gfc,
    person p,
    drivers_license d
		  WHERE gfm.membership_status="gold"
		    AND gfc.check_in_date="20180109"
		    AND p.id = gfm.person_id
		    AND d.plate_number like "%H42W%"
		    AND d.id = p.license_id;
```
id	name	check_in_date	membership_status	plate_number

67318	Jeremy Bowers	20180109	gold	0H42W2

Congrats, you found the murderer! But wait, there's more... If you think you're up for a challenge, try querying the interview transcript of the murderer to find the real villain behind this crime. If you feel especially confident in your SQL skills, try to complete this final step with no more than 2 queries. Use this same INSERT statement with your new suspect to check your answer.

```php
SELECT * FROM interview
  WHERE person_id='67318';
```
person_id	transcript

67318	I was hired by a woman with a lot of money. I don't know her name but I know she's around 5'5" (65") or 5'7" (67"). She has red hair and she drives a Tesla Model S. I know that she attended the SQL Symphony Concert 3 times in December 2017.

```sql
SELECT fb.person_id, p.name from
	facebook_event_checkin fb,
	person p,
	drivers_license d
		WHERE fb.event_name='SQL Symphony Concert'
		AND fb.person_id = p.id
		AND d.id=p.license_id
		AND d.gender = 'female'
		AND d.car_make = 'Tesla'
		AND d.car_model = 'Model S'
    AND d.hair_color = 'red'
    AND d.height > '64'
		AND d.height < '68';
  ```
  person_id	name
99716	Miranda Priestly

Congrats, you found the brains behind the murder! Everyone in SQL City hails you as the greatest SQL detective of all time. Time to break out the champagne!
