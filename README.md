Download Link: https://assignmentchef.com/product/solved-cs305-hw2-parser
<br>
In this homework you will write a context free grammar and implement a simple parser for BMO language for which you designed a scanner in the previous homework. Note that, there might be differences between the syntax of BMO language given in the previous homework and this one. Therefore, take the explanations on the syntax of BMO language given in this homework.

The language that will be generated by your grammar and other requirements of the homework are explained below.

<h1>1             Subset of the Language</h1>

The grammar you will write will generate the BMO language as described below. Here is an example program in this language to give you an idea how a BMO program looks like.

int vector digits, digits2 = [1,2,3,4,5,6,7,8,9,0]; int matrixM = 3; int a = 5;

real realNum = 4.0E-12; int resultV = a + matrixM; int finalResult = a + resultV * 5; int matrix result = [1,2;3,4;5,6;7,8;9,0]; int matrix matrix_1 = [1.2,2.2;3.2,4.1]; int matrix resultT = transpose(result); digits = digits * matrixM; int dotProduct = digits .* digits; if(dotProduct &lt;= matrixM || dotProduct &gt;= result) resultT = resultT * dotProduct;

endif resultT = b; Note that the set of statements given above does not have to make sense. It may even have errors as a BMO program (e.g. an undeclared variable being used, multiplying vector with a matrix, or assigning a non-vector variable to a vector value). We are only using it for explanation purposes. Just focus on the syntactic features used in this example. Below is the detailed syntactic features of the BMO language.

<ol>

 <li>A BMO program consists of a non-empty sequence of statements.</li>

 <li>Each statement in our BMO can be a declaration, or an assignment statement or an if</li>

 <li>A declaration is given by the type, followed by a comma separated list of variable names, followed by an equality sign (i.e. the character =), followed by an expression, and followed by a semicolon.</li>

 <li>The type can be one of the following: int, int vector, int matrix, real, real vector, real matrix.</li>

 <li>An assignment statement given by a variable name, and an equality sign (i.e. the character =), and then an expression, finally followed by a semicolon. E.g.</li>

</ol>

a = b+c;

<ol start="6">

 <li>An if statement starts with keyword if. After the keyword if, a boolean expression resides betweeen ( and ). This is followed by the body of the if statement, which is a non–empty sequence of statements. Finally, the keyword endif is given.</li>

 <li>An expression can be a variable, or a number (integer or real), or a vector literal, or a matrix literal, or two expressions being applied to one of the operators ∗,+,−,<em>/</em>,<em>.</em>∗ or a transpose expression.</li>

 <li>A vector literal is given by a [, followed by a value row, followed by a ].</li>

 <li>A value row is a comma separated list of values, where a value is either a number (integer or real), or a variable name.</li>

 <li>A matrix literal is given by a [, followed by a semicolon separated list of value rows, followed by a ]. There has to be at least two rows in a matrix literal.</li>

 <li>A transpose expression is given by the keyword transpose, followed by a (, followed by an expression, followed by a ).</li>

 <li>A boolean expression is either a simple comparison or two boolean expressions connected with a boolean operator, where we only have &amp;&amp; and || as the boolean operators.</li>

 <li>A simple comparison must have exactly two variables separated with one of the comparison operators &gt;,&lt;,&gt;=,&gt;=,!=,==.</li>

</ol>

<h1>2             Terminal Symbols</h1>

Use the following terminal symbols in your grammar. You can assume that the scanner will return the corresponding token. Do not add any new tokens and do not change the name of the tokens.

tINTTYPE: The scanner returns this token when it sees “int” in the input.

tINTVECTORTYPE: The scanner returns this token when it sees “int vector” in the input.

tINTMATRIXTYPE: The scanner returns this token when it sees “int matrix” in the input. tREALTYPE: The scanner returns this token when it sees “real” in the input.

tREALVECTORTYPE: The scanner returns this token when it sees “real vector” in the input. tREALMATRIXTYPE: The scanner returns this token when it sees “real matrix” in the input. tTRANSPOSE: The scanner returns this token when it sees “transpose” in the input. tIDENT: The scanner returns this token when it sees an identifier in the input. tDOTPROD: The scanner returns this token when it sees “.*” in the input.

tIF: The scanner returns this token when it sees “if” in the input. tENDIF:The scanner returns this token when it sees “endif” in the input. tREALNUM: The scanner returns this token when it sees a real number in the input. tINTNUM: The scanner returns this token when it sees an integer number in the input. tAND: The scanner returns this token when it sees “&amp;&amp;” in the input. tOR: The scanner returns this token when it sees “||” in the input. tGT: The scanner returns this token when it sees “&gt;” in the input. tLT: The scanner returns this token when it sees “&lt;” in the input. tGTE: The scanner returns this token when it sees “&gt;=” in the input. tLTE: The scanner returns this token when it sees “&lt;=” in the input. tNE: The scanner returns this token when it sees “!=” in the input. tEQ: The scanner returns this token when it sees “==” in the input.

Besides these tokens, you if you need any more tokens in your grammar (e.g. [, ;, etc.), directly use the lexeme of such tokens in your grammar.

<h1>3             Non-Terminal Symbols</h1>

Use the following non-terminal symbols in your grammar. This is the entire set of non-terminals that you will use in your grammar. Do not add a new non-terminal symbol, or do not change the name of a non-terminal symbol given here.

&lt;prog&gt;: This is the start symbol of the grammar.

&lt;stmtlst&gt;: Denotes a non–empty list of statements.

&lt;stmt&gt;: Denotes a single statement. &lt;decl&gt;: Denotes a declaration. &lt;type&gt;: Denotes the type in a declaration.

&lt;vars&gt;: Denotes the non–empty variable list in a declaration.

&lt;asgn&gt;: Denotes an assignment statement.

&lt;if&gt;: Denotes an if statement.

&lt;expr&gt;: Denotes an expression.

&lt;transpose&gt;: Denotes a transpose expression.

&lt;vectorLit&gt;: Denotes a vector literal.

&lt;matrixLit&gt;: Denotes a matrix literal.

&lt;row&gt;: Denotes a non–empty list of comma separated values.

&lt;rows&gt;: Denotes a non–empty list of semicolon separated rows. Note that only 1 row is possible, where a matrix literal requires at least 2 rows.

&lt;value&gt;: Denotes a value that can be either an integer number, or a real number, or a variable reference.

&lt;bool&gt;: Denotes a boolean expression.

&lt;comp&gt;: Denotes a simple comprasion.

&lt;relation&gt;: Denotes a binary relational operators (such as ==, etc.) that can be used in a simple comparison.

<h1>4             Output</h1>

Your parser must print out OK and produce a new line, if the input is grammatically correct. Otherwise, your parser must print out ERROR and produce a new line