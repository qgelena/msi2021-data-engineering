# Data Engineer Internship (MacPaw Summer Internship 2021)
Write an application that will extract files from the public AWS S3 bucket, transform them, and load results to the database. The bucket contains JSON files, representing data. Parse JSON and write corresponding content to the database. A list of all possible files in the bucket is available in `files_list.data` file.

**S3 bucket specification**</br>
<table>
  <tr>
    <td>URL</td>
    <td>https://data-engineering-interns.macpaw.io</td>
  </tr>
  <tr>
    <td>Bucket name</td>
    <td>data-engineering-interns.macpaw.io</td>
  </tr>
  <tr>
    <td>Files list object key</td>
    <td>files_list.data</td>
  </tr>
</table>

New files will appear in the bucket periodically, and old ones could be deleted. 
Keep in mind that you have to process only those files you haven't processed yet. 
A list of all files (`files_list.data`) will be updated automatically when a new file arrives. This file is just a newline delimited text file, having one file name on each row.

JSON files are in the following format:

```
[
   {
      "type": "song",
      "data": {
         "artist_name": "Massive Attack",
         "title": "Karmacoma",
         "year": 1994,
         "release": "Protection"
      }
   },
   {
      "type": "movie",
      "data": {
         "original_title:": "Toy Story",
         "original_language": "en",
         "budget": 30000000,
         "is_adult": false,
         "release_date": "1995-10-30"
      }
   },
   
   ...
   
   {
      "type": "app",
      "data": {
         "name": "Geometry Dash",
         "genre": "Games",
         "version": "2.10",
         "rating": 5.0,
         "size_bytes": 83931136
      }
   }
]
```

Each JSON file will contain a list (any length) of objects with a specific type. Note that there might be other types of data in JSON, but only `song`, `movie` and `app` are needed for you. <br>

Your app should read the JSON, process it according to `type`, and write data to the database of your choice. 
Save data to the following tables according to data `type`:

####  **songs** 
| column name | column type|
|----|:----:|
|artist_name|varchar|
|title|varchar|
|year|integer|
|release|varchar|
|ingestion_time|datetime|

Fill `ingestion_time` with a datetime indicating when this record was processed.

 #### **movies** 
 
| column name | column type|
|----|:----:|
|original_title|varchar |
|original_language| varhcar|
|budget|integer|
|is_adult|boolean|
|release_date|date|
|original_title_normalized|varcahar|

Fill `original_title_normalized` with value of `original_title` where any non-letter and non-number characters are removed and spaces replaced with underscore _ (e.g. Star Wars: The Force Awakens -> star_wars_the_force_awakens).
#### **apps**

| column name | column type|
|----|:----:|
|name|varchar|
|genre|varchar|
|rating|float|
|version|varchar|
|size_bytes|integer|
|is_awesome|boolean|

Fill `is_awesome` with a boolean value indicating if an app is awesome or not (feel free to choose any criteria indicating if an app is awesome).

------
Doing this task, feel free to use any RDBMS, programming language (Python is preferred), shared libraries, and frameworks. Pay attention to code flexibility, architecture, and code cleanliness. Wrap your solution into a container environment.

Please, provide us a URL to your repository with the task solution into the registration form as a result of this test task.
