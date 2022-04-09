# Lab 11: Tensorflow

### Part 1
![image](https://user-images.githubusercontent.com/86938356/162546836-577d4c26-d905-4698-aa87-3c3c2b48d6f0.png)

### Part 2
![2022-04-09](https://user-images.githubusercontent.com/86938356/162585329-4423ff63-ba5e-45a6-b94d-743811baa1ae.png)

### Part 3
#### ATTEMPT 1
Original Image:
![image](https://user-images.githubusercontent.com/86938356/162587654-eb6fc98b-2e6e-4f2e-a7dd-cb9ec0adf429.png)

Rescaled image:
![shirt](https://user-images.githubusercontent.com/86938356/162587662-913dd917-8e00-40bc-9908-9089fa1072bc.png)

Results:
```[5.9208719e-07 1.1671295e-14 2.8638050e-07 7.9413995e-09 3.1132300e-14
 3.5870511e-15 8.9058369e-07 2.8359772e-16 9.9999821e-01 1.4945692e-12] 8 Bag
```

#### ATTEMPT 2
Original Image:
![sandal](https://user-images.githubusercontent.com/86938356/162588628-e5faab37-e7ad-445a-b27a-bbd8c516c67c.png)

Rescaled Image:
![sandal](https://user-images.githubusercontent.com/86938356/162588631-62946618-af79-4214-8f1e-2bfc4f1b9672.png)

Results:
```[7.94781907e-10 1.32748715e-21 1.04075737e-09 1.94389725e-13
 1.01628978e-16 1.05645013e-19 6.48150311e-10 9.61214568e-22
 1.00000000e+00 1.34754249e-15] 8 Bag
 ```
 
#### ATTEMPT 3
Original Image:
![image](https://user-images.githubusercontent.com/86938356/162588910-61ee7600-ee78-4089-9168-5c9b44aca7e5.png)

Rescaled Image:
![boots](https://user-images.githubusercontent.com/86938356/162588919-4becf500-6d4c-4af5-b4d5-c0a35d8f128b.png)

Results:
```[5.79112935e-09 7.57239549e-10 3.37277567e-11 2.41184672e-09
 1.02745630e-14 3.72478244e-04 1.02939456e-10 2.26457417e-02
 9.53287724e-08 9.76981699e-01] 9 Ankle boot
 ```
 
 The model seems to think everything is a bag, but it correctly guessed the boots image. Only 1/3
