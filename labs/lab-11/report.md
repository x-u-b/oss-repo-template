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
![sandals](https://user-images.githubusercontent.com/86938356/162589073-834396b7-0882-4b75-b123-fa82c741c7f6.png)

Rescaled Image:
![sandals](https://user-images.githubusercontent.com/86938356/162589093-9e889efb-3ff1-42d1-9690-77afad5501fe.png)

Results:
```[2.3181332e-13 1.2752669e-13 8.4671880e-14 4.4119206e-15 6.6137007e-18
 2.8205733e-14 2.7767025e-13 2.2690692e-31 1.0000000e+00 9.2222536e-21] 8 Bag
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
