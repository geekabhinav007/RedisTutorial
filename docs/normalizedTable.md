# Table Structure

## To achieve normalization using the above-provided data, you can create the following tables and columns

### Post table

- pid (Primary Key)
- content
- timestamp
- edited
- uid (Foreign Key, references User table)
- tid (Foreign Key, references Topic table)

### Event table

- eid (Primary Key)
- newTitle
- type
- oldTitle
- timestamp
- uid (Foreign Key, references User table)

### User table

- uid (Primary Key)
- username
- profileviews
- lastposttime
- postcount
- topiccount

### Topic table

- tid (Primary Key)
- mainPid (Foreign Key, references Post table)
- title
- slug
- viewcount
- postcount
- lastposttime
