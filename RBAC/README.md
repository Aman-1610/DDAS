# Role-Based Access Control (RBAC)

## Why Use RBAC?
- **Purpose**: RBAC is used to control user access to resources based on their assigned roles (e.g., Admin, User, Viewer).
- **Relevance to DDAS**:
  - Ensures only authorized users can access or modify files.
  - Protects sensitive operations like adding or editing metadata.
  - Simplifies system security by defining clear access levels for each role.

### Advantages:
- Enhances **security** by limiting actions to authorized roles.
- Improves **usability** by showing users only relevant options based on their role.
- Provides **auditability** for tracking user actions based on roles.

---

## How to Implement RBAC in DDAS

### Step 1: Define Roles and Permissions
1. **Identify Roles**:
   - **Admin**: Full access to all features (e.g., add/edit metadata, manage users).
   - **User**: Can download files, view metadata.
   - **Viewer**: Can only view metadata but not download.

2. **Assign Permissions**:
   - Map roles to specific permissions (e.g., Admin: CRUD, User: Read-Only).

---

### Step 2: Database Schema for Roles
1. Create tables for users and roles:
```sql
CREATE TABLE roles (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL
);

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    role_id INT,
    FOREIGN KEY (role_id) REFERENCES roles(id)
);
```
2. Insert predefined roles:
```sql
INSERT INTO roles (name) VALUES ('ADMIN'), ('USER'), ('VIEWER');
```
### Step 3: Implement Role-Based Logic in Java
a. Add Spring Security Dependency:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```
b. Configure Security in SecurityConfig:
```java
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
            .antMatchers("/admin/**").hasRole("ADMIN")
            .antMatchers("/user/**").hasRole("USER")
            .antMatchers("/viewer/**").hasRole("VIEWER")
            .antMatchers("/public/**").permitAll()
            .and().formLogin(); // Default login form
    }
}
```
### Step 4: Authentication and Authorization
1. Custom User Details Service: Implement UserDetailsService to fetch user data from the database:

```java
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;

@Service
public class CustomUserDetailsService implements UserDetailsService {

    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        UserEntity user = userRepository.findByUsername(username);
        if (user == null) {
            throw new UsernameNotFoundException("User not found");
        }

        return User.builder()
            .username(user.getUsername())
            .password(user.getPassword())
            .roles(user.getRole().getName()) // Assign role
            .build();
    }
}
```
2. Password Encryption: Use BCrypt to encrypt passwords before storing them:
```java
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;

BCryptPasswordEncoder encoder = new BCryptPasswordEncoder();
String encryptedPassword = encoder.encode("plain_password");
```
### Step 5: Test the RBAC Implementation
1. Create Users and Assign Roles:

```sql
INSERT INTO users (username, password, role_id) VALUES
('admin', 'encrypted_password', 1), -- ADMIN
('user1', 'encrypted_password', 2), -- USER
('viewer1', 'encrypted_password', 3); -- VIEWER
```
2. Access Resources:
 Admin URL: /admin/manage
 User URL: /user/view
 Viewer URL: /viewer/metadata
