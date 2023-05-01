# 책 : 커맨드라인 27장

# 흐름제어 : if 분기

## 프로그램의 분기란?

사용자 권한에 따라 결과를 조정하는 방법(방향을 바꾸는 방법) 

스크립트 내에서 테스트 결과에 따라 “방향을 바꾸는” 방법

## if 사용법

```
if commands; then
	commands
[elif commands; then
	commands...]
[else
	commands]
fi
```

### 종료상태

명령어들(우리가 작성하고 있는 스크립트와 쉘 함수를 모두 포함한 의미)은 종료될 떄 종료 상태(exit status)라는 값을 생성함. 

일반적으로 0은 성공, 다른 숫자는 실패. 

## test의 사용법

test expression

[expression]

두 가지 형태로 쓰이며, expression에는 명령어 성공 여부를 검사하는 표현식이 들어감. 

이 표현식이 참이면 0, 거짓이면 1의 종료 상태 값을 반환함. 

### 파일 표현식에서의 test 사용법

file 표현식은 다음과 같다. 

![LC2700](/src/polytech/suyoung/img/LC27/Untitled.png)

파일 표현식을 확인할 수 있는 스크립트는 

```
# ! / bin/ bash 
 
# test-file: Evaluate the status of a file 
 
FILE=~/ . bashre 
 
if [ -e "$FILE" ] ; then
				 if [ - f "$FILE" ]; then 
							echo "$FILE is a regular file . " 
				 fi 
				 if [ -d "$FILE" ]; then 
						  echo "$FILE is a directory."
				 fi 
				 if [ -r "$FILE" ]; then 
							echo "$FILE is readable . " 
				 fi 
				 if [ -w "$FILE" ]; then 
							echo "$FILE is writable."
				 fi 
				 if [ -x "$ FILE" ] ; then 
							echo "$FILE i s executable/searchable."
				 fi 
else 
				 echo "$FILE does not exist" 
				 exit 1 
 
fi
 
exit
```

1. $FILE 매개변수가 표현식 내에서 사용될 때 따옴표로 인용됨
2. 스크립트 끝 부분의 exit 명령어는 선택적으로 하나의 명령 인자와 함께 사용될 수 있는데 이 인자는 스크립트의 종료 상태를 나타

### 문자열 표현식에서의  test 사용법

문자열 표현식은 다음과 같다

![LC2701](/src/polytech/suyoung/img/LC27/Untitled%201.png)

예제

```
#!/bin/ bash 
 
# test-string: evaluate the value of a string 
 
ANSWER=maybe 
 
if [ -z "$ANSWER" ]; then 
		 echo "There is no answer . " >&2
		 exit 1  
fi 
 
if [ "$ANSWER" = "yes " ] ; then 
		 echo "The answer is YES."
elif [ "$ANSWER" = "no" ] ; then 
		 echo "The answer is NO." 
elif [ "$ANSWER" = "maybe" ] ; then 
		 echo "The answer is MAYBE . " 

else 
		 echo "The answer is UNKNOWN." 
 
fi
```

### 정수 표현식에서의 test 사용법

![LC2702](/src/polytech/suyoung/img/LC27/Untitled%202.png)

예제

```
#!/bin/bash 
 
# test-integer: evaluate the value of an integer. 
 
INT=-5 
 
if [ -z "$INT" ] ; then 
			echo "INT is empty." >&2 
			exit 1 
 
fi 
 
if [ $INT -eq 0 ]; then 
			echo " INT is zero . " 
else 
				if [ $INT _ lt 0 ]; then 
								echo "INT is negative."
				else 
								echo "INT is positive." 
				fi 
				if [ $((INT % 2) ) -eq 0 ] ; then 
								echo "INT is even."
				else 
									echo "INT is odd . "
				fi
fi
```

2로 나눈 나머지값을 계산하는 모듈로 연산을 사용, 결과로 짝,홀을 판단함. 

### 현대식 테스트

bash의 최신버전에는 test의 역할을 대신하는 합성명령어 [[expression]을 지원.

expression에는 참/거짓을 판단하는 표현식을 입력(string1 =~ regex) 

예시

```
#!/bin/bash 
 
# test - integer2: evaluate the value of an integer. 
 
INT= - 5 
 
if [[ "$INT" =~ "- ?[0-9]+$ ]]; then 
				if [ $INT - eq 0 ] ; then 
									echo "INT is zero ."
				else 
									if [ $INT -lt 0 ] ; then 
													echo "INT is negative." 
									else 
													echo "INT i s positive." 
									fi 
									if [ $( ( INT % 2) ) -eq 0 ] ; then 
													echo "INT i s even . " 
									else 
													echo "INT i s odd. " 
									fi 
				fi 
 
else 
				echo "INT is not an integer." >&2
				exit 1  
fi
```

### (())-정수 테스트

bash는 [[ ]] 합성 명령어뿐만 아니라 (( )) 명령식 또한 지원

(( )) 명령식은 산술식의 찹 여부를 검사하고, 이 명령은 산술식의 결과가 0 이 아니면 참 값을 반환함. 

```
#!/bin/bash 
 
# test-integer2a: evaluate the value of an integer. 
 
INT=-5 
 
if [[ "$INT" =~ "-?[0-9]+$ ]]; then 
				if (( INT == 0) ) ; then 
										echo "INT is zero."
				else
						 if ((INT < 0) ) ; then 
												echo "INT is negative."
						 else 
												echo "INT is positive." 
						 fi
						 if (( ((INT % 2) ) == 0) ) ; then 
												echo "INT is even."
						 else 
												echo "INT is odd." 
						 fi 
				fi 
 else 
				echo "INT is not an integer." >&2
				exit 1  
fi
```

### 표현식 조합

논리 연산자를 이용함으로서 조합 가능 

![LC2703](/src/polytech/suyoung/img/LC27/Untitled%203.png)

AND 연산 예시

```
#!/bin/bash 
 
# test - integer3 : determine if an integer is within a 
# specified range of values. 
 
MIN_VAL=l 
MAX_VAL=100 
 
INT=50 
 
if [[ "$INT" =~ " -?[0-9]+$ ]]; then 
				if [ [ INT -ge MIN_VAL && INT -le MAX_VAL ]] ; then
							 echo "$INT is within $MIN_VAL to $MAX_VAL." 
				else 
							 echo "$INT is out of range." 
 
				fi
else 
				echo "INT is not an integer." >&2
				exit 1
fi
```