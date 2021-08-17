---
title: "USERS table description"
weight: 1
# bookFlatSection: true
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# USERS
## Properties

| Names                 | Expected Type | Description                                                                 | Refer to          | Notes            |
| --------------------- | ------------- | --------------------------------------------------------------------------- | ----------------- | ---------------- |
| ID                    | ID            |                                                                             |                   |                  |
| displayName           | string        |                                                                             |                   |                  |
| phoneNumber           | string        | Normalized phone number, country code added, eg: +84328888888               |                   |                  |
| email                 | string        |                                                                             |                   |                  |
| createdBy             | ID            |                                                                             | USERS.ID          | see [User creation](#user-creation) |
| chatfuelMessengerId   | string        |                                                                             |                   | see [User creation](#user-creation) |
| duplicatedWithId      | ID            |                                                                             | USERS.ID          | see [User creation](#user-creation) |
| createdByRestaurantId | ID            |                                                                             | RESTAURANTS.ID    | see [User creation](#user-creation) |
| admin                 | boolean       |                                                                             |                   | see [Admin and roles](#admin-and-roles) |
| roles                 | string[]      |                                                                             | ROLES.ID          | see [Admin and roles](#admin-and-roles) |

## Notes
### User creation 

> - If the user has `createdBy` property, this is ID of the human admin, this user is created by the "Record User" feature on admin panel.
> - If the user has `chatfuelMessengerId` property, this user is created by recording user chat from our facebook group messenger, this is recorded automatically. If by any chances, this user has already signin before and we cannot merge the 2 users, there will be a `duplicatedWithId` indicate that this is a duplicated user and this user and the user with that ID is the same.
> - If the user has `createdByRestaurantId` property, this user is created from crawling data from other sites like _chotot_, _muaban.net_, etc, when a new premise is crawled, the user data from that post is automatically extracted and then create a new user. That property is the post that trigger this process. This is also recorded automatically.
> - Other than that, this user is an organic user, this user signin from our page.
> - One special case is that if the user has `admin == true` property, this is our company's admin.

### Admin and roles

All company admin will have `admin == true` property. Roles will determine if the `admin` has permission to do a specific tasks. Roles and permission is monitored with [**ROLES**](database/entities/roles) table. This table below describe list of roles for admin, for more detail on data structure and notes, see [**ROLES**](database/entities/roles).

| Names                 | Description                                                                  | Notes            |
| --------------------- | ---------------------------------------------------------------------------  | ---------------- |
| superadmin            | Highest permission, can do everything                                        |                  |
| sales                 |                                                                              |                  |
| agent                 | Can create and read post, record user, create bill                           |                  |
| approver              | Can approve bill using proof method                                          |                  |
