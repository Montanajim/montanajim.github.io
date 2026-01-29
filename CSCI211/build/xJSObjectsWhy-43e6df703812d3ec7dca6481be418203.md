# JavaScript Placement



You can include JavaScript code in an HTML document using the dedicated `<script>` tag. The placement of this tag depends on when you want the JavaScript to load:

1. **Inside the `<head>` section**:
   - Insert the `<script>` tag between the opening `<head>` and closing `</head>` tags. Place your JavaScript code inside it.
   - This ensures that the script is loaded and executed when the page loads. However, it can cause a delay in rendering the page because the browser waits for the script to download and execute before continuing with other HTML parsing.
1. **Inside the `<body>` section**:
   - You can place the `<script>` tags containing your JavaScript anywhere within the `<body>` tags.
   - While this approach allows the page to render faster, it may still cause a slight delay if the script is large or resource-intensive.
1. **Just before the `</body>` close tag**:
   - Some developers prefer placing the `<script>` tags just before the closing `</body>` tag.
   - This ensures that the entire HTML content is parsed and displayed before the JavaScript is loaded.
   - However, be cautious: if the script modifies the page content (e.g., via `document.write()`), it can disrupt the rendering process.

Choose the placement based on your specific requirements and performance considerations.



------







