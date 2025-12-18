# CUBI12 - API
API RESTful used as backend for Cubi12 software using .NET 7 and MSSql.

Cubi12 is (currently) an open source project to help students at UCN (Universidad Cat�lica del Norte) at Chile to understand all the subjects they can take and their progress in the career.

## Prerequisites

- SDK [.NET 7](https://dotnet.microsoft.com/es-es/download/dotnet/7.0).
- Port 80 Available
- git [2.33.0](https://git-scm.com/downloads) or higher.
- [Docker](https://www.docker.com/) **Note**: If you do not have installed is highly recommended to see the steps to correctly install docker on your machine with [Linux](https://docs.docker.com/desktop/install/linux-install/), [Windows](https://docs.docker.com/desktop/install/windows-install/) or [MacOs](https://docs.docker.com/desktop/install/mac-install/).


## Getting Started

Follow these steps to get the project up and running on your local machine:

1. Clone the repository to your local machine.

2. Navigate to the root folder.
   ```bash
   cd Backend
   ```

3. Inside the project you will see 2 folders: Cubitwelve and Cubitwelve.tests, navigate to the first.
    ```bash
    cd Cubitwelve
    ```

4. Inside the Cubitwelve folder, create a file called `.env` and fill it with the following example values:
```dotenv
    # Database
    DB_CONNECTION=Host=localhost;Port=5432;Database=cubi12db;Username=postgres;Password=YourStrongPassword123;
    
    # JWT Secret
    JWT_SECRET=your_secure_secret_key_at_least_32_characters_long
    
    # PostgreSQL (for Docker setup)
    POSTGRES_PASSWORD=YourStrongPassword123
```
  **Note 1:** Choose a strong password for `POSTGRES_PASSWORD` (at least 8 characters with letters, numbers, and symbols).
    
    **Note 2:** If you change `POSTGRES_PASSWORD`, also update the `Password` parameter in `DB_CONNECTION`.
    
    **Note 3:** The `JWT_SECRET` should be at least 32 characters long to meet HmacSha256 requirements and avoid runtime exceptions.

5. Install project dependencies using dotnet sdk.
   ```bash
   dotnet restore
   ```

6. Setup the container for mySQL database, because the compose file have the name **dev.yml** the command needs to include *--file* flag
    ```bash
    docker-compose --file dev.yml up -d
    ```

7. Is recommended to wait 5 seconds and the run the project, thus the database structure finish to build before backend tries to connect.

    Either way, the backend tries until 5 times to connect if the database is not responding
    ```bash
    dotnet run
    ```

This will start the development server, and you can access the app in your web browser by visiting http://localhost:80.

## Use

To see the endpoints you can access to OpenAPI Swagger documentation at http://localhost:80/swagger/index.html

Also you can use [Postman](https://www.postman.com/) or another software to use the API.

## Database Persistence

The database container do not have a volume assigned, thus if you stop the container all the information will be deleted.

This behaviour is adopted because the Db container is designed only for development purposes.

## Testing

The project uses [xUnit](https://xunit.net/) as testing framework and [FluentAssertions](https://fluentassertions.com/) to improve readability, to run all the tests run the following commands:

1. If you are inside *Cubitwelve* folder go to root folder
    ```bash
    # Only if you are inside Cubitwelve folder
    cd ..
    ```
2. Now you are on the root folder, run the tests
    ```bash
    dotnet test

    ```
