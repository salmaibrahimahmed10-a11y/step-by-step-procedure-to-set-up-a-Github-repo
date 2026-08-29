# Technical Writing Lab

## Exercise A: User Manual Procedure

### Setting Up a GitHub Repository and Making a First Commit

#### Prerequisites

Before starting, you need a GitHub account, Git installed on your computer, a terminal or command prompt, an internet connection, and a project folder containing at least one file.

#### Procedure

**Step 1: Sign in to GitHub.**

Open GitHub in your web browser and sign in to your account.

**Expected result:** Your GitHub account page opens successfully.

**Step 2: Create a new repository.**

Click the option to create a new repository and enter a name for the repository.

**Expected result:** The new repository form is displayed with the repository name entered.

**Step 3: Set the repository visibility to Public.**

Select the Public option under repository visibility.

**Expected result:** The repository is set to Public.

**Step 4: Create the repository.**

Click the Create repository button.

**Expected result:** GitHub opens the new empty repository page.

**Step 5: Open the terminal.**

Open Terminal on macOS or Command Prompt/Git Bash on Windows.

**Expected result:** A command-line window opens and displays a command prompt.

**Step 6: Navigate to the project folder.**

Use the cd command to move into the project folder.

```bash
cd ~/python_lab


Expected result: The terminal is now working inside the project folder.

**Step 7: Initialise the Git repository.**
git init
**Expected result:** Git creates a new local repository in the project folder.

**Step 8: Stage the project files.**
git add .
**Expected result:** The project files are added to the Git staging area.

**Step 9: Create the first commit.**
git commit -m "Initial project setup"
**Expected result:** Git creates the first commit and displays a summary of the committed files.

**Step 10: Connect the local repository to GitHub.**

Run the following command using the HTTPS address of your GitHub repository:
git remote add origin https://github.com/USERNAME/REPOSITORY.git
**Expected result:** The local repository is connected to the GitHub repository through a remote named origin.

**Step 11: Push the project to GitHub.**
git push -u origin main
**Expected result:** The project files and the first commit are uploaded to the main branch on GitHub.

#### Screenshot Description

I would include a screenshot of the GitHub repository after the first push. The screenshot should show the repository name, the uploaded project files, and the commit history. This would show that the local project was successfully connected to GitHub and uploaded.

##### Troubleshooting

One common error for beginners is src refspec main does not match any when trying to push. This can happen when there is no commit yet or when the local branch is not named main. First, make sure that a commit has been created. Then check the current branch with git branch. If necessary, rename the branch to main using:
git branch -M main
After that, try the push command again.

## Exercise B: API Reference Entry

### Create a New Task

#### Description

This endpoint is used to create a new task in a project management application. The user must be authenticated before creating a task. A task must have a title, an assignee, a due date, and a priority level. The description is optional.

#### HTTP Method and Endpoint

**Method:** `POST`

**Endpoint:** `/api/v1/projects/{projectId}/tasks`

#### Path Parameter

| Name | Data Type | Required | Description |
|---|---|---|---|
| `projectId` | string | Yes | The ID of the project where the new task will be created. |

#### Request Body Parameters

| Name | Data Type | Required | Description |
|---|---|---|---|
| `title` | string | Yes | The name of the task. |
| `description` | string | No | Extra information about the task. |
| `assigneeId` | string | Yes | The ID of the user who will be assigned the task. |
| `dueDate` | string | Yes | The date when the task should be completed, using the `YYYY-MM-DD` format. |
| `priority` | string | Yes | The priority of the task. It can be `low`, `medium`, or `high`. |

#### Request Headers

The request must include the following headers:

- `Authorization` - Required. Contains the user's access token.
- `Content-Type` - Required. Shows that the request body is in JSON format.

Example:

```http
Authorization: Bearer <access_token>
Content-Type: application/json

#### Example Request body

  {"title": "Complete project documentation",
  "description": "Finish writing the project documentation.",
  "assigneeId": "usr_1042",
  "dueDate": "2026-09-15",
  "priority": "high"}

#### Possible Response Codes

| Status Code | Meaning |
|---|---|
| `201 Created` | The task was created successfully. |
| `400 Bad Request` | Some required information is missing or entered incorrectly. |
| `401 Unauthorized` | The user is not authenticated or the access token is invalid. |
| `403 Forbidden` | The user is authenticated but does not have permission to create a task in the project. |
| `404 Not Found` | The project or user ID could not be found. |
| `409 Conflict` | The new task conflicts with existing information. |
| `500 Internal Server Error` | Something went wrong on the server. |

#### example successful response

  {"id": "task_7821",
  "projectId": "proj_204",
  "title": "Complete project documentation",
  "description": "Finish writing the project documentation.",
  "assigneeId": "usr_1042",
  "dueDate": "2026-09-15",
  "priority": "high",
  "status": "pending",
  "createdAt": "2026-08-27T12:30:00Z"}


