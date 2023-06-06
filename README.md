# SQLMurderMysterySolution
My solution to [The SQL Murder Mystery](https://mystery.knightlab.com/)

```sql
SELECT * from crime_scene_report
  WHERE date='20180115'
  AND type='murder'
  AND city ='SQL City';
```

```sql
SELECT * from person
 	where address_street_name = "Northwestern Dr"
	order by address_number desc
	limit 1;
```

```sql
SELECT * from person
 	where name like'%Annabel%'
	and address_street_name='Franklin Ave';
```

```sql
SELECT transcript FROM interview
	WHERE person_id = 14887
	or person_id = 16371;
```

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

```php
SELECT * FROM interview
  WHERE person_id='67318';
```

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
