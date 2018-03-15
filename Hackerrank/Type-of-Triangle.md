Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

* Equilateral: It's a triangle with  sides of equal length.
* Isosceles: It's a triangle with  sides of equal length.
* Scalene: It's a triangle with  sides of differing lengths.
* Not A Triangle: The given values of A, B, and C don't form a triangle.

#### Input Format
The TRIANGLES table is described as follows:

![Yes](https://i.imgur.com/P9DDuCd.png)

Each row in the table denotes the lengths of each of a triangle's three sides.

#### Sample Input

![Yes](https://i.imgur.com/ipU5YfH.png)

#### Sample Output

`Isosceles

Equilateral

Scalene

Not A Triangle`

#### Explanation

Values in the tuple (20,20,23) form an Isosceles triangle, because A☰B .

Values in the tuple (20,20,20) form an Equilateral triangle, because A☰B☰C .

Values in the tuple (20,21,22) form a Scalene triangle, because A!=B!=C.

Values in the tuple (13,14,30) cannot form a triangle because the combined value of sides A and B is not larger than that of side C.


#### Solution

`SELECT
  CASE
    WHEN A = B AND B = C then "Equilateral"
    
    WHEN A + B <= C then "Not A Triangle"
    
    WHEN A + C <= B then "Not A Triangle"
    
    WHEN B + C <= A then "Not A Triangle"
    
    WHEN A = B AND A <> C then "Isosceles"
    
    WHEN A = C AND A <> B then "Isosceles"
    
    WHEN B = C AND A <> B then "Isosceles"
    
    ELSE "Scalene"
  END
FROM triangles`
