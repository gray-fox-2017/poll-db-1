1. SELECT COUNT(id) FROM votes WHERE politician_id = 524;

2. SELECT * FROM congress_members JOIN votes ON congress_members.id = votes.politician_id WHERE congress_members.name = 'Sen. Olympia Snowe';

3. SELECT COUNT(id) FROM votes WHERE politician_id = 339;

4. SELECT congress_members.name, congress_members.party, congress_members.location, congress_members.grade_1996, congress_members.grade_current,    congress_members.years_in_congress, congress_members.dw1_score, COUNT(votes.id) AS 'number_of_votes' FROM congress_members JOIN votes ON congress_members.id = votes.politician_id GROUP BY votes.politician_id ORDER BY COUNT(votes.id) DESC LIMIT 3;

5. SELECT congress_members.name, congress_members.party, congress_members.location, congress_members.grade_1996, congress_members.grade_current, congress_members.years_in_congress, congress_members.dw1_score, COUNT(votes.id) AS 'number_of_votes' FROM congress_members JOIN votes ON congress_members.id = votes.politician_id GROUP BY votes.politician_id ORDER BY COUNT(votes.id) ASC LIMIT 3;