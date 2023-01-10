# Modular Exponentiation

Many of our most important cryptographic algorithm, such as RSA public key encryption and the Diffie-Hellman Key Exchange Protocol, require that we compute the following:

ab mod n

The naive solution to compute this value is to compute ab, take that value mod n, and you’re done. However, in practice, a and b can be on the order of 100 decimal digits, so to compute ab will not only require a very long time to compute (due to the massive number of multiplications needed), but the final answer will be so large that it will overflow on most machines. 

To come up with a more reasonable solution, we make a couple of observations.

- The final value will always be less than n, due to the property of the modulus.
- A property of modulus is that the following identity is true:

ab mod n = (a mod n)(b mod n) mod n


Using observation #2, we can rewrite ab mod n as (a1 mod n)(a(b-1) mod n) mod n.

We can further reduce the problem by successively factoring out a:

	(a1 mod n)(a1 mod n)(a(b-2) mod n) mod n

These observations suggest the following algorithm and example (both taken from Wikipedia)

1. Set c = 1, b′ = 0.
2. Increase e′ by 1.
3. Set c = (a ⋅ c) mod n.
4. If b′ < b, go to step 2. Else, c contains the correct solution to c ≡ ab (mod n).

The example a = 4, b = 13, and n = 497 is presented again. The algorithm passes through step 3 thirteen times:

b' = 1. c = (1 ⋅ 4) mod 497 = 4 mod 497 = 4.

b' = 2. c = (4 ⋅ 4) mod 497 = 16 mod 497 = 16.

b' = 3. c = (16 ⋅ 4) mod 497 = 64 mod 497 = 64.

b' = 4. c = (64 ⋅ 4) mod 497 = 256 mod 497 = 256.

b' = 5. c = (256 ⋅ 4) mod 497 = 1024 mod 497 = 30.

b' = 6. c = (30 ⋅ 4) mod 497 = 120 mod 497 = 120.

b' = 7. c = (120 ⋅ 4) mod 497 = 480 mod 497 = 480.

b' = 8. c = (480 ⋅ 4) mod 497 = 1920 mod 497 = 429.

b' = 9. c = (429 ⋅ 4) mod 497 = 1716 mod 497 = 225.

b' = 10. c = (225 ⋅ 4) mod 497 = 900 mod 497 = 403.

b' = 11. c = (403 ⋅ 4) mod 497 = 1612 mod 497 = 121.

b' = 12. c = (121 ⋅ 4) mod 497 = 484 mod 497 = 484.

b' = 13. c = (484 ⋅ 4) mod 497 = 1936 mod 497 = 445.

The final answer for c is therefore 445.

# Assignment

Your assignment is to implement the modular exponentiation algorithm given above. Use the following test data.

a = 4, b = 13, and n = 497 (c = 445)


a = 67930, b = 32319, and n = 103969 (c = 6582)


a = 321, b = 12345, and n = 54321 (c = 45816 )


This one may not work: 
a = 3078999820144686550157991580392348514515710527551709057687658721854897950097326764688963387710535342
b = 5036061977613730517605247093371621941380257674856308609687266655721910711148679418191449796340381987
n = 1095739848401223530161382030331916535350776424648212970492881299350789366547535284278321916397670092
c = 283237912501648954965202330011994399969716991786816781338682574487609724556521531521606983588567976


 
Instrument your code so that you can answer the following questions for each test input.

How many multiplications does the algorithm perform?


How much space does the algorithm use?

If you have time, implement the naive algorithm (compute ab mod n directly and answer the same questions.

















# C3ProjectTemplate

See solutions in different languages in the "Templates" directory. Once you decide which language you'd like to use,
simply open that directory in your favorite IDE, and you should be able to run the included unit tests "out of the box".

The recommended IDEs are as follows, but feel free to use whatever IDE you are comfortable with.

-   [C#](Templates/C#) - [Microsoft Visual Studio](https://visualstudio.microsoft.com/vs/community/)
-   [Java](Templates/Java) - [IntelliJ Idea](https://www.jetbrains.com/idea/download) (Community Edition is fine)
-   [JavaScript](Templates/JavaScript) - [Microsoft Visual Studio Code](https://code.visualstudio.com/)
-   [Kotlin](Templates/Kotlin) - [IntelliJ Idea](https://www.jetbrains.com/idea/download) (Community Edition is fine)
-   [TypeScript](Templates/TypeScript) - [Microsoft Visual Studio Code](https://code.visualstudio.com/)
