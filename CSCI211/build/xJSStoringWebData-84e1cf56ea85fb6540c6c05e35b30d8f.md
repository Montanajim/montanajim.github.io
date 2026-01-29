# Storing Web Data

All three, cookies, local storage, and session storage, are mechanisms for storing data related to web browsing. They differ in where the data is stored, persistence, accessibility, and use cases.

**Cookies:**

- **Storage:** On the user's device (client-side)
- **Persistence:**  Varies. Cookies can have an expiration date set by the server or persist until manually cleared by the user.
- **Accessibility:** Accessible by both the client (browser) and the server (website). When a browser requests a web page from a server that previously sent a cookie, the browser includes the cookie in the request.
- **Use cases:**  - Remembering user preferences (e.g., language) - Session management (e.g., shopping cart contents) - Tracking user behavior (e.g., analytics)

**Local Storage:**

- **Storage:** On the user's device (client-side)
- **Persistence:** Persistent until manually cleared by the user or until storage quota is reached.
- **Accessibility:** Accessible only by the client (browser) for the specific website that created it. Isolated from other websites and server-side scripts.
- **Use cases:**  - Storing user preferences (e.g., location) - Application data (e.g., to-do list items)

**Session Storage:**

- **Storage:** On the user's device (client-side)
- **Persistence:** Temporary. Data is cleared when the browser tab or window is closed.
- **Accessibility:** Accessible only by the client (browser) for the specific website and tab/window that created it.
- **Use cases:**  - Caching temporary data (e.g., form input during multi-step process)

Here's a table summarizing the key differences:

| Feature       | Cookies              | Local Storage         | Session Storage |
| ------------- | -------------------- | --------------------- | --------------- |
| Storage       | Client-side          | Client-side           | Client-side     |
| Persistence   | Varies               | Persistent            | Session only    |
| Accessibility | Client & Server      | Client only           | Client only     |
| Use cases     | Preferences, Session | Preferences, App data | Temporary data  |



## Lecture Code



### cookiefunctions.js Explanation

Here's a breakdown of the functions:

1. **checkCookie (demo only):** (commented out for other projects)
   - This function retrieves a cookie named "firstName" using the `getCookie` function.
   - It then constructs a welcome message using the retrieved name. (The name itself might be set elsewhere in the main code).
   - It uses console logs (for testing) and DOM manipulation to show/hide welcome messages and an input field based on whether a name is found in the cookie.
1. **setCookie(cookieName, cookieValue, expireDays):**
   - This function creates a cookie with a specified name, value, and expiry time in days.
   - It creates a date object set to the current time plus the provided number of days in milliseconds.
   - It formats the expiry date in the required format for cookies.
   - Finally, it sets the document's cookie with the name, value, and expiry information.
1. **getCookie(cookieName):**
   - This function retrieves a cookie with a specified name.
   - It splits the entire cookie string (which can contain multiple cookies) into an array by semicolons (';').
   - It iterates through the cookie array, searching for each cookie that starts with the provided name.
   - If a matching cookie is found, it extracts the value after the name and returns it.
   - Otherwise, it returns an empty string.
1. **deleteCookie(cookieName):**
   - This function deletes a cookie with a specified name.
   - It creates a date object set to one day in the past (effectively expiring the cookie).
   - It formats the expiry date in the required format for cookies.
   - Finally, it sets the document's cookie with the name, an empty value, and the past expiry date, essentially deleting it.

```javascript
// this is for the demo
// remove if used in other projects
window: onload = checkCookie;

function setCookie(cookieName, cookieValue, expireDays) {

    let d = new Date();
    // days to milliseconds
    d.setTime(d.getTime() + (expireDays * 24 * 60 * 60 * 1000));

    let expires = "expires=" + d.toGMTString();

    document.cookie = cookieName + "=" + cookieValue + ";" + expires;

    // dogname=fido;1232023203
}

// retreive a cookie
function getCookie(cookieName) {
    let name = cookieName + "=";

    let cookieArray = document.cookie.split(';');

    for (let i = 0; i < cookieArray.length; i++) {

        let c = cookieArray[i].trim();

        if (c.indexOf(name) == 0) {
            // testing only
            console.log("Cookie name is " + c.substring(name.length, c.length));

            // actual code
            return c.substring(name.length, c.length);
        }
    }

    return "";

}

function deleteCookie(cookieName) {
    let d = new Date();
    let cookieValue = "";

    d.setTime(d.getTime() + (-1000));

    let expires = "expires=" + d.toGMTString();

    document.cookie = cookieName + "=" + cookieValue + ";" + expires;

}

// for demo only
function checkCookie() {

    // person is written in main file
    let user = getCookie("firstName");
    let message = "Welcome Back " + user + " we've missed you.";

    // for testing only
    console.log(message);

    if (user != "") {
        document.getElementById("EnterName").style.display = "none";
        document.getElementById("Welcome").style.display = "block";
        document.getElementById("p1").innerHTML = message;

    }
    else {
        document.getElementById("EnterName").style.display = "block";
        document.getElementById("Welcome").style.display = "none";
    }

}
```



