# Lab 9 - Spring Boot Transaction

Spring Boot + PostgreSQL + JPA project demonstrating database transactions with `@Transactional`.

## Features
- Create an Account
- Get Account by ID
- Deposit money
- Save DepositTransaction
- Demonstrate COMMIT / ROLLBACK with `@Transactional`

## Database
Create PostgreSQL database:

```sql
CREATE DATABASE lab9;
```

Then edit `src/main/resources/application.properties` and set your PostgreSQL password.

## Run

```bash
mvn spring-boot:run
```

## API

### Create account
POST `/accounts`

```json
{
  "accountNumber": "1234567890",
  "ownerName": "Soranan",
  "balance": 0
}
```

### Get account
GET `/accounts/{id}`

### Deposit
POST `/accounts/{id}/deposit`

```json
{
  "amount": 1000
}
```

## Rollback experiment
Temporarily add this after `depositRepository.save(transaction);`:

```java
throw new RuntimeException("Test Rollback");
```

Keep `@Transactional`, restart the application, and send a deposit request. The transaction should roll back.

After the experiment, remove the `throw` line and keep `@Transactional`.
