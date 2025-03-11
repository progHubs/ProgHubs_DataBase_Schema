# ProgHubs

## The Ultimate Developer Collaboration Platform

ProgHubs is a comprehensive platform designed to streamline collaboration among software development teams. It provides tools for project management, team communication, code challenges, and idea sharing - all in one integrated ecosystem.

### Key Features
- **Team Management**: Create and manage development teams with customizable roles
- **Project Tracking**: Organize work with projects, tasks, and sprints
- **Real-time Communication**: Chat channels and direct messaging
- **Skill Development**: Participate in coding challenges and track progress
- **Innovation Hub**: Share and vote on project ideas
- **Seamless Integration**: Connect with popular development tools

Below is the complete API documentation for developers looking to integrate with or extend the ProgHubs platform.

# ProgHubs -- The Complete API Documentation

## Table of Contents

- [Authentication](#authentication)
- [Users](#users)
- [User Profiles](#user-profiles)
- [Teams](#teams)
- [Projects](#projects)
- [Tasks](#tasks)
- [Messages](#messages)
- [Channels](#channels)
- [Challenges](#challenges)
- [Ideas](#ideas)
- [Comments](#comments)
- [Files](#files)
- [Notifications](#notifications)
- [Sprints](#sprints)
- [Milestones](#milestones)
- [Activity Logs](#activity-logs)
- [Integrations](#integrations)

## Authentication

### Register

- **POST** `/api/auth/register`
- **Description**: Create a new user account
- **Request Body**:
  ```json
  {
    "full_name": "Jane Doe",
    "email": "jane@example.com",
    "password": "securepassword123"
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "full_name": "Jane Doe",
    "email": "jane@example.com",
    "created_at": "timestamp"
  }
  ```

### Login

- **POST** `/api/auth/login`
- **Description**: Authenticate a user and get access token
- **Request Body**:
  ```json
  {
    "email": "jane@example.com",
    "password": "securepassword123"
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "access_token": "jwt_token",
    "refresh_token": "refresh_token",
    "user": {
      "id": "uuid",
      "full_name": "Jane Doe",
      "email": "jane@example.com"
    }
  }
  ```

### Refresh Token

- **POST** `/api/auth/refresh`
- **Description**: Get a new access token using refresh token
- **Request Body**:
  ```json
  {
    "refresh_token": "refresh_token"
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "access_token": "new_jwt_token"
  }
  ```

### Password Reset Request

- **POST** `/api/auth/password-reset`
- **Description**: Request a password reset token
- **Request Body**:
  ```json
  {
    "email": "jane@example.com"
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "message": "Password reset instructions sent to email"
  }
  ```

### Password Reset Confirmation

- **POST** `/api/auth/password-reset/confirm`
- **Description**: Reset password using token
- **Request Body**:
  ```json
  {
    "token": "reset_token",
    "password": "new_password"
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "message": "Password successfully reset"
  }
  ```

### Logout

- **POST** `/api/auth/logout`
- **Description**: Invalidate current token
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "message": "Successfully logged out"
  }
  ```

## Users

### Get Current User

- **GET** `/api/users/me`
- **Description**: Get details of authenticated user
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "full_name": "Jane Doe",
    "email": "jane@example.com",
    "is_active": true,
    "last_login_at": "timestamp",
    "created_at": "timestamp"
  }
  ```

### Get User by ID

- **GET** `/api/users/{user_id}`
- **Description**: Get details of a specific user
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "full_name": "Jane Doe",
    "profile_image_url": "url_to_image",
    "role": "Frontend Developer"
  }
  ```

### Update User

- **PUT** `/api/users/me`
- **Description**: Update current user's details
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "full_name": "Jane Smith",
    "email": "jane.smith@example.com"
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "full_name": "Jane Smith",
    "email": "jane.smith@example.com",
    "updated_at": "timestamp"
  }
  ```

### List Users

- **GET** `/api/users`
- **Description**: Get a list of users
- **Authentication**: Required
- **Query Parameters**:
  - `page`: Page number (default: 1)
  - `limit`: Items per page (default: 20)
  - `search`: Search by name or email
- **Response**: `200 OK`
  ```json
  {
    "total": 42,
    "page": 1,
    "limit": 20,
    "users": [
      {
        "id": "uuid",
        "full_name": "Jane Doe",
        "profile_image_url": "url_to_image",
        "role": "Frontend Developer"
      },
      ...
    ]
  }
  ```

## User Profiles

### Get Profile

- **GET** `/api/profiles/{user_id}`
- **Description**: Get a user's profile details
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "user_id": "uuid",
    "social_media_urls": [
      "https://github.com/username",
      "https://linkedin.com/in/username"
    ],
    "role": "Frontend Developer",
    "profile_image_url": "url_to_image",
    "bio": "Full-stack developer with 5 years of experience",
    "resume_url": "url_to_resume",
    "skills": ["JavaScript", "React", "Node.js"],
    "experience": [
      {
        "company": "Tech Inc",
        "position": "Senior Developer",
        "start_date": "2020-01",
        "end_date": "2022-12",
        "description": "Worked on various projects"
      }
    ],
    "education": [
      {
        "institution": "University of Technology",
        "degree": "Bachelor of Computer Science",
        "year": "2018"
      }
    ]
  }
  ```

### Update Profile

- **PUT** `/api/profiles/me`
- **Description**: Update current user's profile
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "social_media_urls": ["https://github.com/newusername"],
    "role": "Full Stack Developer",
    "bio": "Updated bio information",
    "skills": ["JavaScript", "React", "Node.js", "Python"]
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "user_id": "uuid",
    "social_media_urls": ["https://github.com/newusername"],
    "role": "Full Stack Developer",
    "profile_image_url": "url_to_image",
    "bio": "Updated bio information",
    "skills": ["JavaScript", "React", "Node.js", "Python"],
    "updated_at": "timestamp"
  }
  ```

### Upload Profile Image

- **POST** `/api/profiles/me/image`
- **Description**: Upload or update profile image
- **Authentication**: Required
- **Request**: Form data with image file
- **Response**: `200 OK`
  ```json
  {
    "profile_image_url": "new_image_url"
  }
  ```

### Upload Resume

- **POST** `/api/profiles/me/resume`
- **Description**: Upload or update resume
- **Authentication**: Required
- **Request**: Form data with resume file
- **Response**: `200 OK`
  ```json
  {
    "resume_url": "new_resume_url"
  }
  ```

## Teams

### Create Team

- **POST** `/api/teams`
- **Description**: Create a new team
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "name": "Dream Team",
    "description": "A team of awesome developers",
    "is_public": true
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "name": "Dream Team",
    "description": "A team of awesome developers",
    "logo_url": null,
    "is_public": true,
    "created_at": "timestamp"
  }
  ```

### Get Team

- **GET** `/api/teams/{team_id}`
- **Description**: Get team details
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "name": "Dream Team",
    "description": "A team of awesome developers",
    "logo_url": "url_to_logo",
    "is_public": true,
    "member_count": 5,
    "created_at": "timestamp"
  }
  ```

### Update Team

- **PUT** `/api/teams/{team_id}`
- **Description**: Update team details
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Request Body**:
  ```json
  {
    "name": "Updated Team Name",
    "description": "Updated description",
    "is_public": false
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "name": "Updated Team Name",
    "description": "Updated description",
    "logo_url": "url_to_logo",
    "is_public": false,
    "updated_at": "timestamp"
  }
  ```

### List Teams

- **GET** `/api/teams`
- **Description**: Get a list of teams
- **Authentication**: Required
- **Query Parameters**:
  - `page`: Page number (default: 1)
  - `limit`: Items per page (default: 20)
  - `search`: Search by name
  - `is_public`: Filter by public/private (true/false)
- **Response**: `200 OK`
  ```json
  {
    "total": 15,
    "page": 1,
    "limit": 20,
    "teams": [
      {
        "id": "uuid",
        "name": "Dream Team",
        "description": "A team of awesome developers",
        "logo_url": "url_to_logo",
        "member_count": 5
      },
      ...
    ]
  }
  ```

### Upload Team Logo

- **POST** `/api/teams/{team_id}/logo`
- **Description**: Upload or update team logo
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Request**: Form data with image file
- **Response**: `200 OK`
  ```json
  {
    "logo_url": "new_logo_url"
  }
  ```

### Add Team Member

- **POST** `/api/teams/{team_id}/members`
- **Description**: Add a user to a team with specified role
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Request Body**:
  ```json
  {
    "user_id": "uuid",
    "role": "Member" // Member, Co-Leader, Owner
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "team_id": "uuid",
    "user_id": "uuid",
    "role": "Member",
    "joined_at": "timestamp"
  }
  ```

### Update Team Member Role

- **PUT** `/api/teams/{team_id}/members/{user_id}`
- **Description**: Update a team member's role
- **Authentication**: Required (Team Owner only)
- **Request Body**:
  ```json
  {
    "role": "Co-Leader"
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "team_id": "uuid",
    "user_id": "uuid",
    "role": "Co-Leader",
    "updated_at": "timestamp"
  }
  ```

### Remove Team Member

- **DELETE** `/api/teams/{team_id}/members/{user_id}`
- **Description**: Remove a user from a team
- **Authentication**: Required (Team Owner, Co-Leader, or the member themselves)
- **Response**: `204 No Content`

### List Team Members

- **GET** `/api/teams/{team_id}/members`
- **Description**: Get a list of team members with their roles
- **Authentication**: Required
- **Query Parameters**:
  - `role`: Filter by role (Owner, Co-Leader, Member)
  - `search`: Search by name
- **Response**: `200 OK`
  ```json
  {
    "members": [
      {
        "user_id": "uuid",
        "full_name": "Jane Doe",
        "profile_image_url": "url_to_image",
        "role": "Owner",
        "joined_at": "timestamp"
      },
      ...
    ]
  }
  ```

### Team Invitation

### Invite User to Team

- **POST** `/api/teams/{team_id}/invitations`
- **Description**: Send invitation to a user to join a team
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Request Body**:
  ```json
  {
    "email": "user@example.com",
    "role": "Member",
    "message": "Hey, join our awesome team!"
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "email": "user@example.com",
    "role": "Member",
    "expires_at": "timestamp",
    "created_at": "timestamp"
  }
  ```

### List Team Invitations

- **GET** `/api/teams/{team_id}/invitations`
- **Description**: Get pending invitations for a team
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Response**: `200 OK`
  ```json
  {
    "invitations": [
      {
        "id": "uuid",
        "email": "user@example.com",
        "role": "Member",
        "status": "pending",
        "created_at": "timestamp",
        "expires_at": "timestamp"
      },
      ...
    ]
  }
  ```

### Accept Team Invitation

- **POST** `/api/invitations/{invitation_id}/accept`
- **Description**: Accept a team invitation
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "team_id": "uuid",
    "team_name": "Dream Team",
    "user_id": "uuid",
    "role": "Member",
    "joined_at": "timestamp"
  }
  ```

### Reject Team Invitation

- **POST** `/api/invitations/{invitation_id}/reject`
- **Description**: Reject a team invitation
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "message": "Invitation rejected successfully"
  }
  ```

### Cancel Team Invitation

- **DELETE** `/api/teams/{team_id}/invitations/{invitation_id}`
- **Description**: Cancel a pending team invitation
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Response**: `204 No Content`

### Team Analytics

### Get Team Activity Stats

- **GET** `/api/teams/{team_id}/analytics/activity`
- **Description**: Get team activity statistics over time
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Query Parameters**:
  - `period`: Time period (day, week, month, year)
  - `start_date`: Start date for custom period
  - `end_date`: End date for custom period
- **Response**: `200 OK`
  ```json
  {
    "period": "month",
    "data_points": [
      {
        "date": "2023-07-01",
        "tasks_created": 12,
        "tasks_completed": 8,
        "comments": 24,
        "active_members": 5
      },
      ...
    ],
    "totals": {
      "tasks_created": 45,
      "tasks_completed": 32,
      "comments": 87,
      "active_members": 6
    }
  }
  ```

### Get Team Member Performance

- **GET** `/api/teams/{team_id}/analytics/members`
- **Description**: Get performance metrics for team members
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Query Parameters**:
  - `period`: Time period (week, month, quarter, year)
- **Response**: `200 OK`
  ```json
  {
    "period": "month",
    "members": [
      {
        "user_id": "uuid",
        "full_name": "Jane Doe",
        "tasks_assigned": 15,
        "tasks_completed": 12,
        "completion_rate": 80,
        "avg_completion_time": "2.3 days",
        "comments": 18
      },
      ...
    ]
  }
  ```

### Get Team Project Stats

- **GET** `/api/teams/{team_id}/analytics/projects`
- **Description**: Get statistics for team projects
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Response**: `200 OK`
  ```json
  {
    "total_projects": 5,
    "active_projects": 3,
    "completed_projects": 1,
    "on_hold_projects": 1,
    "projects": [
      {
        "id": "uuid",
        "name": "E-commerce Platform",
        "status": "Active",
        "progress": 68,
        "tasks_total": 34,
        "tasks_completed": 23
      },
      ...
    ]
  }
  ```

### Team Settings

### Update Team Settings

- **PUT** `/api/teams/{team_id}/settings`
- **Description**: Update team settings
- **Authentication**: Required (Team Owner only)
- **Request Body**:
  ```json
  {
    "default_member_role": "Member",
    "allow_member_invites": true,
    "require_join_approval": true,
    "visibility": "public"
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "team_id": "uuid",
    "default_member_role": "Member",
    "allow_member_invites": true,
    "require_join_approval": true,
    "visibility": "public",
    "updated_at": "timestamp"
  }
  ```

### Get Team Settings

- **GET** `/api/teams/{team_id}/settings`
- **Description**: Get team settings
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Response**: `200 OK`
  ```json
  {
    "team_id": "uuid",
    "default_member_role": "Member",
    "allow_member_invites": true,
    "require_join_approval": true,
    "visibility": "public",
    "created_at": "timestamp",
    "updated_at": "timestamp"
  }
  ```

### Team Join Requests

### Request to Join Team

- **POST** `/api/teams/{team_id}/join-requests`
- **Description**: Request to join a team
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "message": "I'd like to join your team because..."
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "team_id": "uuid",
    "user_id": "uuid",
    "status": "pending",
    "message": "I'd like to join your team because...",
    "created_at": "timestamp"
  }
  ```

### List Join Requests

- **GET** `/api/teams/{team_id}/join-requests`
- **Description**: Get pending join requests for a team
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Response**: `200 OK`
  ```json
  {
    "requests": [
      {
        "id": "uuid",
        "user": {
          "id": "uuid",
          "full_name": "John Smith",
          "profile_image_url": "url_to_image"
        },
        "message": "I'd like to join your team because...",
        "created_at": "timestamp"
      },
      ...
    ]
  }
  ```

### Approve Join Request

- **POST** `/api/teams/{team_id}/join-requests/{request_id}/approve`
- **Description**: Approve a request to join the team
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Request Body**:
  ```json
  {
    "role": "Member"
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "team_id": "uuid",
    "user_id": "uuid",
    "role": "Member",
    "joined_at": "timestamp"
  }
  ```

### Reject Join Request

- **POST** `/api/teams/{team_id}/join-requests/{request_id}/reject`
- **Description**: Reject a request to join the team
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Response**: `200 OK`
  ```json
  {
    "message": "Join request rejected successfully"
  }
  ```

### Cancel Join Request

- **DELETE** `/api/teams/{team_id}/join-requests/{request_id}`
- **Description**: Cancel a pending join request (by the requester)
- **Authentication**: Required
- **Response**: `204 No Content`

## Projects

### Create Project

- **POST** `/api/teams/{team_id}/projects`
- **Description**: Create a new project for a team
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Request Body**:
  ```json
  {
    "name": "E-commerce Platform",
    "description": "Building an online marketplace",
    "status": "Planning",
    "start_date": "2023-06-01"
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "name": "E-commerce Platform",
    "description": "Building an online marketplace",
    "team_id": "uuid",
    "status": "Planning",
    "start_date": "2023-06-01",
    "end_date": null,
    "created_at": "timestamp"
  }
  ```

### Get Project

- **GET** `/api/projects/{project_id}`
- **Description**: Get project details
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "name": "E-commerce Platform",
    "description": "Building an online marketplace",
    "team": {
      "id": "uuid",
      "name": "Dream Team"
    },
    "status": "Active",
    "start_date": "2023-06-01",
    "end_date": null,
    "task_count": {
      "total": 25,
      "completed": 10
    },
    "created_at": "timestamp"
  }
  ```

### Update Project

- **PUT** `/api/projects/{project_id}`
- **Description**: Update project details
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Request Body**:
  ```json
  {
    "name": "Updated Project Name",
    "description": "Updated description",
    "status": "Active",
    "end_date": "2023-12-31"
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "name": "Updated Project Name",
    "description": "Updated description",
    "status": "Active",
    "end_date": "2023-12-31",
    "updated_at": "timestamp"
  }
  ```

### List Projects

- **GET** `/api/projects`
- **Description**: Get a list of all projects the user has access to
- **Authentication**: Required
- **Query Parameters**:
  - `page`: Page number (default: 1)
  - `limit`: Items per page (default: 20)
  - `search`: Search by name
  - `status`: Filter by status
  - `team_id`: Filter by team
- **Response**: `200 OK`
  ```json
  {
    "total": 12,
    "page": 1,
    "limit": 20,
    "projects": [
      {
        "id": "uuid",
        "name": "E-commerce Platform",
        "team_name": "Dream Team",
        "status": "Active",
        "progress": 40,
        "start_date": "2023-06-01"
      },
      ...
    ]
  }
  ```

### List Team Projects

- **GET** `/api/teams/{team_id}/projects`
- **Description**: Get a list of projects for a specific team
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "projects": [
      {
        "id": "uuid",
        "name": "E-commerce Platform",
        "status": "Active",
        "progress": 40,
        "start_date": "2023-06-01"
      },
      ...
    ]
  }
  ```

### Delete Project

- **DELETE** `/api/projects/{project_id}`
- **Description**: Delete a project
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Response**: `204 No Content`

## Tasks

### Create Task

- **POST** `/api/projects/{project_id}/tasks`
- **Description**: Create a new task for a project
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "title": "Implement user authentication",
    "description": "Create login and registration forms",
    "assigned_to": "user_uuid",
    "priority": "High",
    "due_date": "2023-07-15",
    "estimated_time": "8h"
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "title": "Implement user authentication",
    "description": "Create login and registration forms",
    "project_id": "uuid",
    "assigned_to": "user_uuid",
    "priority": "High",
    "status": "To Do",
    "due_date": "2023-07-15",
    "estimated_time": "8h",
    "actual_time": null,
    "created_at": "timestamp"
  }
  ```

### Get Task

- **GET** `/api/tasks/{task_id}`
- **Description**: Get task details
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "title": "Implement user authentication",
    "description": "Create login and registration forms",
    "project": {
      "id": "uuid",
      "name": "E-commerce Platform"
    },
    "assigned_to": {
      "id": "uuid",
      "full_name": "Jane Doe",
      "profile_image_url": "url_to_image"
    },
    "priority": "High",
    "status": "In Progress",
    "due_date": "2023-07-15",
    "estimated_time": "8h",
    "actual_time": "4h",
    "created_at": "timestamp",
    "updated_at": "timestamp"
  }
  ```

### Update Task

- **PUT** `/api/tasks/{task_id}`
- **Description**: Update task details
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "title": "Updated task title",
    "description": "Updated description",
    "assigned_to": "another_user_uuid",
    "priority": "Medium",
    "status": "In Progress"
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "title": "Updated task title",
    "description": "Updated description",
    "assigned_to": "another_user_uuid",
    "priority": "Medium",
    "status": "In Progress",
    "updated_at": "timestamp"
  }
  ```

### List Tasks

- **GET** `/api/projects/{project_id}/tasks`
- **Description**: Get a list of tasks for a project
- **Authentication**: Required
- **Query Parameters**:
  - `status`: Filter by status
  - `priority`: Filter by priority
  - `assigned_to`: Filter by assigned user
- **Response**: `200 OK`
  ```json
  {
    "tasks": [
      {
        "id": "uuid",
        "title": "Implement user authentication",
        "priority": "High",
        "status": "In Progress",
        "assigned_to": {
          "id": "uuid",
          "full_name": "Jane Doe",
          "profile_image_url": "url_to_image"
        },
        "due_date": "2023-07-15"
      },
      ...
    ]
  }
  ```

### Log Task Progress

- **POST** `/api/tasks/{task_id}/progress`
- **Description**: Log time and notes for a task
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "time_spent": "2h",
    "notes": "Completed the login form design"
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "task_id": "uuid",
    "user_id": "uuid",
    "time_spent": "2h",
    "notes": "Completed the login form design",
    "created_at": "timestamp"
  }
  ```

### Get Task Progress

- **GET** `/api/tasks/{task_id}/progress`
- **Description**: Get progress history for a task
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "progress": [
      {
        "id": "uuid",
        "user": {
          "id": "uuid",
          "full_name": "Jane Doe"
        },
        "time_spent": "2h",
        "notes": "Completed the login form design",
        "created_at": "timestamp"
      },
      ...
    ],
    "total_time_spent": "6h"
  }
  ```

### Delete Task

- **DELETE** `/api/tasks/{task_id}`
- **Description**: Delete a task
- **Authentication**: Required
- **Response**: `204 No Content`

## Messages

### Send Team Message

- **POST** `/api/teams/{team_id}/messages`
- **Description**: Send a message to a team
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "content": "Hello team! Our meeting is scheduled for tomorrow at 10 AM.",
    "reply_to": "message_uuid" // Optional
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "sender_id": "uuid",
    "team_id": "uuid",
    "content": "Hello team! Our meeting is scheduled for tomorrow at 10 AM.",
    "reply_to": "message_uuid",
    "is_pinned": false,
    "sent_at": "timestamp"
  }
  ```

### Get Team Messages

- **GET** `/api/teams/{team_id}/messages`
- **Description**: Get messages for a team
- **Authentication**: Required
- **Query Parameters**:
  - `limit`: Items per page (default: 50)
  - `before`: Get messages before this timestamp
- **Response**: `200 OK`
  ```json
  {
    "messages": [
      {
        "id": "uuid",
        "sender": {
          "id": "uuid",
          "full_name": "Jane Doe",
          "profile_image_url": "url_to_image"
        },
        "content": "Hello team! Our meeting is scheduled for tomorrow at 10 AM.",
        "reply_to": null,
        "is_pinned": false,
        "sent_at": "timestamp"
      },
      ...
    ],
    "has_more": true
  }
  ```

### Pin/Unpin Message

- **PUT** `/api/teams/{team_id}/messages/{message_id}/pin`
- **Description**: Pin or unpin a message
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Request Body**:
  ```json
  {
    "is_pinned": true
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "is_pinned": true,
    "updated_at": "timestamp"
  }
  ```

### Get Pinned Messages

- **GET** `/api/teams/{team_id}/messages/pinned`
- **Description**: Get pinned messages for a team
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "messages": [
      {
        "id": "uuid",
        "sender": {
          "id": "uuid",
          "full_name": "Jane Doe"
        },
        "content": "Important announcement: New project kickoff next Monday!",
        "sent_at": "timestamp"
      },
      ...
    ]
  }
  ```

### Send Direct Message

- **POST** `/api/messages/direct`
- **Description**: Send a direct message to a user
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "recipient_id": "user_uuid",
    "content": "Hey, do you have time to review my PR?"
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "sender_id": "uuid",
    "recipient_id": "user_uuid",
    "content": "Hey, do you have time to review my PR?",
    "is_read": false,
    "sent_at": "timestamp"
  }
  ```

### Get Direct Message Conversations

- **GET** `/api/messages/direct/conversations`
- **Description**: Get list of direct message conversations
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "conversations": [
      {
        "user": {
          "id": "uuid",
          "full_name": "John Smith",
          "profile_image_url": "url_to_image"
        },
        "last_message": {
          "content": "Hey, do you have time to review my PR?",
          "sent_at": "timestamp",
          "is_read": false,
          "is_from_me": true
        },
        "unread_count": 0
      },
      ...
    ]
  }
  ```

### Get Direct Messages with User

- **GET** `/api/messages/direct/users/{user_id}`
- **Description**: Get direct messages with a specific user
- **Authentication**: Required
- **Query Parameters**:
  - `limit`: Items per page (default: 50)
  - `before`: Get messages before this timestamp
- **Response**: `200 OK`
  ```json
  {
    "messages": [
      {
        "id": "uuid",
        "sender_id": "uuid",
        "recipient_id": "user_uuid",
        "content": "Hey, do you have time to review my PR?",
        "is_read": true,
        "sent_at": "timestamp"
      },
      ...
    ],
    "has_more": false
  }
  ```

### Mark Direct Message as Read

- **PUT** `/api/messages/direct/{message_id}/read`
- **Description**: Mark a direct message as read
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "is_read": true,
    "updated_at": "timestamp"
  }
  ```

## Channels

### Create Channel

- **POST** `/api/teams/{team_id}/channels`
- **Description**: Create a new channel in a team
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Request Body**:
  ```json
  {
    "name": "frontend-dev",
    "description": "Channel for frontend development discussions",
    "is_private": false
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "team_id": "uuid",
    "name": "frontend-dev",
    "description": "Channel for frontend development discussions",
    "is_private": false,
    "created_at": "timestamp"
  }
  ```

### Get Channel

- **GET** `/api/channels/{channel_id}`
- **Description**: Get channel details
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "team_id": "uuid",
    "name": "frontend-dev",
    "description": "Channel for frontend development discussions",
    "is_private": false,
    "created_at": "timestamp"
  }
  ```

### Update Channel

- **PUT** `/api/channels/{channel_id}`
- **Description**: Update channel details
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Request Body**:
  ```json
  {
    "name": "frontend-developers",
    "description": "Updated description"
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "name": "frontend-developers",
    "description": "Updated description",
    "updated_at": "timestamp"
  }
  ```

### List Team Channels

- **GET** `/api/teams/{team_id}/channels`
- **Description**: Get channels for a team
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "channels": [
      {
        "id": "uuid",
        "name": "general",
        "description": "General discussion",
        "is_private": false
      },
      {
        "id": "uuid",
        "name": "frontend-dev",
        "description": "Channel for frontend development discussions",
        "is_private": false
      },
      ...
    ]
  }
  ```

### Send Channel Message

- **POST** `/api/channels/{channel_id}/messages`
- **Description**: Send a message to a channel
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "content": "I've updated the UI components, please review",
    "reply_to": "message_uuid" // Optional
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "channel_id": "uuid",
    "sender_id": "uuid",
    "content": "I've updated the UI components, please review",
    "reply_to": "message_uuid",
    "sent_at": "timestamp"
  }
  ```

### Get Channel Messages

- **GET** `/api/channels/{channel_id}/messages`
- **Description**: Get messages for a channel
- **Authentication**: Required
- **Query Parameters**:
  - `limit`: Items per page (default: 50)
  - `before`: Get messages before this timestamp
- **Response**: `200 OK`
  ```json
  {
    "messages": [
      {
        "id": "uuid",
        "sender": {
          "id": "uuid",
          "full_name": "Jane Doe",
          "profile_image_url": "url_to_image"
        },
        "content": "I've updated the UI components, please review",
        "reply_to": null,
        "sent_at": "timestamp"
      },
      ...
    ],
    "has_more": true
  }
  ```

### Delete Channel

- **DELETE** `/api/channels/{channel_id}`
- **Description**: Delete a channel
- **Authentication**: Required (Team Owner or Co-Leader only)
- **Response**: `204 No Content`

## Challenges

### Create Challenge

- **POST** `/api/challenges`
- **Description**: Create a new challenge
- **Authentication**: Required (Admin only)
- **Request Body**:
  ```json
  {
    "title": "Build a Weather App",
    "description": "Create a web app that displays weather information from a public API",
    "difficulty": "Medium",
    "points": 100,
    "start_date": "2023-07-01",
    "end_date": "2023-07-15"
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "title": "Build a Weather App",
    "description": "Create a web app that displays weather information from a public API",
    "difficulty": "Medium",
    "points": 100,
    "start_date": "2023-07-01",
    "end_date": "2023-07-15",
    "created_at": "timestamp"
  }
  ```

### Get Challenge

- **GET** `/api/challenges/{challenge_id}`
- **Description**: Get challenge details
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "title": "Build a Weather App",
    "description": "Create a web app that displays weather information from a public API",
    "difficulty": "Medium",
    "points": 100,
    "start_date": "2023-07-01",
    "end_date": "2023-07-15",
    "submission_count": 12,
    "created_at": "timestamp"
  }
  ```

### List Challenges

- **GET** `/api/challenges`
- **Description**: Get a list of challenges
- **Authentication**: Required
- **Query Parameters**:
  - `page`: Page number (default: 1)
  - `limit`: Items per page (default: 20)
  - `difficulty`: Filter by difficulty
  - `status`: Filter by status (active, upcoming, completed)
- **Response**: `200 OK`
  ```json
  {
    "total": 8,
    "page": 1,
    "limit": 20,
    "challenges": [
      {
        "id": "uuid",
        "title": "Build a Weather App",
        "difficulty": "Medium",
        "points": 100,
        "status": "active",
        "end_date": "2023-07-15",
        "submission_count": 12
      },
      ...
    ]
  }
  ```

### Submit Challenge Solution

- **POST** `/api/challenges/{challenge_id}/submissions`
- **Description**: Submit a solution for a challenge
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "submission_url": "https://github.com/username/weather-app"
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "challenge_id": "uuid",
    "user_id": "uuid",
    "submission_url": "https://github.com/username/weather-app",
    "submitted_at": "timestamp"
  }
  ```

### Grade Challenge Submission

- **PUT** `/api/challenges/submissions/{submission_id}/grade`
- **Description**: Grade a challenge submission
- **Authentication**: Required (Admin only)
- **Request Body**:
  ```json
  {
    "score": 85,
    "feedback": "Good work! Consider adding error handling for API requests."
  }
  ```
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "score": 85,
    "feedback": "Good work! Consider adding error handling for API requests.",
    "updated_at": "timestamp"
  }
  ```

### Get User Submissions

- **GET** `/api/users/me/challenge-submissions`
- **Description**: Get user's challenge submissions
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "submissions": [
      {
        "id": "uuid",
        "challenge": {
          "id": "uuid",
          "title": "Build a Weather App",
          "difficulty": "Medium",
          "points": 100
        },
        "submission_url": "https://github.com/username/weather-app",
        "score": 85,
        "feedback": "Good work! Consider adding error handling for API requests.",
        "submitted_at": "timestamp"
      },
      ...
    ]
  }
  ```

### Get Challenge Submissions

- **GET** `/api/challenges/{challenge_id}/submissions`
- **Description**: Get submissions for a challenge
- **Authentication**: Required (Admin only)
- **Response**: `200 OK`
  ```json
  {
    "submissions": [
      {
        "id": "uuid",
        "user": {
          "id": "uuid",
          "full_name": "Jane Doe"
        },
        "submission_url": "https://github.com/username/weather-app",
        "score": 85,
        "submitted_at": "timestamp"
      },
      ...
    ]
  }
  ```

### Get Leaderboard

- **GET** `/api/leaderboard`
- **Description**: Get global leaderboard
- **Authentication**: Required
- **Query Parameters**:
  - `limit`: Number of entries (default: 100)
- **Response**: `200 OK`
  ```json
  {
    "leaderboard": [
      {
        "rank": 1,
        "user": {
          "id": "uuid",
          "full_name": "Jane Doe",
          "profile_image_url": "url_to_image"
        },
        "points": 450,
        "challenges_completed": 5
      },
      ...
    ]
  }
  ```

## Ideas

### Create Idea

- **POST** `/api/ideas`
- **Description**: Submit a new idea
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "title": "Code Review Bot",
    "description": "A bot that automatically reviews code and suggests improvements",
    "category": "Productivity"
  }
  ```
- **Response**: `201 Created`
  ```json
  {
    "id": "uuid",
    "user_id": "uuid",
    "title": "Code Review Bot",
    "description": "A bot that automatically reviews code and suggests improvements",
    "category": "Productivity",
    "status": "New",
    "votes_count": 0,
    "created_at": "timestamp"
  }
  ```

### Get Idea

- **GET** `/api/ideas/{idea_id}`
- **Description**: Get idea details
- **Authentication**: Required
- **Response**: `200 OK`
  ```json
  {
    "id": "uuid",
    "title": "Code Review Bot",
    "description": "A bot that automatically reviews code and suggests improvements",
    "category": "Productivity",
    "user": {
      "id": "uuid",
      "full_name": "Jane Doe",
      "profile_image_url": "url_to_image"
    },
    "status": "New",
    "votes_count": 10,
    "created_at": "timestamp",
    "updated_at": "timestamp"
  }
  ```

### List Ideas

- **GET** `/api/ideas`
- **Description**: Get a list of ideas
- **Authentication**: Required
- **Query Parameters**:
  - `page`: Page number (default: 1)
  - `limit`: Items per page (default: 20)
  - `category`: Filter by category
  - `status`: Filter by status
  - `sort`: Sort by (votes, newest, oldest)
- **Response**: `200 OK`
  ```json
  {
    "total": 18,
    "page": 1,
    "limit": 20,
    "ideas": [
      {
        "id": "uuid",
        "title": "Code Review Bot",
        "category": "Productivity",
        "user": {
          "id": "uuid",
          "full_name": "Jane Doe"
        },
        "votes_count": 10,
        "status": "New",
        "created_at": "timestamp"
      },
      ...
    ]
  }
  ```

### Update Idea

- **PUT** `/api/ideas/{idea_id}`
- **Description**: Update an idea (owner or admin only)
- **Authentication**: Required
- **Request Body**:
  ```json
  {
    "title": "Updated Idea Title",
    "description": "Updated description",
    "category": "Development"
  }
  ```
