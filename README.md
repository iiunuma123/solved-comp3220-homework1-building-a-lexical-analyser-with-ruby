Download Link: https://assignmentchef.com/product/solved-comp3220-homework1-building-a-lexical-analyser-with-ruby
<br>
The grammar rules for the language “TINY” are listed below. In this assignment we will identify the tokens in this language and build a lexical analyser (lexer) for recognizing and outputting TINY tokens.

# <a href="http://www.cs.rochester.edu/~brown/173/readings/05_grammars.txt">https://www.cs.rochester.edu/~brown/173/readings/05_grammars.txt</a> #

# “TINY” Grammar #

<table width="528">

 <tbody>

  <tr>

   <td width="104"># PGM</td>

   <td width="48">–&gt;</td>

   <td width="376">STMT+</td>

  </tr>

  <tr>

   <td width="104"># STMT</td>

   <td width="48">–&gt;</td>

   <td width="376">ASSIGN | “print” EXP</td>

  </tr>

  <tr>

   <td width="104"># ASSIGN</td>

   <td width="48">–&gt;</td>

   <td width="376">ID “=” EXP</td>

  </tr>

  <tr>

   <td width="104"># EXP</td>

   <td width="48">–&gt;</td>

   <td width="376">TERM ETAIL</td>

  </tr>

  <tr>

   <td width="104"># ETAIL</td>

   <td width="48">–&gt;</td>

   <td width="376">“+” TERM ETAIL | “-” TERM ETAIL | EPSILON</td>

  </tr>

  <tr>

   <td width="104"># TERM</td>

   <td width="48">–&gt;</td>

   <td width="376">FACTOR TTAIL</td>

  </tr>

  <tr>

   <td width="104"># TTAIL</td>

   <td width="48">–&gt;</td>

   <td width="376">“*” FACTOR TTAIL | “/” FACTOR TTAIL | EPSILON</td>

  </tr>

  <tr>

   <td width="104"># FACTOR#</td>

   <td width="48">–&gt;</td>

   <td width="376">“(” EXP “)” | INT | ID</td>

  </tr>

  <tr>

   <td width="104"># ID</td>

   <td width="48">–&gt;</td>

   <td width="376">ALPHA+</td>

  </tr>

  <tr>

   <td width="104"># ALPHA</td>

   <td width="48">–&gt;</td>

   <td width="376">a | b | … | z or</td>

  </tr>

  <tr>

   <td width="104">#</td>

   <td width="48"> </td>

   <td width="376">A | B | … | Z</td>

  </tr>

  <tr>

   <td width="104"># INT</td>

   <td width="48">–&gt;</td>

   <td width="376">DIGIT+</td>

  </tr>

  <tr>

   <td width="104"># DIGIT</td>

   <td width="48">–&gt;</td>

   <td width="376">0 | 1 | … | 9</td>

  </tr>

  <tr>

   <td colspan="2" width="152"># WHITESPACE –&gt;</td>

   <td width="376">Ruby Whitespace</td>

  </tr>

 </tbody>

</table>




Whenever a token is identified, we encapsulate it using the Token class below. Each token has a type and text. For example, if DOG was identified as a variable in this language, it could have type “id” and

text “DOG”. The add operator might have type “addOp” and text “+” or type “+” and text “+”.  These values are somewhat arbitrary – choose values that make sense to you.

<h1>Token Class</h1>

I have given you a partially complete Token class that you should modify for this assignment called “<strong>TinyToken.rb</strong>”. It has a few constants already defined. The VALUES of these variables represent the name of the token. You will need to build more constants to store all of the tokens that exist in this language. For this assignment, you get to decide what categories of lexemes there are and what you want to name those categories.

It is important to test all the code you write. At the very least, use “puts” to test the class methods. You can build the tests in separate files and load them as needed: load “mytest.rb”.  The code below tests the Token class methods.

# Test the Token class

tok = Token.new(“atype”,”atext”) puts “Token type: #{tok.type}” puts “Token text: #{tok.text}” tok.type = “btype” tok.text = “btext” puts “Token type: #{tok.type}” puts “Token text: #{tok.text}” puts “Token: #{tok}”

<h1>The “Lexer”</h1>

The first goal is to build a Scanner (or Lexer) for TINY. I have sketched the basic structure in file named “<strong>TinyScanner.rb</strong>”. Here are a few points to consider:

<ul>

 <li>The constructor is passed a file name which contains the source code for a TINY program. The constructor opens the file and reads the first character, storing it in class variable @c (which acts as a one-character look ahead). <strong>I already did this.</strong></li>

 <li>Currently, the Scanner abends if it is passed a file that doesn’t exist. <strong>Modify</strong> the code so that it fails gracefully in this circumstance.</li>

 <li>Method nextCh() updates @c with the next character and returns it, unless it has reached the end of the file, in which case it will return “<strong>eof</strong>”. <strong>I already did this.</strong></li>

 <li>Method nextToken() returns the next token identified by the scanner. It is not complete, as it does not identify all Tokens in your grammar yet. In addition to identifying and returning a token, this method should print what it finds, each time it identifies a token (just like the example of the lexer in the PowerPoint for chapter 4). <strong>You must complete this method.</strong></li>

 <li>Contiguous whitespace should be combined and emitted as a single token. <strong>I already did this for you</strong>.</li>

 <li>An end of file (EOF) token should be emitted when the file has been completely processed. <strong>I already did this for you</strong>.</li>

 <li>There are several helper methods defined at the bottom of “TinyScanner.rb” that you can use to help you to identify different types of characters (like numbers, letters, and whitespace).</li>

</ul>

<h1>Display and Print Tokens</h1>

I’ve included a file called “<strong>TestTinyLexer.rb</strong>” that you can use to test your lexer (previous section). For the time being, it simply scans a file and stores all of the tokens in a text file called “tokens”. Feel free to modify this file to test different things about your lexer, or to open the tokens file to see what was actually saved.

I’ve also included a sample input file (input.txt) that adheres to our TINY programming language. You should experiment with different inputs that both adhere to and don’t adhere to the grammar to verify the correctness of your lexer.

<h1>Sample Program Output</h1>

Below is a screenshot of sample output that would result from using the included sample input file.

<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2021/11/687.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2021/11/687.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>