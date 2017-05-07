**POLL - 1**

1.	SELECT count(*) FROM congress_members
inner join votes on congress_members.id = votes.politician_id
where politician_id = '524'

2.	SELECT * FROM congress_members
inner join votes on congress_members.id = votes.politician_id
where politician_id = '524'

3.	SELECT count(votes.id) FROM congress_members
inner join votes on congress_members.id = votes.politician_id
where name like "%Erik Paulsen"

4.	SELECT name,party,location,grade_1996,grade_current,years_in_congress,dw1_score,COUNT(congress_members.id) as number_of_votes  FROM congress_members
inner join votes on congress_members.id = votes.politician_id
group by name,party,location,grade_1996,grade_current,years_in_congress,dw1_score
ORDER BY number_of_votes desc
LIMIT 3

5.	SELECT name,party,location,grade_1996,grade_current,years_in_congress,dw1_score,COUNT(congress_members.id) as number_of_votes  FROM congress_members
inner join votes on congress_members.id = votes.politician_id
group by name,party,location,grade_1996,grade_current,years_in_congress,dw1_score 
ORDER BY number_of_votes asc
LIMIT 3
