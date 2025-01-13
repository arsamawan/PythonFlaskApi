# Room Temperature Monitoring API

This project is a Python-based Flask API for managing room data and recording temperature readings in a PostgreSQL database. It allows creating rooms, adding temperature readings, and retrieving average temperature statistics.

## Features

1. **Create Room**: Add a new room with a unique name.
2. **Add Temperature**: Record temperature readings for a specific room with an optional timestamp.
3. **Retrieve Averages**: Get the global average temperature and the total number of distinct days with recorded temperatures.

## Prerequisites

- **Python 3.8+**
- **PostgreSQL**: Ensure PostgreSQL is installed and running.
- **Dependencies**:
  Install the required Python libraries:
  ```bash
  pip install flask psycopg2-binary python-dotenv
  ```

## Setup

1. **Database Configuration**:  (local db)
   Ensure you have a PostgreSQL database named `test` with a user `postgres` and password `admin`. Update the connection details in the script if needed:
   ```python
   connection = psycopg2.connect(
       database="test",
       user="postgres",
       password="admin",
       port=5432
   )
   ```

2. **Environment Variables**:  
   Use a `.env` file to store database credentials and load them with `dotenv` for security:
   ```dotenv
   DATABASE_URL=your_database_connection_url
   ```

3. **Run the Application**:  
   Start the Flask app:
   ```bash
   python app.py
   ```
   The API will be accessible at `http://localhost:5000`.

## API Endpoints

### 1. **Create Room**
   **POST** `/api/rooms`  
   - **Request Body**:
     ```json
     {
       "name": "Living Room"
     }
     ```
   - **Response**:
     ```json
     {
       "id": 1,
       "message": "Room Living Room created."
     }
     ```

### 2. **Add Temperature**
   **POST** `/api/temperature`  
   - **Request Body**:
     ```json
     {
       "temperature": 22.5,
       "room": 1,
       "date": "01-12-2025 14:30:00"  // Optional, defaults to current time
     }
     ```
   - **Response**:
     ```json
     {
       "message": "temperature added"
     }
     ```

### 3. **Get Global Average**
   **GET** `/api/average`  
   - **Response**:
     ```json
     {
       "average": 22.45,
       "days": 5
     }
     ```

## Database Schema

### Tables:
1. **rooms**:
   - `id` (Primary Key): Unique identifier for each room.
   - `name`: Name of the room.

2. **temperatures**:
   - `room_id`: Foreign key referencing `rooms.id`.
   - `temperature`: Recorded temperature.
   - `date`: Timestamp of the temperature reading.

## Notes

- Make sure the database user has the necessary permissions to create tables and insert data.
- The app uses SQL statements with PostgreSQL. Modify the SQL queries if using a different database system.
