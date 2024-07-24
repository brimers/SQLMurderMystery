https://mystery.knightlab.com/

/*
crime was a ​murder​ that occurred sometime on 
​Jan.15, 2018​ and that it took place in ​SQL Cit
*/

select * from crime_scene_report
where city = "SQL City" and date = "20180115" and type = "murder"
order by date asc  

/*
20180115	murder	Security footage shows that there were 2 witnesses. The first witness lives at the last house on "Northwestern Dr". The second witness, named Annabel, lives somewhere on "Franklin Ave".	SQL City
*/

select name, MAX(address_number), address_street_name
from person
where address_street_name = "Northwestern Dr"

/*
Morty Schapiro	4919	Northwestern Dr
*/

select name, address_number, address_street_name
from person
where name like "%Annabel%" and address_street_name = "Franklin Ave"

/*
Annabel Miller	103	Franklin Ave
*/

select name, transcript
from get_fit_now_member
inner join interview on get_fit_now_member.person_id = interview.person_id
where name = "Annabel Miller"

/*
Annabel Miller	I saw the murder happen, and I recognized the killer from my gym when I was working out last week on January the 9th.
*/

select id, person_id, name, membership_id, check_in_date, check_in_time, check_out_time
from get_fit_now_member m
inner join get_fit_now_check_in  c
on m.id = c.membership_id
where check_in_date = "20180109"

select id, person_id, name, membership_id, check_in_date, check_in_time, check_out_time
from get_fit_now_member m
inner join get_fit_now_check_in  c
on m.id = c.membership_id
where check_in_date = "20180109" and (check_in_time <= 1600 and check_out_time >= 1700)

/*
id	person_id	name	membership_id	check_in_date	check_in_time	check_out_time
48Z7A	28819	Joe Germuska	48Z7A	20180109	1600	1730
48Z55	67318	Jeremy Bowers	48Z55	20180109	1530	1700
90081	16371	Annabel Miller	90081	20180109	1600	1700
*/

select name, transcript
from get_fit_now_member
inner join interview on get_fit_now_member.person_id = interview.person_id
where name = "Joe Germuska" or name = "Jeremy Bowers"

/*
name	transcript
Jeremy Bowers	I was hired by a woman with a lot of money. I don't know her name but I know she's around 5'5" (65") or 5'7" (67"). She has red hair and she drives a Tesla Model S. I know that she attended the SQL Symphony Concert 3 times in December 2017. 
*/

select p.id, p.name, d.height, d.car_make, d.car_model, d.height, d.hair_color, d.car_make, d.car_model, f.event_name, f.date
from ((person p
inner join drivers_license d on p.license_id = d.id)
inner join facebook_event_checkin f on p.id = person_id)
where
65 <= d.height <= 67 AND
d.hair_color = "red" AND
d.car_make = "Tesla" AND
d.car_model = "Model S" AND
f.event_name = "SQL Symphony Concert" AND
date like "201712%"
group by p.name
having count(f.event_name = "SQL Symphony Concert") = 3

/*
id	name	height	car_make	car_model	height	hair_color	car_make	car_model	event_name	date
99716	Miranda Priestly	66	Tesla	Model S	66	red	Tesla	Model S	SQL Symphony Concert	20171206
99716	Miranda Priestly	66	Tesla	Model S	66	red	Tesla	Model S	SQL Symphony Concert	20171212
99716	Miranda Priestly	66	Tesla	Model S	66	red	Tesla	Model S	SQL Symphony Concert	20171229
*/


              
