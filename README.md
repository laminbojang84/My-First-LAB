# Лабораторная работа №1
## Выполнил студент группы БСТ2201 Боджанг.М.Л

### Задание №1
<i> Вызвать функцию print() и передать туда строку Hello, World! </i>

print("Hello,World!")

### Задание №2
нужно написать генератор случайных многомерных матриц (возможность ввода значений предоставляется пользователю)


import random

def generate_random_matrix():

    m = int(input("Введите количество строк в матрице: "))
    
    n = int(input("Введите количество столбцов в матрице: "))
    
    min_limit = int(input("Введите минимальное значение для генерации случайных чисел: "))
    
    max_limit = int(input("Введите максимальное значение для генерации случайных чисел: "))
    
    # Генерация случайной матрицы заданной размерности
    random_matrix = [[random.randint(min_limit, max_limit) for _ in range(n)] for _ in range(m)]
    
    return random_matrix

 Пример использования генератора случайных многомерных матриц

random_matrix = generate_random_matrix()

print("Случайная матрица:")

for row in random_matrix:

    print(row)



   ### Задание №3
Реализовать методы сортировки строк числовой матрицы в соответствии с
заданием. 

def insertion_sort(arr):

     for i in range(1, len(arr)):
     
         key = arr[i]
         
         j = i - 1
         
         while j >= 0 and key < arr[j]:
         
             arr[j + 1] = arr[j]
             
             j -= 1
             
         arr[j + 1] = key

             
#Пример исползования

arr = [35,18, 65, 10,7] 

insertion_sort(arr)

print("вставка отсортирована:", arr)


def bubble_sort(arr):
    n = len(arr)

    for i in range(n):
    
         for j in range(0, n-i-1):
         
             if arr[j] > arr[j+1]:
             
                 arr[j], arr[j+1]= arr[j+1], arr[j]

    return arr

#Пример использования

arr = [75, 33, 19, 14, 29, 44, 98]

sorted_arr = bubble_sort(arr)

print("отсортированный пузырь :", sorted_arr)


def selection_sort(arr):
    n = len(arr)
    
    for i in range(n):
    
        min_index = i
        
        for j in range(i+1, n):
        
            if arr[j] < arr[min_index]:
            
                min_index = j 
                
        arr[i], arr[min_index] = arr[min_index], arr[i]


arr = [75, 31, 14, 25, 112]
selection_sort(arr)
print("выбор отсортирован:", arr)


def shell_sort(arr):
    n = len(arr)
    gap = n // 2
    while gap > 0:
        for i in range(gap, n):
            temp = arr[i]
            j = i
            while j >= gap and arr[j - 
gap] > temp:
                 arr[j] = arr[j - gap]
                 j -= gap
            arr[j] = temp
        gap //=2

arr = [102, 34, 54, 18, 3]
     
shell_sort(arr)
print("отсортировала Шелла:", arr)


                def quick_sort(arr):
    if len(arr) <=1:
        return arr
    else:
        pivot = arr[0]
        less = [x for x in arr[1:]
if x <= pivot]
        greater = [x for x in arr[1:
] if x > pivot]
        return quick_sort(less) + [
pivot] + quick_sort(greater)
        
arr = [20, 15, 10, 150, 1, 2, 15]
sorted_arr = quick_sort(arr)
print("Быстрая сортировка :",sorted_arr)


import random

def random_matrix(m=3, n=3, min_limit=1,
max_limit=10):
    return [[random.randint(min_limit,
max_limit) for _ in range(n)] for _ in
range(m)]


matrix = random_matrix(5, 5, 0, 300)
for row in matrix:
    print(row)



    def tournament_sort(arr):
    n = len(arr)
    tree = [None] * (2*n - 1)

    def build_tree(node, start, end):
        if start == end:
            tree[node] = start
            return
        mid = (start + end) // 2
        build_tree(2*node+1, start, mid)
        build_tree(2*node+2, mid+1, end)
        if arr[tree[2*node+1]] < arr[tree[2*node+2]]:
            tree[node] = tree[2*node+1]
        else:
            tree[node] = tree[2*node+2]

    def query_tree(node, start, end, qstart, qend):
        if start > qend or end < qstart:
            return -1  # Invalid range
        if start >= qstart and end <= qend:
            return tree[node]
        mid = (start + end) // 2
        left = query_tree(2*node+1, start, mid, qstart, qend)
        right = query_tree(2*node+2, mid+1, end, qstart, qend)
        if left == -1:
            return right
        elif right == -1:
            return left
        elif arr[left] < arr[right]:
            return left
        else:
            return right

    def update_tree(node, start, end, idx):
        if start == end:
            return
        mid = (start + end) // 2
        if idx <= mid:
            update_tree(2*node+1, start, mid, idx)
        else:
            update_tree(2*node+2, mid+1, end, idx)
        if arr[tree[2*node+1]] < arr[tree[2*node+2]]:
            tree[node] = tree[2*node+1]
        else:
            tree[node] = tree[2*node+2]

    build_tree(0, 0, n-1)

    sorted_arr = []
    for i in range(n):
        idx = query_tree(0, 0, n-1, 0, n-1)
        sorted_arr.append(arr[idx])
        arr[idx] = float('inf')  # Infinity as a placeholder
        update_tree(0, 0, n-1, idx)

    return sorted_arr
    
arr = [29, 10, 14, 37, 13]
sorted_arr = tournament_sort(arr)
print("Отсортированный массив:")
print(sorted_arr)



import timeit

def print_hello_world():
    print("Hello, World!")

for func in [print_hello_world, bubble_sort, quick_sort, shell_sort, selection_sort, tournament_sort]:

    if func.__name__ == "print_hello_world":
    
        time_taken = timeit.timeit(func, number=1)
    else:
        arr = [random.randint(1, 1000) for _ in range(1000)]
        
        time_taken = timeit.timeit(lambda: func(arr.copy()), number=1)
        
    print(f"{func.__name__}: {time_taken:.6f} seconds")

Hello, World!

print_hello_world: 0.000252 seconds

bubble_sort: 0.000034 seconds

quick_sort: 0.000032 seconds

shell_sort: 0.000029 seconds

selection_sort: 0.000033 seconds

tournament_sort: 0.000037 seconds
