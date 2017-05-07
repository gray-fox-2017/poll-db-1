<!-- Release 1  -->

<!-- 1. Hitung jumlah vote untuk Sen. Olympia Snowe yang memiliki id 524. -->
## select count(id) from votes where politician_id =524;
<!-- 2. Sekarang lakukan JOIN tanpa menggunakan id `524`. Query kedua tabel votes dan congress_members. -->
## select*from congress_members inner join votes on congress_members.id = votes.politician_id where congress_members.id=524;
<!-- 3. Sekarang gimana dengan representative Erik Paulsen? Berapa banyak vote yang dia dapatkan? -->
## select id, name from congress_members where name like '%erik paulsen%'; select count(id) from votes where politician_id=339;
<!-- 4. Buatlah daftar peserta Congress yang mendapatkan vote terbanyak. Jangan sertakan field `created_at` dan `updated_at`. -->
## select name, party, location, grade_1996, grade_current, years_in_congress, dw1_score, count(votes.voter_id) as number_of_votes from congress_members join votes where congress_members.id = votes.politician_id group by congress_members.id order by number_of_votes desc limit 3;
<!-- 5. Sekarang buatlah sebuah daftar semua anggota Congress yang setidaknya mendapatkan beberapa vote dalam urutan dari yang paling sedikit. Dan juga jangan sertakan field-field yang memiliki tipe date. -->
## select name, party, location, grade_1996, grade_current, years_in_congress, dw1_score, count(votes.voter_id) as number_of_votes from congress_members join votes where congress_members.id = votes.politician_id group by congress_members.id order by number_of_votes asc limit 3;
<!-- Release 2  -->

<!-- 1. Siapa anggota Congress yang mendapatkan vote terbanyak? List nama mereka dan jumlah vote-nya. Siapa saja yang memilih politisi tersebut? List nama mereka, dan jenis kelamin mereka. -->
## SELECT v.first_name,v.last_name,vs.politician_id, x.total_votes FROM voters AS v JOIN votes AS vs on v.id = vs.voter_id JOIN ( SELECT count(politician_id) as total_votes, politician_id FROM votes GROUP BY politician_id ORDER BY total_votes DESC ) x on vs.politician_id = x.politician_id ORDER BY x.politician_id ASC
<!-- 2. Berapa banyak vote yang diterima anggota Congress yang memiliki grade di bawah 9 (gunakan field `grade_current`)? Ambil nama, lokasi, grade_current dan jumlah vote. -->
## SELECT v.politician_id, cm.name, cm.location,cm.grade_current, count(v.politician_id) as total_votes FROM votes AS v JOIN congress_members AS cm ON v.politician_id = cm.id WHERE cm.grade_current < 9 GROUP BY v.politician_id, cm.name, cm.location,cm.grade_current ORDER BY cm.grade_current DESC
<!-- 3. Apa saja 10 negara bagian yang memiliki voters terbanyak? List semua orang yang melakukan vote di negara bagian yang paling populer. (Akan menjadi daftar yang panjang, kamu bisa gunakan hasil dari query pertama untuk menyederhanakan query berikut ini.) -->

<!-- 4. List orang-orang yang vote lebih dari dua kali. Harusnya mereka hanya bisa vote untuk posisi Senator dan satu lagi untuk wakil. Wow, kita dapat si tukang curang! Segera laporkan ke KPK!! -->

<!-- 5. Apakah ada orang yang melakukan vote kepada politisi yang sama dua kali? Siapa namanya dan siapa nama politisinya? -->
## SELECT vrs.first_name, vrs.last_name, vrs.gender, curang.total_votes, cm.name FROM voters AS vrs JOIN ( SELECT count(politician_id) as total_votes, voter_id, politician_id FROM votes GROUP BY voter_id, politician_id HAVING total_votes = 2 ) AS curang on curang.voter_id = vrs.id JOIN congress_members AS cm ON cm.id = curang.politician_id ORDER BY cm.name
