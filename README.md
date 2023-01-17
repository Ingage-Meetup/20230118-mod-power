# Modular Exponentiation

Many of our most important cryptographic algorithms, such as RSA public key encryption and the Diffie-Hellman Key Exchange Protocol, require that we compute the following:

a<sup>b</sup> mod n

The naive solution to compute this value is to compute a<sup>b</sup>, take that value mod n, and you’re done. However, in practice, a and b can be on the order of 100 decimal digits, so to compute a<sup>b</sup> will not only require a very long time to compute (due to the massive number of multiplications needed), but the final answer will be so large that it will overflow on most machines. 

To come up with a more reasonable solution, we make a couple of observations.

- The final value will always be less than n, due to the property of the modulus.
- A property of modulus is that the following identity is true:

    xy mod n = (x mod n)(y mod n) mod n


Using observation #2, we can rewrite a<sup>b</sup> mod n as (a mod n)(a<sup>(b-1)</sup> mod n) mod n.

We can further reduce the problem by successively factoring out a:

    (a mod n)(a mod n)(a^(b-2) mod n) mod n

We can further decompose the expression so that it is a succession of (a mod n) (a mod n) ... (a mod n) with b factors.

These observations suggest the following algorithm and example (both taken from Wikipedia)

1. Set c = 1, d = 0. (d is just a counter)
2. Increase d by 1.
3. Set c = (a ⋅ c) mod n.
4. If d < b, go to step 2. Else, c contains the correct solution to c ≡ a<sup>b</sup> (mod n).

The example a = 4, b = 13, and n = 497 is presented again. The algorithm passes through step 3 thirteen times:

d = 1. c = (1 ⋅ 4) mod 497 = 4 mod 497 = 4.

d = 2. c = (4 ⋅ 4) mod 497 = 16 mod 497 = 16.

d = 3. c = (16 ⋅ 4) mod 497 = 64 mod 497 = 64.

d = 4. c = (64 ⋅ 4) mod 497 = 256 mod 497 = 256.

d = 5. c = (256 ⋅ 4) mod 497 = 1024 mod 497 = 30.

d = 6. c = (30 ⋅ 4) mod 497 = 120 mod 497 = 120.

d = 7. c = (120 ⋅ 4) mod 497 = 480 mod 497 = 480.

d = 8. c = (480 ⋅ 4) mod 497 = 1920 mod 497 = 429.

d = 9. c = (429 ⋅ 4) mod 497 = 1716 mod 497 = 225.

d = 10. c = (225 ⋅ 4) mod 497 = 900 mod 497 = 403.

d = 11. c = (403 ⋅ 4) mod 497 = 1612 mod 497 = 121.

d = 12. c = (121 ⋅ 4) mod 497 = 484 mod 497 = 484.

d = 13. c = (484 ⋅ 4) mod 497 = 1936 mod 497 = 445.

The final answer for c is therefore 445.

# Assignment

1. Implement the modular exponentiation algorithm given above. Use the following test data.

    a = 4, b = 13, and n = 497 (c = 445)


    a = 67930, b = 32319, and n = 103969 (c = 6582)


    a = 321, b = 12345, and n = 54321 (c = 45816 )


    This one may not work: 

    a = 3078999820144686550157991580392348514515710527551709057687658721854897950097326764688963387710535342
    
    b = 5036061977613730517605247093371621941380257674856308609687266655721910711148679418191449796340381987

    n = 1095739848401223530161382030331916535350776424648212970492881299350789366547535284278321916397670092

    c = 283237912501648954965202330011994399969716991786816781338682574487609724556521531521606983588567976

 
2. Implement the naive algorithm.

3. Instrument both implementations to measure the execution time of each.

4. Which algorithm is faster? 



# C3ProjectTemplate

See solutions in different languages in the "Templates" directory. Once you decide which language you'd like to use,
simply open that directory in your favorite IDE, and you should be able to run the included unit tests "out of the box".

The recommended IDEs are as follows, but feel free to use whatever IDE you are comfortable with.

-   [C#](Templates/C#) - [Microsoft Visual Studio](https://visualstudio.microsoft.com/vs/community/)
-   [Java](Templates/Java) - [IntelliJ Idea](https://www.jetbrains.com/idea/download) (Community Edition is fine)
-   [JavaScript](Templates/JavaScript) - [Microsoft Visual Studio Code](https://code.visualstudio.com/)
-   [Kotlin](Templates/Kotlin) - [IntelliJ Idea](https://www.jetbrains.com/idea/download) (Community Edition is fine)
-   [TypeScript](Templates/TypeScript) - [Microsoft Visual Studio Code](https://code.visualstudio.com/)
