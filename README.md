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

5. Features:

-> Basic Functionality:

    Runs Python code on request

    Returns output and error messages as JSON

-> Safety Improvements

    Execution timeout:

    Memory limit

    CPU limit

    Network isolation

    Read-only filesystem

    Temporary writable directory (/tmp)

    Code length validation (maximum 5000 characters)

    Clear and meaningful error messages

-> Docker Security Experiments

    Read access to internal system files (such as /etc/passwd)

    Write attempts blocked outside /tmp

    Understanding what Docker isolates and what it does not

6. Requirements:

  -> Python 3

  -> Docker Desktop

  -> pip packages:

      Flask

      flask-cors

7. Setup Instructions:

  -> Install required Python packages.

  -> Start Docker Desktop.

  -> Run the API server using:

          python app.py
          
  -> The API will run on:

      http://127.0.0.1:5000
      
8. Testing the System:

  -> Basic Tests

        Print statements
        
              <img width="1200" height="216" alt="Screenshot 2025-12-11 044128" src="https://github.com/user-attachments/assets/db9cdc01-                72a5-473d-b56a-6c2833033f39" />

        Arithmetic operations

        Simple loops


   -> Safety Tests

        Infinite loop should timeout

        Memory-heavy code should be killed

        Network requests should fail

        File writes should fail on read-only filesystem

        File writes to /tmp should succeed

    -> Docker Behavior Tests

        Reading /etc/passwd should work

        Writing to protected directories should fail

        Temporary writes inside /tmp should work
        
9. API Summary;

    -> Endpoint: POST /run
   
    -> Request body must include a "code" field containing Python code.
   
    -> Response contains:

          output – printed output

          errors – Python errors or sandbox violations

    -> Error cases include:

          Missing code

          Code exceeding character limit

          Timeout

          Memory kill

          Network blocked

          Read-only filesystem errors

10. What I Learned:

    How to run untrusted code in a safe environment

    How to apply Docker’s resource limits and isolation

    Why network and filesystem restrictions are important

    How online code execution systems protect themselves

    How to design clean and clear API responses

    How to document and structure a backend project

11. Conclusion:

  This project demonstrates a complete workflow for building a secure code execution sandbox using Docker and Python. It covers backend
  
  development, container security, safe execution practices, and practical DevOps concepts. The system is fully documented, testable, and
  
  ready for demonstration.

