openapi: 3.0.3
info:
  title: BulletinBoard API
  description: |
    BulletinBoard is a Java-based web application for posting and managing messages in a bulletin board system. 
    It allows users to create, read, update, and delete posts in an organized manner.
    
    ## Features
    - ✔️ CRUD operations – Create, Read, Update, and Delete posts
    - ✔️ Password validation for editing and deleting posts
    - ✔️ Bootstrap-based UI for a responsive design
    - ✔️ Database integration for storing messages persistently
    - ✔️ Error & success messages for better user feedback
    
    ## Technology Stack
    - Java (Spring Boot) – Backend framework
    - PostgreSQL / MySQL – Database for storing messages
    - Thymeleaf – Template engine for rendering views
    - Bootstrap – Frontend framework for styling
  version: 1.0.0
  contact:
    name: Ajax-Z01
    url: https://github.com/Ajax-Z01/bulletinboard
  license:
    name: MIT
    url: https://opensource.org/licenses/MIT

servers:
  - url: http://localhost:8080
    description: Local development server
  - url: https://api.bulletinboard.example.com
    description: Production server

tags:
  - name: Posts
    description: Operations related to bulletin board posts
  - name: Authentication
    description: Password validation for post operations

paths:
  /api/posts:
    get:
      tags:
        - Posts
      summary: Get all posts
      description: Retrieve a list of all bulletin board posts
      parameters:
        - name: page
          in: query
          description: Page number for pagination
          required: false
          schema:
            type: integer
            minimum: 0
            default: 0
        - name: size
          in: query
          description: Number of posts per page
          required: false
          schema:
            type: integer
            minimum: 1
            maximum: 100
            default: 10
        - name: sort
          in: query
          description: Sort field and direction (e.g., createdAt,desc)
          required: false
          schema:
            type: string
            default: "createdAt,desc"
      responses:
        '200':
          description: Successfully retrieved posts
          content:
            application/json:
              schema:
                type: object
                properties:
                  content:
                    type: array
                    items:
                      $ref: '#/components/schemas/Post'
                  totalElements:
                    type: integer
                  totalPages:
                    type: integer
                  size:
                    type: integer
                  number:
                    type: integer
        '500':
          description: Internal server error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

    post:
      tags:
        - Posts
      summary: Create a new post
      description: Create a new bulletin board post
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/CreatePostRequest'
      responses:
        '201':
          description: Post created successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Post'
        '400':
          description: Bad request - validation errors
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ValidationErrorResponse'
        '500':
          description: Internal server error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /api/posts/{id}:
    get:
      tags:
        - Posts
      summary: Get post by ID
      description: Retrieve a specific post by its ID
      parameters:
        - name: id
          in: path
          required: true
          description: Post ID
          schema:
            type: integer
            format: int64
      responses:
        '200':
          description: Post found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Post'
        '404':
          description: Post not found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        '500':
          description: Internal server error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

    put:
      tags:
        - Posts
      summary: Update a post
      description: Update an existing post with password validation
      parameters:
        - name: id
          in: path
          required: true
          description: Post ID
          schema:
            type: integer
            format: int64
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UpdatePostRequest'
      responses:
        '200':
          description: Post updated successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Post'
        '400':
          description: Bad request - validation errors
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ValidationErrorResponse'
        '401':
          description: Unauthorized - invalid password
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        '404':
          description: Post not found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        '500':
          description: Internal server error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

    delete:
      tags:
        - Posts
      summary: Delete a post
      description: Delete a post with password validation
      parameters:
        - name: id
          in: path
          required: true
          description: Post ID
          schema:
            type: integer
            format: int64
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required:
                - password
              properties:
                password:
                  type: string
                  description: Password for the post
                  example: "mypassword123"
      responses:
        '204':
          description: Post deleted successfully
        '401':
          description: Unauthorized - invalid password
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        '404':
          description: Post not found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        '500':
          description: Internal server error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /api/posts/search:
    get:
      tags:
        - Posts
      summary: Search posts
      description: Search posts by title or content
      parameters:
        - name: query
          in: query
          required: true
          description: Search query string
          schema:
            type: string
            minLength: 1
        - name: page
          in: query
          description: Page number for pagination
          required: false
          schema:
            type: integer
            minimum: 0
            default: 0
        - name: size
          in: query
          description: Number of posts per page
          required: false
          schema:
            type: integer
            minimum: 1
            maximum: 100
            default: 10
      responses:
        '200':
          description: Search results
          content:
            application/json:
              schema:
                type: object
                properties:
                  content:
                    type: array
                    items:
                      $ref: '#/components/schemas/Post'
                  totalElements:
                    type: integer
                  totalPages:
                    type: integer
                  size:
                    type: integer
                  number:
                    type: integer
        '400':
          description: Bad request - invalid search parameters
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        '500':
          description: Internal server error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /api/posts/{id}/verify-password:
    post:
      tags:
        - Authentication
      summary: Verify post password
      description: Verify if the provided password is correct for a post
      parameters:
        - name: id
          in: path
          required: true
          description: Post ID
          schema:
            type: integer
            format: int64
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required:
                - password
              properties:
                password:
                  type: string
                  description: Password to verify
                  example: "mypassword123"
      responses:
        '200':
          description: Password verification result
          content:
            application/json:
              schema:
                type: object
                properties:
                  valid:
                    type: boolean
                    description: Whether the password is valid
                  message:
                    type: string
                    description: Result message
        '404':
          description: Post not found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        '500':
          description: Internal server error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

