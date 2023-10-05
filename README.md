# Room Conditions API

API for managing properties, rooms, and room conditions.

## Version: v1.2.3

### Base URL

- Base URL: `https://prop.tech/v1`

### Authentication

- Security: Bearer Token (BearerAuth)
- Bearer Token Format: JWT

## Paths

### `/properties`

#### `GET`

- Summary: Get all properties
- Response (200 OK):
  - Description: A list of properties.
  - Content-Type: application/json
  - Schema:
    - Type: array
    - Items: [PropertyWithRooms](#propertywithrooms)

#### `POST`

- Summary: Create a new property
- Request Body:
  - Required: true
  - Content-Type: application/json
  - Schema: [PropertyWithRooms](#propertywithrooms)
- Response (201 Created):
  - Description: The created property.
  - Content-Type: application/json
  - Schema: [PropertyWithRooms](#propertywithrooms)

### `/properties/{propertyId}`

#### Parameters

- `propertyId` (path)
  - Description: ID of the property
  - Type: string
  - Required: true

#### `GET`

- Summary: Get a property by ID
- Response (200 OK):
  - Description: The requested property.
  - Content-Type: application/json
  - Schema: [PropertyWithRooms](#propertywithrooms)

#### `PUT`

- Summary: Update a property by ID
- Parameters:
  - `propertyId` (path)
    - Description: ID of the property
    - Type: string
    - Required: true
- Request Body:
  - Required: true
  - Content-Type: application/json
  - Schema: [PropertyWithRooms](#propertywithrooms)
- Response (200 OK):
  - Description: The updated property.
  - Content-Type: application/json
  - Schema: [PropertyWithRooms](#propertywithrooms)

#### `DELETE`

- Summary: Delete a property by ID
- Response (204 No Content):
  - Description: Property deleted successfully

### `/properties/{propertyId}/rooms`

#### Parameters

- `propertyId` (path)
  - Description: ID of the property
  - Type: string
  - Required: true

#### `GET`

- Summary: Get all rooms of a property
- Response (200 OK):
  - Description: A list of rooms.
  - Content-Type: application/json
  - Schema:
    - Type: array
    - Items: [RoomWithConditions](#roomwithconditions)

### `/properties/{propertyId}/rooms/{roomId}`

#### Parameters

- `propertyId` (path)
  - Description: ID of the property
  - Type: string
  - Required: true
- `roomId` (path)
  - Description: ID of the room
  - Type: string
  - Required: true

#### `GET`

- Summary: Get a room by ID
- Response (200 OK):
  - Description: The requested room.
  - Content-Type: application/json
  - Schema: [RoomWithConditions](#roomwithconditions)

#### `PUT`

- Summary: Update a room by ID
- Request Body:
  - Required: true
  - Content-Type: application/json
  - Schema: [RoomWithConditions](#roomwithconditions)
- Response (200 OK):
  - Description: The updated room.
  - Content-Type: application/json
  - Schema: [RoomWithConditions](#roomwithconditions)

#### `DELETE`

- Summary: Delete a room by ID
- Response (204 No Content):
  - Description: Room deleted successfully

### `/properties/{propertyId}/rooms/{roomId}/conditions`

#### Parameters

- `propertyId` (path)
  - Description: ID of the property
  - Type: string
  - Required: true
- `roomId` (path)
  - Description: ID of the room
  - Type: string
  - Required: true

#### `GET`

- Summary: Get all room conditions of a room
- Response (200 OK):
  - Description: A list of room conditions.
  - Content-Type: application/json
  - Schema:
    - Type: array
    - Items: [RoomWithConditions](#roomwithconditions)

### `/properties/{propertyId}/rooms/{roomId}/conditions/{conditionId}`

#### Parameters

- `propertyId` (path)
  - Description: ID of the property
  - Type: string
  - Required: true
- `roomId` (path)
  - Description: ID of the room
  - Type: string
  - Required: true
- `conditionId` (path)
  - Description: ID of the room condition (temperature, humidity, lightLevel)
  - Type: string
  - Required: true

#### `GET`

- Summary: Get a room condition by ID
- Response (200 OK):
  - Description: The requested room condition.
  - Content-Type: application/json
  - Schema: [RoomCondition](#roomcondition)

#### `PUT`

- Summary: Update a room condition by ID
- Request Body:
  - Required: true
  - Content-Type: application/json
  - Schema: [RoomCondition](#roomcondition)
- Response (200 OK):
  - Description: The updated room condition.
  - Content-Type: application/json
  - Schema: [RoomCondition](#roomcondition)

#### `DELETE`

- Summary: Delete a room condition by ID
- Response (204 No Content):
  - Description: Room condition deleted successfully

## Schemas

### Property

- Type: object
- Properties:
  - `id` (string)
    - Description: Unique identifier for the property.
    - Required: true
  - `name` (string)
    - Description: Name of the property (e.g., building, flat, home).
    - Required: true

### PropertyWithRooms

- Type: object
- Extends: [Property](#property)
- Properties:
  - `rooms` (array of [RoomWithConditions](#roomwithconditions))
    - Description: List of rooms associated with the property.

### Room

- Type: object
- Properties:
  - `id` (string)
    - Description: Unique identifier for the room.
    - Required: true
  - `name` (string)
    - Description: Name of the room.
    - Required: true

### RoomWithConditions

- Type: object
- Extends: [Room](#room)
- Properties:
  - `conditions` (array of [RoomCondition](#roomcondition))
    - Description: List of conditions associated with the room.

### RoomCondition

- Type: object
- Properties:
  - `temperature` (number)
    - Description: Temperature in the room.
    - Required: true
  - `humidity` (number)
    - Description: Humidity in the room.
    - Required: true
  - `lightLevel` (number)
    - Description: Light level in the room.
    - Required: true
