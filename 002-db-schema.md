# 002 - Template

DB Schema by use cases from [001-usecases.md](./usecases.md)

## Status

* 2018-04-27: proposed
* 2018-05-09: updated

## Context

By the defined use cases in the previous ADR to design a DB schema and describe all data

## Decision

* Use RDMS like Postgres
* Initial SQL script like the following: 

```sql
CREATE TABLE person (
  id SERIAL PRIMARY KEY,
  login VARCHAR(20) NOT NULL,
  name VARCHAR(35) NOT NULL,
  email VARCHAR(35) UNIQUE NOT NULL,
  location VARCHAR(50),
  bio VARCHAR,
  avatar_url VARCHAR
);

CREATE TABLE organization (
  id SERIAL PRIMARY KEY,
  name VARCHAR(35) NOT NULL,
  email VARCHAR(35) UNIQUE NOT NULL,
  description VARCHAR,
  location VARCHAR(50),
  avatar_url VARCHAR
);

CREATE TABLE membership (
  organization_id INT REFERENCES organization(id),
  person_id INT REFERENCES person(id),
  role VARCHAR CHECK (role IN ('owner', 'member')),
  CONSTRAINT membership_id PRIMARY KEY (organization_id, person_id)
);

CREATE TABLE vacancy (
  id SERIAL PRIMARY KEY,
  title VARCHAR(30) NOT NULL,
  description VARCHAR NOT NULL,
  location VARCHAR(50),
  organization_id INT REFERENCES organization(id)
);

CREATE TABLE applicant (
  vacancy_id INT REFERENCES vacancy(id),
  person_id INT REFERENCES person(id),
  CONSTRAINT applicant_id PRIMARY KEY (vacancy_id, person_id)
);

CREATE TABLE test (
  id SERIAL PRIMARY KEY,
  title VARCHAR(30) NOT NULL,
  vacancy_id INT REFERENCES vacancy(id)
);

CREATE TABLE question (
  id SERIAL PRIMARY KEY,
  description VARCHAR NOT NULL,
  test_id INT REFERENCES test(id),
);

CREATE TABLE answer (
  id SERIAL PRIMARY KEY,
  description VARCHAR NOT NULL,
  is_correct BOOLEAN NOT NULL,
  question_id INT REFERENCES question(id)
);

CREATE TABLE test_result (
  id SERIAL PRIMARY KEY,
  applicant_id INT REFERENCES applicant(id),
  answer_id INT REFERENCES answer(id)
);
```

## Consequences

TBD