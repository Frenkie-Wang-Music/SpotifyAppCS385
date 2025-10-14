# Steps to run the project:
The first time you clone the project:

`npm install`

Run the project on localhost:

`cd frontend`

`npm run dev`

### The project is deployed at:
https://spotify-app-cs-385.vercel.app/

# Clean the data

1) Change Column Name
```sql
ALTER TABLE origin_data RENAME COLUMN Track TO track;
ALTER TABLE origin_data RENAME COLUMN Artist TO artist;
ALTER TABLE origin_data RENAME COLUMN `Spotify Streams` TO streams;
FROM origin_data; 
```

2) Create a new Column for Release Year
```sql
ALTER TABLE origin_data ADD COLUMN release INT;
```

```sql
UPDATE origin_data
SET release = YEAR(STR_TO_DATE(`Release Date` , '%d/%m/%Y'));
```

3) Create new Table with only 4 Columns
```sql
CREATE TABLE spotify_2024 AS
SELECT track, artist, release, streams
FROM origin_data; 
```

4) Delete old Table
```sql
DROP TABLE origin_data;
```

5) Data cleaning 
```sql
DELETE FROM spotify_2024
WHERE 
    TRIM(track) = '' OR track LIKE '%???%'
 OR TRIM(artist) = '' OR artist LIKE '%???%'
 OR TRIM(release) = '' OR release LIKE '%???%'
 OR TRIM(streams) = '' OR streams LIKE '%???%';
   ```

6) Export new Excel and convert into JSON 