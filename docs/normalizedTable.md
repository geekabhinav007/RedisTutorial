# Table Structure

## To achieve normalization using the desire columns in last part of this tutorial, you can create the following tables and columns

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

### Demo Table

Post table:

| pid | content | timestamp | edited | uid | tid |
|-----|---------|----------|--------|-----|-----|
|     |         |          |        |     |     |

Event table:

| eid | newTitle | type | oldTitle | timestamp | uid |
|-----|----------|------|----------|----------|-----|
|     |          |      |          |          |     |

User table:

| uid | username | profileviews | lastposttime | postcount | topiccount |
|-----|----------|--------------|--------------|-----------|-----------|
|     |          |              |              |           |           |

Topic table:

| tid | mainPid | title | slug | viewcount | postcount | lastposttime |
|-----|---------|-------|------|----------|-----------|--------------|
|     |         |       |      |          |           |              |
