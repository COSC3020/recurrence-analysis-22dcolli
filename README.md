[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

ANSWER:
First we start by analyzing the structure of the code to gain information. Starting with the first if else statement, the if portion checks for the base case whilst the else portion contains nested for loops. Looking at the number of times we have to loop, those being the $n* n$ , $n$ , and $n*n$ from the three for loops we can combine that into an easy $n^{5}$. We also see that the mystery function $mystery(\frac{n}{3})$ will result in 3 calls with $n / 3$. With this information the result is $3T(\frac{n}{3}) + n ^ {5}$ where we see the $3T(\frac{n}{3})$ portion come from $mystery(\frac{n}{3})$ and the $n^{5}$ from the for loops.

Working through the problem we assume:

$T(n) = 1$ for $n \le 1$ (the base case from the if statement)

and

$3T(\frac{n}{3}) + n ^ {5}$ (as stated before)

The goal now is to establish a pattern, here substitution will be used:

Starting with $T(n) = 3T(\frac{n}{3}) + n ^ {5}$


$=3(3T(\frac{n}{9})+(\frac{n}{3})^{5})+n^{5}$

combining

$=9T(\frac{n}{9}) + n^{5} + 3(\frac{n}{3})^{5}$

$=9(3T(\frac{n}{27}) + (\frac{n^{5}}{9})) + n^{5} + \frac{n^{5}}{3^{4}}$

combining

$=27T(\frac{n}{27}) + n^{5} + \frac{n^{5}}{3^{4}}+ \frac{n^{5}}{9^{4}}$

With this we have gathered enough information to know the occuring pattern:

$T(n) = 3^{i}(\frac{n}{3^{i}}) + \frac{n^{5}}{3^{4(i-1)}} + \frac{n^{5}}{3^{4(i-2)}} + ... + n^{5}$

$i$ needs to make it so the base case($T(1)$ is reached, meaning here, that we assume $i$ will be $log_{3}(n)$.

Using that knowledge we now have:

$T(n) = 3^{log_{3}(n)}T(\frac{n}{3^{log_{3}(n)}}) + \frac{n^{5}}{3^{4(log_{3}(n)-1)}} + \frac{n^{5}}{3^{4(log_{3}(n)-2)}} + ... + n^{5}$

Simplified further

$T(n) = 3^{log_{3}(n)}T(\frac{n}{3^{log_{3}(n)}}) + \frac{n^{5}}{3^{4log_{3}(n)-4}} + \frac{n^{5}}{3^{4log_{3}(n)-8}} + ... + n^{5}$

$=nT(1) + \frac{n^{5}{(n^{4}*3^{-4})} + $
