# 문제
![20200308_215901](https://user-images.githubusercontent.com/51700219/76163285-2e646780-6188-11ea-86b1-7338d4ca8b7d.png)

# 풀이
- 정렬된 상태이므로 각 행에 대하여 -1 이하인 숫자의 인덱스를 바이너리서치로 찾아주면 된다.

~~~python
def binary_search_descending(list, value):
  lo = 0
  hi = len(list)-1
  mid = (lo+hi)//2
  
  while lo <= hi:

    if list[mid] == value:
      while list[mid-1] == value:
        mid -= 1
      return mid
    elif list[mid] > value:
      lo = mid+1
      mid = (lo+hi)//2
    else:
      hi = mid-1
      mid = (lo+hi)//2
  
  return -1
~~~

- 위 코드에서 `mid = (lo+hi)//2` 를 두번 하므로 보기 안좋다. while문 시작 부분으로 옮겨주자.
~~~python
def binary_search_descending(list, value):
  lo = 0
  hi = len(list)-1
  mid = (lo+hi)//2
  
  while lo <= hi:
    mid = (lo+hi)//2
    if list[mid] == value:
      while list[mid-1] == value:
        mid -= 1
      return mid
    elif list[mid] > value:
      lo = mid+1
    else:
      hi = mid-1
  
  return -1
~~~
- 여기서 문제가 있는데
  - 첫번째로 [1, -1, -1, -1, -1] 같은 경우에는 1을 반환해줘야 하는데 2를 반환해준다.
  - 두번째로 [1, 0, -3, -4, -4] 같은 경우에는 2 반환해줘야하는데 -1을 찾지 못해서 -1을 반환한다.
  - 파이썬의 bisect 처럼 최초로 조건을 만족하는 부분을 찾아 주도록 바꿀 필요가 있음.
