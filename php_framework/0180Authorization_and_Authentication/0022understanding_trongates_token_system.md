# Understanding Trongate’s Token System

## Core Components of Trongate’s Token System


At the heart of Trongate’s authorization and authentication framework lies a trio of database tables that work together to manage user access securely. These tables form the backbone of the token system, enabling granular control over user roles, permissions, and session management.

### trongate_user_levels


This table defines the various user levels (e.g., admin, member) within the application. Each user level corresponds to a specific set of permissions, determining what actions a user can perform. For example:

```sql
INSERT INTO `trongate_user_levels` (`id`, `level_title`) 
VALUES (1, 'admin');
```


By defining user levels here, developers can enforce role-based access control across the application.

### trongate_users


The `trongate_users` table serves as a bridge between users and their roles. It links each user to a specific user level via the `user_level_id` field. Additionally, it generates a unique `code` for each user, which can be used for secure identification. For instance:

```sql
INSERT INTO `trongate_users` (`id`, `code`, `user_level_id`) 
VALUES (1, 'Tz8tehsWsTPUHEtzfbYjXzaKNqLmfAUz', 1);
```


This table ensures that every user is associated with a role, enabling seamless integration with the token system.

### trongate_tokens


The `trongate_tokens` table manages the generation, storage, and validation of authentication tokens. Each token is tied to a specific user (`user_id`) and has an expiration date (`expiry_date`). For example:

```sql
CREATE TABLE IF NOT EXISTS `trongate_tokens` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `token` varchar(125) DEFAULT NULL,
  `user_id` int(11) DEFAULT 0,
  `expiry_date` int(11) DEFAULT NULL,
  `code` varchar(3) DEFAULT '0',
  PRIMARY KEY (`id`)
);
```


Tokens are automatically purged from the database once they expire, ensuring a high level of security.

> [!NOTE]
> **Just To Let You Know...**
>
> The `user_id` column establishes a relational link to the `id` column in the `trongate_users` table through a foreign key relationship.



To visualize how these tables interact, refer to the following **table joins screenshot**, which illustrates the relationships between `trongate_tokens`, `trongate_users`, and `trongate_user_levels`.

![The contents of a basic Trongate web application](https://trongate.io/images/tokens_tables.webp)
        
*How the database tables involved in authorization and authentication are related.*
## How Tokens Enable Secure Access


Tokens play a pivotal role in Trongate’s security framework by acting as proof of authentication. Once a user successfully logs in, a token is generated and stored securely—either in the session, a cookie, or passed via HTTP headers. This token is then used to authenticate the user during subsequent requests.


For example, when a user submits a request to access a protected endpoint, Trongate validates the token by checking its expiration date and ensuring it matches a valid user. If the token is valid, access is granted; otherwise, the request is denied.

## Token Lifecycle Overview


While upcoming pages will delve deeper into the specifics of token generation, validation, and cleanup, here’s a high-level overview of the token lifecycle:


- **Generation:** Tokens are created upon specific events, such as successful login or account creation. Developers can customize parameters like `expiry_date` and whether the token should be stored in a cookie.
- **Storage:** Tokens can be stored in multiple locations, including:
        
- **Session:** Ideal for server-side applications.
- **Cookies:** Useful for client-side persistence.
- **HTTP Headers:** Commonly used for API-based interactions.


    
- **Validation:** Trongate validates tokens by querying the `trongate_tokens` table, ensuring the token is active and associated with a valid user.
- **Expiration and Cleanup:** Tokens have a default lifespan of one day (86,400 seconds). Expired tokens are automatically purged from the database to maintain system integrity.