### index.html Explanation

This code snippet appears to be an HTML form that demonstrates the usage of cookies, local storage, and session storage. Here's a breakdown of the code:

**HTML Structure:**

- The code defines a basic HTML page with a form and buttons.
- The form has fields for first name, last name, and city.
- There are buttons to delete cookies, local storage, and session storage.
- There's also a link to a second page ("Page 2").

**JavaScript Functions:**

- validateForm():
  - This function is called when the form is submitted.
  - It retrieves the values from the form fields for first name, last name, and city.
  - It calls the `setCookie` function to store these values in cookies with an expiry time of 20 days.
  - It uses `localStorage.setItem` to store the values in local storage (no expiry).
  - It uses `sessionStorage.setItem` to store the values in session storage (expires when the tab closes).
  - The function returns true, allowing the form submission to proceed.
- deleteCookies():
  - This function calls the `deleteCookie` function (cookiefunctions.js`) to delete the cookies named "firstName", "lastName", and "city".
- deleteLocalStorage():
  - This function uses `localStorage.clear()` to remove all items from local storage. (Alternatively, it could use `localStorage.removeItem` to target specific items).
- deleteSessionStorage():
  - This function uses `sessionStorage.clear()` to remove all items from session storage. (Alternatively, it could use `sessionStorage.removeItem` to target specific items).

**Overall Functionality:**

- When the user enters their information and submits the form, the data is stored in cookies (with expiry), local storage (no expiry), and session storage (expires with the tab).
- The buttons allow the user to delete the stored data from cookies, local storage, or session storage independently.
- There's a link to a second page ("Page 2") but it's unclear how this page might interact with the stored data.

This code provides a basic example of using these data storage mechanisms in a web page. In a real application, you'd likely want to consider the appropriate storage method based on the type of data and how long you need it to persist.



![image-20240426155445805](assets/image-20240426155445805-1714168488778-1.png)



![image-20240426155806240](assets/image-20240426155806240-1714168689001-3.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Page 1</title>
    <script src="cookiefunctions.js" type="text/javascript"></script>

    <style>
        .theContent {
            width: 40%;
            margin: 100px auto;
            background-color: bisque;
            padding: 40px;
            color: black;
        }
    </style>



    <script>

        function validateForm() {

            let xfname, xlname, xcity;

            xfname = document.getElementById("fname").value;
            xlname = document.getElementById("lname").value;
            xcity = document.getElementById("city").value;

            // set cookies - expires by time
            setCookie("firstName", xfname, 20);
            setCookie("lastName", xlname, 20);
            setCookie("city", xcity, 20);

            // set localstorage - no expiration date
            localStorage.setItem("firstName", xfname);
            localStorage.setItem("lastName", xlname);
            localStorage.setItem("city", xcity);

            // set set session storage
            sessionStorage.setItem("firstName", xfname);
            sessionStorage.setItem("lastName", xlname);
            sessionStorage.setItem("city", xcity);

            return true;

        }

        function deleteCookies() {
            deleteCookie("firstName");
            deleteCookie("lastName");
            deleteCookie("city");

        }

        function deleteLocalStorage() {
            // clear them all
            localStorage.clear();

            // delete one item;
            //localStorage.removeItem("firstName");
        }

        function deleteSessionStorage() {
            sessionStorage.clear();

            // delete one
            // sessionStorage.removeItem("firstName");
        }

    </script>


</head>

<body>
    <div class="theContent">
        <h1>Persistent Data</h1>
        <div id="Welcome">
            <p id="p1"></p>
        </div>

        <div id="EnterName">

            <p>Local Storage = no expiration date</p>
            <p>Session Storage = expires when the tab is closed</p>
            <p>Cookie Storage = expires by date or when user delete history/cookies</p>


            <form onsubmit="return validateForm()" action="">

                <table border="1">
                    <tr>
                        <td><label for="fname">First Name</label></td>
                        <td><input type="text" name="fname" id="fname" 
                            value="Bob" size="25"></td>
                    </tr>
                    <tr>
                        <td><label for="lname">Last Name</label></td>
                        <td><input type="text" name="lname" id="lname" 
                            value="Smith" size="25"></td>
                    </tr>
                    <tr>
                        <td><label for="city">City</label></td>
                        <td><input type="text" name="city" id="city" 
                            value="Kalispell" size="25"></td>
                    </tr>
                    <tr>
                        <td></td>
                        <td><input type="submit" value="Enter" size="25"></td>
                    </tr>

                </table>

            </form>


        </div>
        <br>
        <button onclick="deleteCookies()">Delete Cookies</button><br><br>
        <button onclick="deleteLocalStorage()">Delete Local Storage</button><br><br>
        <button onclick="deleteSessionStorage()">Delete Session Storage</button><br><br>
        <a href="page2.html">Page 2</a>
    </div>
</body>

</html>
```



### page2.html Explanation

The second page ("Page 2") of the same website. This page focuses on displaying the information stored in cookies, local storage, and session storage.

Here's a breakdown of the code:

**HTML Structure:**

- The structure is similar to the previous page with a "theContent" class for styling.
- It has a link back to the homepage ("index.html").
- There are sections for "Cookie Information," "Local Storage Information," and "Session Storage Information".
- Each section has empty spans with IDs for displaying retrieved data.

**JavaScript:**

- The code retrieves the values from cookies, local storage, and session storage using the same functions (`getCookie`, `localStorage.getItem`, and `sessionStorage.getItem`) as in the previous page.
- It then finds the corresponding span elements using their IDs and sets their innerHTML content to the retrieved values.

**Overall Functionality:**

- This page retrieves the data previously stored on the first page and displays it in separate sections for cookies, local storage, and session storage.
- This allows the user to see what information is stored using each mechanism.

In essence, this code demonstrates how to access and display data stored on the previous page ("Page 1") using cookies, local storage, and session storage.



![image-20240426155913700](assets/image-20240426155913700-1714168756834-5-1714168758859-7.png)



```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Page 2</title>
    <script src="cookiefunctions.js" type="text/javascript"></script>

    <style>
        .theContent {
            width: 40%;
            margin: 100px auto;
            background-color: bisque;
            padding: 40px;
            color: black;
        }
    </style>
</head>

<body>
    <div class="theContent">
        <h1>Persistent Data</h1>
        <a href="index.html">Home Page</a>

        <h2>Cookie Information</h2>
        <span id="cspanfn"></span><br>
        <span id="cspanln"></span><br>
        <span id="cspancity"></span><br><br>

        <h2>Local Storage Information</h2>
        <span id="lspanfn"></span><br>
        <span id="lspanln"></span><br>
        <span id="lspancity"></span><br><br>

        <h2>Session Storage Information</h2>
        <span id="sspanfn"></span><br>
        <span id="sspanln"></span><br>
        <span id="sspancity"></span><br><br>
    </div>
    <script>
        document.getElementById("cspanfn").innerHTML = getCookie("firstName");
        document.getElementById("cspanln").innerHTML = getCookie("lastName");
        document.getElementById("cspancity").innerHTML = getCookie("city");

        document.getElementById("lspanfn").innerHTML =
            localStorage.getItem("firstName");
        document.getElementById("lspanln").innerHTML =
            localStorage.getItem("lastName");
        document.getElementById("lspancity").innerHTML =
            localStorage.getItem("city");

        document.getElementById("sspanfn").innerHTML =
            sessionStorage.getItem("firstName");
        document.getElementById("sspanln").innerHTML =
            sessionStorage.getItem("lastName");
        document.getElementById("sspancity").innerHTML =
            sessionStorage.getItem("city");
    </script>
</body>

</html>
```

