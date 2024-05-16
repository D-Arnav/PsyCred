# PsyCred

This is the official Repo for PsyCred during the 30 Hour Hackathon "MATHack"

link: https://github.com/tarunkay7/PsyCred

## Git Guide for Team

There are 4 essential commands you use in Git which are 

- `git add PATH/TO.FILE` : Adds the file to the staging area
- `git commit -m "COMMIT MESSAGE"` : Commits the file 
- `git push -u origin` : Pushes the file to remote repo
- `git pull` : Pulls changes from report repo

## Database Schema

### Users Table

The `Users` table stores information about users.

| Column Name | Data Type       | Constraints                | Description                     |
|-------------|-----------------|----------------------------|---------------------------------|
| Unique_id   | INTEGER         | PRIMARY KEY, AUTOINCREMENT | Unique identifier for each user|
| name        | VARCHAR         |                            | Name of the user                |
| age         | INTEGER         | CHECK (age > 18)           | Age of the user (must be over 18)|
| phone_number| TEXT            | UNIQUE                     | Phone number of the user        |
| pincode     | INTEGER         |                            | Pincode of the user             |

### Scores Table

The `Scores` table stores scores related to users.

| Column Name           | Data Type | Constraints           | Description                                   |
|-----------------------|-----------|-----------------------|-----------------------------------------------|
| user_id               | INTEGER   |                       | Foreign key referencing the Unique_id column in the Users table |
| demographic_score     | DECIMAL   | DEFAULT 0             | Score representing user's demographic data    |
| psychometric_test_score| DECIMAL   | DEFAULT 0             | Score representing user's psychometric test performance |

### creditworthiness_score Table

The `creditworthiness_score` table stores creditworthiness scores of users.

| Column Name           | Data Type | Constraints           | Description                                   |
|-----------------------|-----------|-----------------------|-----------------------------------------------|
| user_id               | INTEGER   | PRIMARY KEY           | Primary key referencing the Unique_id column in the Users table |
| creditworthiness_score| DECIMAL   | DEFAULT 0             | Score representing user's creditworthiness    |

### Foreign Key Constraints

- The `user_id` column in the `Scores` table references the `Unique_id` column in the `Users` table.
- The `user_id` column in the `creditworthiness_score` table references the `Unique_id` column in the `Users` table.

This schema is designed to store user information, including demographic details, psychometric test scores, and creditworthiness scores. Foreign key constraints ensure referential integrity between related tables.

## API Documentation

This document provides documentation for the user management APIs.

### Create User

- **URL**: `/api/users/v1/create_user`
- **Method**: `POST`
- **Description**: Creates a new user in the database.
- **Request Body**:

    ```json
    {
        "name": "John Doe",
        "age": 30,
        "phone_number": "1234567890",
        "education": "Bachelor's Degree",
        "pincode": "12345"
    }
    ```

- **Response**:

    - **Success (201)**:

        ```json
        {
            "message": "User created successfully"
        }
        ```

    - **Error (400)**:

        ```json
        {
            "error": "Incomplete user data"
        }
        ```

        OR

        ```json
        {
            "error": "Invalid request body"
        }
        ```

    - **Error (500)**:

        ```json
        {
            "error": "Internal Server Error"
        }
        ```

### Get User

- **URL**: `/api/users/v1/get_user/<int:user_id>`
- **Method**: `GET`
- **Description**: Retrieves user details by ID from the database.
- **Parameters**:
    - `user_id`: Unique identifier of the user.
- **Response**:

    - **Success (200)**:

        ```json
        {
            "Unique_id": 1,
            "name": "John Doe",
            "age": 30,
            "phone_number": "1234567890",
            "education": "Bachelor's Degree",
            "pincode": "12345"
        }
        ```

    - **Error (404)**:

        ```json
        {
            "error": "User not found"
        }
        ```

    - **Error (500)**:

        ```json
        {
            "error": "Internal Server Error"
        }
        ```

### Update User

- **URL**: `/api/users/v1/update_user/<int:user_id>`
- **Method**: `PUT`
- **Description**: Updates user details by ID in the database.
- **Parameters**:
    - `user_id`: Unique identifier of the user.
- **Request Body**:

    ```json
    {
        "name": "John Doe",
        "age": 35,
        "phone_number": "9876543210",
        "education": "Master's Degree",
        "pincode": "54321"
    }
    ```

- **Response**:

    - **Success (200)**:

        ```json
        {
            "message": "User updated successfully"
        }
        ```

    - **Error (404)**:

        ```json
        {
            "error": "User not found"
        }
        ```

    - **Error (500)**:

        ```json
        {
            "error": "Internal Server Error"
        }
        ```

### Delete User

- **URL**: `/api/v1/users/delete_user/<int:user_id>`
- **Method**: `DELETE`
- **Description**: Deletes a user by ID from the database.
- **Parameters**:
    - `user_id`: Unique identifier of the user.
- **Response**:

    - **Success (200)**:

        ```json
        {
            "message": "User deleted successfully"
        }
        ```

    - **Error (404)**:

        ```json
        {
            "error": "User not found"
        }
        ```

    - **Error (500)**:

        ```json
        {
            "error": "Internal Server Error"
        }
        ```