components:
  schemas:
    Post:
      type: object
      properties:
        id:
          type: integer
          format: int64
          description: Unique identifier for the post
          example: 1
        title:
          type: string
          description: Title of the post
          example: "Welcome to BulletinBoard"
        content:
          type: string
          description: Content of the post
          example: "This is the first post on our bulletin board!"
        author:
          type: string
          description: Author of the post
          example: "John Doe"
        createdAt:
          type: string
          format: date-time
          description: When the post was created
          example: "2024-09-07T10:00:00Z"
        updatedAt:
          type: string
          format: date-time
          description: When the post was last updated
          example: "2024-09-07T10:00:00Z"
        hasPassword:
          type: boolean
          description: Whether the post is password protected
          example: true

    CreatePostRequest:
      type: object
      required:
        - title
        - content
        - author
      properties:
        title:
          type: string
          minLength: 1
          maxLength: 255
          description: Title of the post
          example: "Welcome to BulletinBoard"
        content:
          type: string
          minLength: 1
          maxLength: 5000
          description: Content of the post
          example: "This is the first post on our bulletin board!"
        author:
          type: string
          minLength: 1
          maxLength: 100
          description: Author of the post
          example: "John Doe"
        password:
          type: string
          minLength: 4
          maxLength: 100
          description: Optional password to protect the post
          example: "mypassword123"

    UpdatePostRequest:
      type: object
      required:
        - title
        - content
        - author
        - password
      properties:
        title:
          type: string
          minLength: 1
          maxLength: 255
          description: Updated title of the post
          example: "Updated: Welcome to BulletinBoard"
        content:
          type: string
          minLength: 1
          maxLength: 5000
          description: Updated content of the post
          example: "This is the updated first post on our bulletin board!"
        author:
          type: string
          minLength: 1
          maxLength: 100
          description: Updated author of the post
          example: "John Doe"
        password:
          type: string
          description: Current password for the post
          example: "mypassword123"

    ErrorResponse:
      type: object
      properties:
        timestamp:
          type: string
          format: date-time
          description: When the error occurred
          example: "2024-09-07T10:00:00Z"
        status:
          type: integer
          description: HTTP status code
          example: 404
        error:
          type: string
          description: Error type
          example: "Not Found"
        message:
          type: string
          description: Error message
          example: "Post with ID 999 not found"
        path:
          type: string
          description: Request path that caused the error
          example: "/api/posts/999"

    ValidationErrorResponse:
      type: object
      properties:
        timestamp:
          type: string
          format: date-time
          description: When the validation error occurred
          example: "2024-09-07T10:00:00Z"
        status:
          type: integer
          description: HTTP status code
          example: 400
        error:
          type: string
          description: Error type
          example: "Bad Request"
        message:
          type: string
          description: General error message
          example: "Validation failed"
        path:
          type: string
          description: Request path that caused the error
          example: "/api/posts"
        validationErrors:
          type: array
          items:
            type: object
            properties:
              field:
                type: string
                description: Field that failed validation
                example: "title"
              message:
                type: string
                description: Validation error message
                example: "Title cannot be empty"

  securitySchemes:
    BasicAuth:
      type: http
      scheme: basic
      description: Basic authentication for admin operations

security:
  - BasicAuth: []
