# 001 - Use cases

Interviewr is an app to simplify and enhance interview process

## Status

* 2018-04-21: proposed

## Context

It contains the following steps:

* User:
  * Register/Login
  * Become an organization member
  * Become a candidate

* Candidate:
  * Create/update candidate profile
  * Search the relevant vacancies
  * Attempt to pass the vacancy test

* Company (the members):
  * Update organization
  * Control member list
  * Publish vacancies
  * View test results

Also, future functionality is planned with the next features:
* Arrange an interview
* Create a video chat for the
The current version doesn't cover these cases

## Decision

* A company can publish many vacancies and a candidate can try to apply for job
* The both scenarios are possible for user: to be an organization member and to be a candidate
* A candidate has additional features like candidate profile, possibilities to pass tests, and others

* A test is a separate part of vacancy that includes some amount of questions
* A candidate can try to pass the test once and the result are visible for him and for organization members
* A test represented like a quiz with some amount of possible answers

## Consequences

The Data Model should be presented in the next ADR with all decisions above