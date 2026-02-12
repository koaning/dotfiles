# Conductor Setup

This skill helps you create a `conductor.json` file for your project.

## What is conductor.json?

The `conductor.json` file lives in your project's root directory and tells Conductor how to set up, run, and manage workspaces. It contains a `scripts` object with three fields:

```json
{
  "scripts": {
    "setup": "",
    "run": "",
    "archive": ""
  }
}
```

### Fields

- **setup**: Runs automatically when a new workspace is created. Use this to install dependencies, copy environment files, run migrations, or any other initialization your project needs.
- **run**: The command to start your development server or main process.
- **archive**: Runs when a workspace is archived. Use this to clean up resources like stopping background services or removing temporary files.

### Example

For a Python/Django project using uv:

```json
{
  "scripts": {
    "setup": "cp $CONDUCTOR_ROOT_PATH/.env . && uv sync && uv run python manage.py migrate",
    "run": "uv run python manage.py runserver",
    "archive": ""
  }
}
```

For a Node.js project it might look like:

```json
{
  "scripts": {
    "setup": "cp $CONDUCTOR_ROOT_PATH/.env . && npm install",
    "run": "npm run dev",
    "archive": ""
  }
}
```

## Environment Variables

Conductor exposes several environment variables that you can use in your scripts:

| Variable | Description |
|---|---|
| `CONDUCTOR_WORKSPACE_NAME` | Name of the current workspace |
| `CONDUCTOR_WORKSPACE_PATH` | Path to the current workspace |
| `CONDUCTOR_ROOT_PATH` | Path to the repository root directory |
| `CONDUCTOR_DEFAULT_BRANCH` | Name of the default branch (defaults to `main`) |
| `CONDUCTOR_PORT` | First in a range of 10 ports assigned to the workspace |

These are available in both terminals and scripts, so you can use them to dynamically reference paths and avoid port conflicts across workspaces. For example, `$CONDUCTOR_ROOT_PATH/.env` references the `.env` file in your repo root, letting each workspace copy it during setup.
