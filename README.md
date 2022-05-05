# Vigenère cipher
#### Video Demo:  <https://youtu.be/wqOQJsI3JkA>
#### Description: Web-app that teaches how to use the Vigenère Cipher

Reading **"Nathan Fox: Dangerous Time"**, a fascinating book about a secret agent and his aventures,
I was keeping interest in the encryptions they show and how to do it, so I decided to make a website to show how to do the encryption that I liked the most.

The **Vigenère Cipher** is a method of encrypting alphabetic text by using a series of interwoven Caesar ciphers, based on the letters of a keyword. It employs a form of polyalphabetic substitution.

For the implementation I used python, flask, ajax, html, css, and javascript.

I started doing a research about the **Vigenère Cipher**, then I was ready to do the implementation.
First I use a HTML template and personalize to do the website, including everything I would needed.
then I implement the python part, using flask to create to routes, one which point to `/` that just render a template call `layout.html`, and another which point to `/vige` which in it will be implemented the **Vigenère Cipher**.

In the **Vigenère Cipher** implentation we need two values, the plain-text(The text we want to encrypt) and a key(Which the cipher needs to employ the polyalphabetic substitution).
Also for my implementation we neeed a third value, that is the method(If the user wants to encrypt o decrypt the text).

So in the route `/vige` for the implementation, first we request the three values mentioned above, for sanity check we are going to check if the user's input is not blank and is only alphabetic characters. If it is not, then we notify the user.
Then we need to implement three function:
-`generate_key(message, key)`: which compare is the length of the key is the same that the plain-text, if they are same then return the key, if is not then the function will repeat key until it is the same length as the plain-text.
-`encrypt(message, key)`: for the encryption using the **Vigenère Cipher** we are going to use this function, giving it the message and the key previously checked by `generate_key`. For the algorithm we use a loop to check every letter with their respective key, to the use and alphabetic substitution. 
Every letter has a ASCII value, to that value we sum the ASCII value for the key, then we get the residue of the sum divided by 26 to the the ASCII character that going to the representation in the cipher-text, to that character we sum 65(A value in ASCII), to keep it in the correct ASCII representation.
Then we return a new string with the cipher-text.
-`decrypt(message, key)`: we are going to do the same we did in the implementation of 'encrypt' but instead of sum the key ASCII value to letter ASCII value, we are going to sustract it.

Next in the implementation for `/vige` we are going to use three functions above, first we call `generate_key` to check the key length, then we are going to check which method the user request(encryption or decryption),
based on that we are going to execute `encrypt` or `decrypt` which are going to return the cipher-text.

I was debating something about the design, whether to render other templates or if there was another way to make the website dynamic. So I did a research and I find AJAX.
AJAX is a technique that consists of making a request to the web server in parallel using JavaScript code. It is used to update certain content on a web page without having to reload it completely, which provides greater transfer speed by requesting only the necessary data, better appearance and more comfort for the user.

Now with AJAX in `layout.html` we do an implementation, every time the user press on one bottom "**Try it**" with Javascript we are going to call a function call `pass_data()`, this function will use AJAX and JQuery(a library of AJAX), who is going to request the user's input and pass it to the server route `/vige`.
Then in this route the user's input will be processes and return the cipher-text or an error message, If it's necessary. The return is going to be through a library of python called `flask.json` using the function `jsonify` that creates a Response with the JSON representation of the given arguments with an application/json mimetype. The arguments to this function are the same as to the dict constructor.
Next `pass_data()` is going to check the return a print the error(In case there is one) or the cipher-text to the user and with that finish the implementation of the **Vigenère Cipher**.