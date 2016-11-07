# Punchy
Web API using node.js, express, rabbitmq, elasticSearch &amp; mongoDB
The API will be used as a foundation for a new service called "punchcard.com", where both companies and their users can register, and users can then issue a "punch". When they've collected enough punches (usually 10), they will get a discount at the company (perhaps a free meal at a restaurant after buying 10 meals, or 20% discount of their next purchase at some shop etc.).

## Setup

* mongod
* mongo
* node consumer
* node producer
* docker

## Routes

### **GET** /api/companies[?page=N&max=N&search=Q]
Authentication: none
Requires:
Returns: list of companies

### **POST** /api/companies
Authentication: none
Requires: name, punchCount, description
Returns: company_id

### **GET** /api/companies/:id
Authentication: none
Requires:
Returns: company

### **GET** /api/users/
Authentication: administration token
Requires:
Returns: list of users

### **POST**  /api/users/
Authentication: administration token
Requires: name, email, gender
Returns: user's token

### **GET** /api/users/:id/punches?company=:id
Authentication: administration token
Requires:
Returns: list of user's punches

### **POST** /api/users/:id/punches
Authentication: administration token
Requires: company_id
Returns:

### **POST** /api/my/punches
Authentication: user token
Requires: company_id
Returns: id of punch and "discount: true" if collected enough punches

## Authentication
When a user is created he gets an unique token.
When a user wants to access his punches (/api/my/punches), his token must be put in the authorization header.
An administration token must be in the authorazion header to createa new company or user. The token is hardcoded as "smuuu".

## Data

### Users
_id: string
name: string
token: string
gender: string: m, f or o

### Companies
_id: string
name: string
punchCount: number

### Punches
_id: string
company_id: string
user_id: string
created: string
used: number

## Bugs to fix

- [ ] 201 í post föllum
- [ ] company name í punches en ekki bara companyid
- [ ] cant set headers after they are sent
- [ ] token undefined.  get /api/users