# Participant Data Verification Python Script

This Python script is used to verify participant data from an Excel sheet. It checks if participant handles exist on different online platforms like GeeksForGeeks, Codeforces, LeetCode, CodeChef, and HackerRank. The verification process is logged in a text file, and verified participant details are stored in a CSV file.

## How to Use:

### `main.py`

- **What it does:** Loads participant data, checks handle existence, logs the process, and generates a CSV file with verified details.
- **How to run:** Simply execute `main.py` in your Python environment.

### `builder.yml`

- **What it does:** Automates the process of running `main.py`, committing generated files, and pushing changes to the repository using GitHub Actions.
- **How to use:** Just add this file to your GitHub repository under the `.github/workflows` directory.

## How it Works:

### `main.py`

1. **Load Data**: Reads participant data from an Excel sheet.
2. **Check Handles**: Verifies participant handles on various platforms using HTTP requests.

   * This function is responsible for checking the existence of participant handles on various online platforms. It utilizes HTTP requests to determine if the provided URLs are valid and accessible. Here's a detailed explanation of how it works:
    
    1. **Input Parameter**:
            - `url`: The URL to be checked for existence.

    2. **Functionality**:

       - **LeetCode URL Check**:
         - If the URL starts with "https://leetcode.com/", it checks if the URL returns a valid response (status code 200). LeetCode handles are verified by checking the HTTP response status.
         - Leetcode always returns a 404 status code for non-existing handles. So, if the status code is 404, it means the handle does not exist.
 
       - **Other Platforms URL Check**:
         - For other platforms (GeeksForGeeks, Codeforces, CodeChef, HackerRank), it constructs a custom HTTP request with a user-agent header to simulate a web browser request.
         - It then sends an HTTP GET request to the provided URL and checks the response status code.
         - If the status code is 200, it means the URL exists and is accessible.
         - Additionally, it checks if the URL has been redirected to specific pages associated with non-existing handles on the platforms.
 
       - **Handling Redirects**:
         - For certain platforms like Codeforces and GeeksForGeeks, the function checks if the final URL after redirection matches specific patterns associated with non-existing handles.
         - For example, if the final URL for Codeforces is "https://codeforces.com/", it indicates that the handle does not exist.
         - Similarly, for GeeksForGeeks, if the final URL is "https://auth.geeksforgeeks.org/?to=https://auth.geeksforgeeks.org/profile.php", it implies that the handle does not exist.
 
       - **Exception Handling**:
         - The function catches any exceptions that may occur during the HTTP request process and returns a default value ("Exception") to indicate an error.

   3. **Output**:
      - The function returns a tuple containing a boolean value indicating whether the URL exists (`True` for existence, `False` for non-existence) and the final URL after any redirection.

3. **Log Process**: Logs the verification process and results in a text file (`log.txt`).
4. **Generate CSV**: Creates a CSV file (`participant_details.csv`) with verified participant details.

### `builder.yml`

1. **Set Up Environment**: Prepares the Python environment for execution.
2. **Install Dependencies**: Installs required Python packages.
3. **Run Script**: Executes the Python script to verify participant data.
4. **Commit and Push**: Saves generated files (`participant_details.csv`, `log.txt`) to the repository.

