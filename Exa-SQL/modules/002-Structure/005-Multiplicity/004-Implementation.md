
## One to Many Relationship

A good example of a one to many relationship could be an `albums` and `songs` table. 1 album can have many songs however 1 song cannot be on many albums (excluding "Greatest Hits" albums). This is a one-to-many relationship. As stated in the previous section, to implement a one-to-many relationship we need to have a foreign key in the "many" table that references the "one" table. In our case, the many is the `songs` table and the one is the `albums` table. 


***albums table***

|album_id | album_name | 
| ------- | ---------- |
| 1 | 'Thriller' |
| 2 | 'Abbey Road'|

***songs table***

|song_id |song_name |album_fk |
| ------ | -------- | ------- |
| 1 | 'Billie Jean' | 1 |
| 2 | 'Beat it' | 1 | 
| 3 | 'Come Together' | 2 |

## Many to One Relationship

The only difference between a one-to-many relationship and a many-to-one relationship is perspective. People generally refer to a relationship as a many-to-one because they are thinking in relation to the "many" table. However, many-to-one and One-to-many are actually the same thing. Please refer to the one-to-many example on how to implement this.

## Many to Many Relationship

One example of a many-to-many relationship could be `doctors` table and a `patients` table. 1 doctor can have many patients and 1 patient can have many doctors. Since the relationship goes both ways, this is a many-to-many relationship. We achieve a many-to-many relationship utilizing a third table called a junction table (as shown below).

***doctors table***

|doctor_id | doctor_name | 
| ------- | ---------- |
| 1 | 'Dr. Smith' |
| 2 | 'Dr. Adams'|
| 3 | 'Dr. Keen'|

***patients table***

|patient_id | patient_name | 
| ------- | ---------- |
| 1 | 'Abbey Jones' |
| 2 | 'Jane Stevens'|
| 3 | 'Devin Kennedy'|

***doctors_patients table (this is the junction table)***

|doctor_id_fk | patient_id_fk | 
| ------- | ---------- |
| 1 | 1 |
| 1 | 2 | 
| 3 | 2 | 
| 2 | 1 | 
| 2 | 2 | 




## One to One Relationship

For a one-to-one relationship, let's have a table for `students` as well as `backpacks`. A student posesses one backpack and alternatively a backpack only belongs to one student. Let's see how these tables would look like below. 

***students table***

|student_id | student_name | 
| ------- | ---------- |
| 1 | 'Mike Jones' |
| 2 | 'Steven Nguyen'|
| 3 | 'Jane Jackson' |

***backpacks table***

|backpack_id | book_count| student_id_fk |
| ------ | -------- | -------- |
| 1 | 3 | 2 |
| 2 | 3 | 3 |
| 3 | 3 | 1 | 

The example above looks very similar to a one-to-many relationship. This is because it is! The only difference in the implementation of a one-to-one relationship and a one-to-many relationship is that in a one-to-one relationship, a `UNIQUE` constraint needs to be added on the foreign key.

