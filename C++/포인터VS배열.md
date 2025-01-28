<h1>포인터VS배열</h1>

 ![header](https://capsule-render.vercel.app/api?color=gradient&type=waving)

###  포인터 VS 배열

결론부터 말하면, 포인터와 배열의 큰 차이점은 


* **포인터**: 가리키는 변수의 주소 값을 저장하는 별도의 메모리를 할당

* **배열**: 미리 할당되어 저장된 연속된 원소들을 모두 포함하여 배열이 구성됨, 단지 배열 이름은 배열의 첫 주소를 가리키고 <U>별도의 메모리에 배열의 첫 주소를 저장해두지는 않음</U>

즉 **배열**은 연속적으로 할당된 데이터가 본체이며, 별도의 변수에 첫 원소를 가리키는 주소를 담지 않는다는 것이, 별도의 공간에 가리키는 변수의 주소를 저장하는 **포인터**와 큰 차이점을 지닌다.

<br>
<br>

![LocalVariableImage](/Images/ArrayVsPointer1.png) 

위 스샷을 보면, Hello World 라는 문자열은 const char []형 으로 상수 배열의 특징을 가지며, 데이터 섹션-> .rod 섹션에 저장되어 있다.    

![LocalVariableImage](/Images/ArrayVsPointer2.png) 
![LocalVariableImage](/Images/ArrayVsPointer3.png) 

(데이터 섹션의 Hello World 저장 부분)

<br>
<br>

![LocalVariableImage](/Images/ArrayVsPointer4.png) 
const char* 형 포인터에 이것을 저장하는 경우, 디스어셈블러를 확인해보면 .rod 섹션에 저장된 해당 문자열의 첫번째 시작 주소(0X00307BCC)를 포인터에 다이렉트로 저장하는것을 확인할 수 있다.

<br>
<br>

![LocalVariableImage](/Images/ArrayVsPointer5.png)

![LocalVariableImage](/Images/ArrayVsPointer6.png) 

반면 char []형 배열의 경우에는, 데이터 섹션의 첫 원소 주소를 저장하는 것이 아니라,  main 함수의 시작 스택 포인터 ebp 에서 -22 를 한 msg 변수부터 4바이트 단위로 Hello World가 담긴 .rod 섹션의 원소들을 복사하여 배열에 저장한다.

![LocalVariableImage](/Images/ArrayVsPointer7.png) 

![LocalVariableImage](/Images/ArrayVsPointer8.png) 

이렇게 4바이트씩 배열에 복사하여 저장하고, 배열 변수 자체는 첫 원소가 저장된 주소를 가리킨다.