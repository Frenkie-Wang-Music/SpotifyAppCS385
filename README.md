# Steps to run the project:
The first time you clone the project:

`npm install`

Run the project on localhost:

`cd frontend`

`npm run dev`

### The project is deployed at:
https://spotify-app-cs-385.vercel.app/

# Clean the data
1) Create new Table with only 4 Columns
```sql
CREATE TABLE spotify_2024 AS
SELECT track, artist, release, streams
FROM origin_data; 
```

2) Delete old Table
```sql
DROP TABLE origin_data;
```

3) Data cleaning 
```sql
DELETE FROM spotify_2024
WHERE 
    TRIM(track) = '' OR track LIKE '%???%'
 OR TRIM(artist) = '' OR artist LIKE '%???%'
 OR TRIM(release) = '' OR release LIKE '%???%'
 OR TRIM(streams) = '' OR streams LIKE '%???%';
   ```

4) Export new Excel and convert into JSON 