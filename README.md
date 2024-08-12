# Cybersecurity_XSS_Demo
Cross-Site Scripting (XSS) Demo

### Step-by-Step Guide for XSS Demonstration

1. **Ensure PHP is Running:**
   - Make sure the local server environment is running and capable of processing PHP files.

2. **Vulnerable PHP Code for Demonstration:**

```php
<!DOCTYPE html>
<html>
<body>
  <form action="xss_demo.php" method="GET">
    <input type="text" name="query">
    <input type="submit" value="Search">
  </form>
  <?php
    if (isset($_GET['query'])) {
        echo "Search results for: " . $_GET['query'];
    }
  ?>
</body>
</html>
```

3. **Place the File in the Correct Directory:**
   - Save the above code as `xss_demo.php`.

4. **Access the File in the Browser:**
   - Open your web browser and navigate to `http://localhost/xss_demo.php`.

### Testing the Vulnerable Page

1. **Enter the XSS Payload:**
   - In the text input field, enter the following script:

```html
<script>alert('XSS Vulnerability!');</script>
```

2. **Click "Search":**
   - The page should display an alert box with the message "XSS Vulnerability!" indicating the vulnerability.

### Fixing the XSS Vulnerability

1. **Fixed PHP Code:**

```php
<!DOCTYPE html>
<html>
<body>
  <form action="xss_demo_fixed.php" method="GET">
    <input type="text" name="query">
    <input type="submit" value="Search">
  </form>
  <?php
    if (isset($_GET['query'])) {
        echo "Search results for: " . htmlspecialchars($_GET['query']);
    }
  ?>
</body>
</html>
```

2. **Sve the Fixed File:**
   - Save the file as `xss_demo_fixed.php` with the fixed code above.

3. **Load the fixed page:**
   - Load the fixed page `http://localhost/xss_demo_fixed.php`.

### Testing the Mitigated Page

1. **Enter the Same XSS Payload:**
   - In the text input field, enter the same script:

```html
<script>alert('XSS Vulnerability!');</script>
```

2. **Click "Search":**
   - This time, the script should be displayed as plain text, and the alert box should not appear.

### Troubleshooting

1. **Ensure PHP is Executing:**
   - Make sure your local server is configured correctly to execute PHP files. You can verify by creating a simple `phpinfo.php` file:

```php
<?php phpinfo(); ?>
```

   - Place this file in the webserver folder. It should display the PHP configuration information.

2. **Check for Errors:**
   - Check your server logs for any errors that might indicate issues with PHP execution.

3. **Browser Cache:**
   - Clear your browser cache or use an incognito window to ensure you're seeing the latest version of the page.

Following these steps should help you successfully demonstrate the XSS vulnerability and its mitigation. If you still encounter issues, please provide Fred the details about the server environment and any error messages you might be seeing.
