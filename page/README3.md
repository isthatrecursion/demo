To create and test a CI pipeline using GitHub Actions.

## Step 1: Create a Repository

1. Open [GitHub](https://github.com/) and sign in.
2. Click **New repository**.
3. Enter the repository name `CI-CD-Demo`.
4. Click **Create repository**.

## Step 2: Create `index.html`

1. Open your repository.
2. Click **Add file → Create new file**.
3. Enter the filename `index.html`.
4. Paste the following code:

```html
<html>
<body>
    <h1>CI Demo</h1>
</body>
</html>
```

5. Click **Commit changes**.

## Step 3: Open the Actions Tab

1. Open your repository.
2. Click the **Actions** tab.
3. Click **New workflow**.
4. Select **set up a workflow yourself**.

## Step 4: Create `main.yml`

Create the workflow file with the following path:

`.github/workflows/main.yml`

Paste the following YAML code:

```yaml
name: CI Pipeline

on: push

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
      - run: echo "Started"
      - run: pwd
      - run: ls
```

Click **Commit changes**.

## Step 5: Check the Workflow

1. Click the **Actions** tab.
2. Select **CI Pipeline**.
3. Open the latest workflow run.
4. Click the `build` job.

Expected output:

```text
Started
```

A green tick indicates that the workflow completed successfully.

## Step 6: Modify `index.html`

1. Return to the **Code** tab.
2. Open `index.html`.
3. Click the pencil icon to edit the file.
4. Change the heading to:

```html
<h1>CI Pipeline Updated</h1>
```

5. Click **Commit changes**.

## Step 7: Check the New Run

1. Return to the **Actions** tab.
2. Open the latest workflow run.
3. Verify that the new commit triggered the workflow automatically.
4. Check the `build` job for successful execution.

## Result

Successfully created and tested a Continuous Integration (CI) pipeline using GitHub Actions. The workflow runs automatically whenever a push event occurs in the repository.