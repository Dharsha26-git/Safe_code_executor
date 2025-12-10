                                                Safe Code Executor


1. Project Overview:

  The API accepts Python code through a POST request and executes it inside a sandboxed Docker environment.

  The sandbox is heavily restricted to prevent harmful behavior such as infinite loops, memory abuse, network access, and filesystem
  
  modifications.

The purpose of the project is to understand:

-> How to execute untrusted code safely

-> How Docker provides process isolation

-> How to enforce limits such as timeout, memory, CPU, and read-only filesystem

-> How real-world code execution platforms operate internally.

2. Project Goals:

-> Build an API that runs Python code.

-> Run submitted code inside a Docker container.

-> Add safety controls to handle malicious or faulty code.

-> Study Docker’s security boundaries.

-> Create basic documentation and a simple web UI for testing.

3. Project Structure:

  Safe-exec/

  ├── app.py 

  ├── runner.py 

  └── index.html

4. How the System Works:

-> User submits Python code to the API.

-> The backend stores the code in a temporary file.

-> A Docker container is launched with strict security flags:

. No network access

. Limited memory usage

. Limited CPU usage

. Read-only filesystem

. Only /tmp is writable

-> The code runs inside the container.

-> Standard output and errors are captured.

-> The API returns the results in JSON format.

-> A simple HTML file allows users to test the API from the browser.
