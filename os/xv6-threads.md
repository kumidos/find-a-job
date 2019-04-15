#### 关于 thread create 和 thread join
```c
int thread_create(void (*start_routine)(void*, void*), void* arg1, void* arg2)
{
  void* freeptr = malloc(PGSIZE*2);
  void* stack;
  if(freeptr == 0)
    return -1;
  if((uint)freeptr % PGSIZE == 0)
    stack = freeptr;
  else
    stack = freeptr + (PGSIZE - ((uint)freeptr % PGSIZE));
  for(int i = 0; i < MAX_PROC; i++){
    if(ptrs[i].busy == 0){
      ptrs[i].ptr = freeptr;
      ptrs[i].stack = stack;
      ptrs[i].busy = 1;
      break;
    }
  }
  int ret = clone(start_routine, arg1, arg2, stack);
  return ret;
}

int thread_join()
{
  void* stack;
  int ret = join(&stack);
  for(int i = 0; i < MAX_PROC; i++){
    if(ptrs[i].busy == 1 && ptrs[i].stack == stack){
      free(ptrs[i].ptr);
      ptrs[i].stack = NULL;
      ptrs[i].busy = 0;
      ptrs[i].ptr = NULL;
      break;
    }
  }
  return ret;
}
```
#### 为实现 threads 内核中的改动
- clone  join 复制原数据， 从func开始运行新的程序栈
- wait里跳过 thread 
- sbrk 
