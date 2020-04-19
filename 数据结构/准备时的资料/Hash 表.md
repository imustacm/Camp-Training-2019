## Hash 表

###### 作用：数据整理以便查询

#### 数据结构模板

##### 链地址法

``` cpp
const int M;

vector<int> nums[M];

int hashCode(int num){
    return num % M;		//此处非固定
}

void insert(int num){
    nums[hashCode(num)].push_back(num);
}

bool search(int num){
    for(int i = 0;i < nums[hashCode(num)].size();i++)
        if(nums[hashCode(num)][i] == num)
            return true;
    return false;
}
```

##### 开放地址法

``` cpp
const int M;

int nums[M];

int hashCode(int num){
    return num % M;		//此处非固定
}

void insert(int num){		//线性探测法
    if(nums[hashCode(num)] == 0)	//我们假设0代表这个位置没有值
        nums[hashCode(num)] = num;
    else{
        for(int i = 0;i < M;i++)
            if(nums[(hashCode(num) + i) % M] == 0){
                nums[(hashCode(num) + i) % M] = num;
                break;
            }
    }
}

bool search(int num){		//线性探测法的搜索
    if(nums[hashCode(num)] == num)
        return true;
    
    for(int i = 0;i < M;i++)
        if(nums[hashCode(num) + i] == num)
            return true;
    return false;
}

void insert(int num){		//平方探测法
    if(nums[hashCode(num)] == 0)
        nums[hashCode(num)] = num;
    else{
        for(int i = 0;i < (int)sqrt(M);i++)
            if(nums[(hashCode(num) + i * i) % M] == 0){
                nums[(hashCode(num) + i * i) % M] = num;
                return ;
            }
        	else if(nums[(hashCode(num) - i * i + M) % M] == 0){
                nums[(hashCode(num) + i * i + M) % M] = num;
                return ;
            }
    }
}

bool search(int num){		//平方探测法的搜索
    if(nums[hashCode(num)] == num)
        return true;
    
    for(int i = 0;i < (int)sqrt(M);i++)
        if(nums[(hashCode(num) + i * i) % M] == num){
            return true;
        }
        else if(nums[(hashCode(num) - i * i + M) % M] == num){
            return false;
        }
}
```

