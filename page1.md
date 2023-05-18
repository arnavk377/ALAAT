<html>
  <head>
    <link rel="stylesheet" href="page1.css">
    <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
  </head>
  <body>
    <button id="dark" onclick="darkMode()">Dark Mode</button>
    <h3><img id= "EC2" src ="images/fav.png"></h3>
    <h4><i class="material-icons">favorite</i>click on each topic to learn more!<i class="material-icons">favorite</i></h4>
        <div class="row">
        <button onclick="visibility()">Basic User Interface (UI) Properties</button>
        </div>
        <div class="column" id="column1">
        <h2>Properties:</h2>
    <p>
        <ul>
          <li>Color: This refers to the hue, saturation, and brightness of the UI elements such as background, text, buttons, etc.</li>
            <a href="https://htmlcolorcodes.com/">HTML Color Codes</a><br>
            <img src ="images/css4.jpg">
            <br><br>
          <li>Font: This refers to the typeface, size, weight, and style of the text displayed on the UI.</li>
            <a href="https://www.w3schools.com/css/css_font.asp">HTML Fonts</a><br>
            <img src ="images/css3.jpg">
            <br><br>
          <li>Layout: This refers to the arrangement and positioning of UI elements such as buttons, text boxes, images, etc</li>
            <p>Make wireframes to plan Layout!</p>
            <p>Resources: canva</p>
            <br><br>
          <li>Icons: These are small graphical symbols used to represent actions or ideas in the UI.</li>
            <br><br>
          <li>Interactivity: This refers to how the UI responds to user actions, such as clicking, tapping, dragging, and scrolling.</li>
            <br><br>
          <li>Accessibility: This refers to the ability of the UI to be used by people with disabilities, such as support for screen readers, keyboard navigation, and color contrast.</li>
        </ul>
      <br>
      <p>Identify all these properties on this page</p>
    </p>
        </div>
        <div class="row">
        <button onclick="visibility2()">Adding/Changing Colors</button>
        </div>
    <div class="column" id="column2">
        <h2>Changing Text and Background Color:</h2>
        <p>
    - The color property defines the foreground color of an HTML element's content and the background-color property defines the element's background color. 
    <br><br>
    - Text: color property is used when drawing the text and any text decorations. 
    <br><br>
    - backround-color is the text's backround color.
    <br><br>
    - text-shadow: configues a shadow effect to apply to text
    <br><br>
    - text-decoration-color: By default, text decorations use the color property as their colors. You can override that behavior and use a different color for them with the text-decoration-color property.
    <br><br>
    Hex Color Codes: composed of a hashtag and three pairs of characters hat represent the intensity of the three primary colors. 
    <br><br>
    - Value Range: 00 (the lowest intensity of a primary color) to FF (the highest intensity of a primary color)
    <br><br>
    - Every hex code consists of six characters in total. These six characters can be any combination of ten numerals (0-9) and six letters (a-f) <a href="https://github.com/1908901/elliepang/issues/30">(more combinations)</a><br>
    <br>
    </p>
    <img src ="images/css1.jpg">
    <img src ="images/css2.jpg">
    <h2>Themes</h2>
    <p>
    Theming: gives the users the ability to make customizations to websites and applications.
    <br><br>
     - Clicking a button to change the background of a website to red or black
    <br><br>
     - Increasing or decreasing the font size of a site website/application
    <br><br>
    - Clicking a button to remove content not relevant to the user.
    <br><br>
    - fonts, font size, color schemes, layouts, asthetics, ect.
    <br><br>
    Theme Properties: a set of CSS custom properties that make up a theme. <a href="https://github.com/1908901/elliepang/issues/30">example</a><br>
    <br>
    </p>
    </div>
      <div class="row">
    <button onclick="visibility3()">Images</button>
    </div>
    <div class="column" id="column3">
    <p>
      <h2>Styling Images (No Animation)</h2>
      <ul>
        <li>rounded corners on images and buttons</li>
        <li>center</li>
        <li>opacity</li>
        <li>grayscale</li>
      </ul>
      <img src ="images/bordrad.jpg">
      <img src ="images/EC2.png" id="EC2">
      <h2>Other Things You Need to Know for the AP Exam</h2>
      <h5>Data Compression</h5>
      <a href="https://www.canva.com/design/DAFgrBRoIy8/0N3nUSNywRLzRR53Vl5moQ/view?utm_content=DAFgrBRoIy8&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink">
  <img src="images/loss.jpg" id="loss">
</a>
<br>click on image to see full screen
        <br><br>
      <h5>base 64</h5>
        Binary data: Base64 is used to encode binary data, such as images, audio, and video files. You will need to understand how binary data is represented and stored in computing systems.
        <br><br>
        ASCII encoding: Base64 converts binary data into ASCII text format, which can be transmitted and stored more easily than binary data. You will need to understand ASCII encoding and how it works.
        <br><br>
        Encoding process: Base64 encodes binary data by splitting it into 6-bit chunks and encoding each chunk as a single character in the Base64 character set. You will need to understand how this encoding process works.
        <br><br>
        Decoding process: Base64 also includes a decoding process that converts Base64-encoded text back into binary data. You will need to understand how this decoding process works.
    </p>
    </div>
        <div class="row">
        <button onclick="visibility4()">Importance of Wireframes</button>
        </div>

  <div class="column" id="column4">
        <h2>Properties:</h2>
    <img src ="images/Page1WF.jpg">
    <p>
    - allows designers to plan the layout and interaction of an interface without being distracted by colors or other factors of their website. 
    <br><br>
    - Wireframes are also useful in determining how the user interacts with the interface (ex: buttons or menu behaviors)
    <br><br>
    - keep the concept user-focused, they clarify and define website features, and they are quick to create
    </p>
    </div>
    <script>
    var visibility = (function() {
      var first = true;
      return function() {
        first ? showColumn() : hideColumn();
        first = !first;
      }
    })();
    hideColumn();
      function hideColumn(){
    document.getElementById("column1").style.visibility = "hidden";
    }
        function showColumn() {
      document.getElementById("column1").style.visibility = "";
    }
    var visibility2 = (function() {
      var first = true;
      return function() {
        first ? showColumn2() : hideColumn2();
        first = !first;
      }
    })();
    hideColumn2();
      function hideColumn2(){
    document.getElementById("column2").style.visibility = "hidden";
    }
        function showColumn2() {
      document.getElementById("column2").style.visibility = "";
    }
    var visibility3 = (function() {
      var first = true;
      return function() {
        first ? showColumn3() : hideColumn3();
        first = !first;
      }
    })();
    hideColumn3();
      function hideColumn3(){
    document.getElementById("column3").style.visibility = "hidden";
    }
        function showColumn3() {
      document.getElementById("column3").style.visibility = "";
    }
    var visibility4 = (function() {
      var first = true;
      return function() {
        first ? showColumn4() : hideColumn4();
        first = !first;
      }
    })();
    hideColumn4();
      function hideColumn4(){
    document.getElementById("column4").style.visibility = "hidden";
    }
        function showColumn4() {
      document.getElementById("column4").style.visibility = "";
    }
    function darkMode() {
      var element = document.body;
      element.classList.toggle("dark-mode");
    }
    </script>