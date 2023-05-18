<html>
    <head>
    <link rel="stylesheet" href="snake.css">
    </head>
    <body>
    <div>
        <br>
        <h1>Constructing + Customizing a Javascript Snake Game!</h1>
        <br>
        <h2>Construction - HTML</h2>
        <p>The order that you write code from top to bottom in the HTML file is the same order that it will appear on the website, UNLESS you change its position in CSS:
        <br>
        <table>
            <tr>
                <td>
                    <h4>HTML:</h4>
                    <div style="margin: 0 auto; width: 500px">
                    <img src="images/snakelesson1.jpg" style=" width: 500px;" align="top|center">
                    </div>
                    <br>
                    <h4>CSS:</h4>
                    <div style="margin: 0px auto; width: 300px">
                    <img src="images/snakelesson3.jpg" style=" width: 300px; text-align: center;" align="center">
                    </div>
                    <div style="margin: 0px auto; width: 300px">
                    <img src="images/snakelesson7.jpg" style=" width: 300px; text-align: center;" align="center">
                    </div>
                </td>
                <td>
                    <p style="text-align: center; font-weight:bolder; font-size: 50px; padding: 10px;"> &#8680;</p>
                </td>
                <td>
                    <img src="images/snakelesson2.jpg" style=" width: 750px; padding-right: 75px; padding-top: 0px;" align="right">
                </td>
            </tr>
        </table>
        </p>
        <h2>Functions - JavaScript</h2>
        <p>
        <table>
            <tr>
                <td>
                    <div>
                    <img src="images/snakelesson5.jpg" style=" width: 600px; text-align: center;" align="center">
                    </div>
                </td>
                <td>
                    <ul>
                    <li><b>Selection</b>: use of "if statement" to determine if apple's xy position is the same as the xy position of a pixel of the snake</li>
                    <li>If statement is true, the following will be executed:
                        <ul>
                            <li>Add 1 to the length of the snake</li>
                            <li>Add 1 to the user's current score</li>
                            <li>Display score on interface</li> 
                            <li>Randomly generate apple's next x and y position</li> 
                        </ul> 
                    </li>
                    <li><b>Sequencing</b>: Code is executed in a specific order for function purpose</li>
                    </ul>
                </td>
            </tr>
            <tr>
                <td>
                <div>
                <img src="images/snakelesson6.jpg" style=" width: 600px; text-align: center;" align="center">
                </div>
                </td>
                <td>
                    <ul>
                        <li><b>Iteration:</b>Use of "for loop" to iterate through each of the snake's cells until it reaches the length of the entire snake</li>
                            <ul>
                                <li>Note: Purpose of "var i = index + 1" is to initialize i to start at 1, which represents the snake's number of cells. This way it's not confusing when the index is 0 but the snake appears to have a length of 1.</li>
                            </ul>
                        <li><b>Selection: If the head of the snake is in the same x and y position of any of the other cells of the snake</b></li>
                            <ul>
                                <li>Now that it is confirmed the user lost the game this round, check if current score is greater than max. If true, set that score to new max</li>
                                <li>Now set snake back to default conditions</li>
                                    <ul>
                                        <li>Snake starts at x y position 160px in respect to 400 px by 400 px grid</li>
                                        <li>Array keeps track of all the cells the snake occupies</li>
                                        <li>Snake generates as 4 cells long</li>
                                        <li>Intialize score to 0 & display score on interface</li>
                                        <li>Reset apple's position</li>
                                        <li>Display new high score</li>
                                    </ul>
                            </ul>
                    </ul>
                </td>
            </tr>
        </table>
        </p>
        <!-- Add Button -->
        <h2>Customization - CSS</h2>
        <p>
        <br>
        <table>
            <tr>
                <td>
                    <div>
                    <img src="images/snakelesson11.jpg" style=" width: 600px; text-align: center;" align="center">
                    </div>
                    <div>
                    <img src="images/snakelesson9.jpg" style=" width: 600px; text-align: center;" align="center">
                    </div>
                    <div>
                    <img src="images/snakelesson8.jpg" style=" width: 400px; text-align: center;" align="center">
                    </div>
                </td>
                <td>
                    <ul>
                        <li>First set the variables that you will later reference in your CSS code</li>
                            <ul>
                                <li><b>"canvas"</b> represents the screen of the game </li>
                                <li><b>"context"</b> uses the Canvas API. (You must have a canvas established in the HTML in order to use this.) The call, "getContext()" returns drawing context. The identifier "2d", provides 2d drawing functions. We set this to a variable in order to call it later.</li>
                                <li><b>"root"</b> calls the :root element from the CSS. This is a method of setting values, such as color, for Javascript elements.</li>
                            </ul>
                        <li><b>Drawing cells</b></li>
                            <ul>
                                <li>Set apple color to value set in root</li>
                                <li>Fill the "context" allows you to fill in single cell at a specified color and xy position in the canvas </li>
                                <li>After drawing the apple cell, you can reassign context to a new color. This way, the snake and apple can be different colors with no interference.</li>
                                <li>NOTE: The purpose of grid - 1 (grid = 16) is so that the cell does not fill up entire 16 x 16 pixels but 15 x 15 pixels. This is especially useful for the snake where there are multiple cells next to each other and  creates the visual effect of spaces in between each snake's block that allows you to count its length easily</li>
                            </ul>
                        <li><b>CSS</b>: assign the colors to the apple and snake through root
                            <ul>
                            <li>Declare global CSS variables with --x. You can assign colors, padding, position, size, etc. to variables, and call them throughout your code, including in Javascript.</li>
                            </ul>
                        </li>
                    </ul>
                </td>
            </tr>
        </table>
        </p>
    </div>
    </body>
</html>