# 自己写的代码
1、存在的问题，循环输入两次4个1之后报错\

   解决办法：正在调试查找
   
   TypeError: list indices must be integers or slices, not str
   
   字典与列表之间数据传递的时候出现混淆现象
   
   列表操作 append（）
   字典操作 info['key']=name
   
   人员信息存储是使用列表里面嵌套字典，实现元素的多元化


```python
#全局变量的定义
#创建一个空字典用于存储所有成员

info=[]

#函数定义声明
def in_sys():
    """界面显示"""
    print('欢迎来到学员管理系统')
    print('1、添加学员')
    print('2、删除学员')
    print('3、修改学员信息')
    print('4、查询学员信息')
    print('5、显示所有学员信息')
    print('6、退出系统')
    
def add_people():
    """添加学员"""
    add_id = input('请输入学号：')
    add_name = input('请输入姓名：')
    add_tel = input('请输入手机号：')

    global info
    flag=0  
    #立一个标志 0说明添加新用户，用户重复
    for i in info:
        if i['name']==add_name:
            print('此用户已经存在')
            flag=1
            #立一个标志 0说明添加新用户，用户重复
            return 
    '''
    info['id'] = add_id
    info['name'] = add_name
    info['tel'] = add_tel    
    '''
    # 2.2 如果输入的姓名不存在，添加数据：准备空字典，字典新增数据，列表追加字典
    
    info_dict = {}

    # 字典新增数据
    info_dict['id'] = add_id
    info_dict['name'] = add_name
    info_dict['tel'] = add_tel
    # print(info_dict)

    # 列表追加字典
    info.append(info_dict)
    print(info)
    
    
def del_people():
    """删除学员"""
    del_name=input('请输入要删除学员的名字：')
    
    global info
    
    for i in info:
        if i['name']==del_name:
            info.remove(i)            
            print('成员删除成功')
            break
        else:
            print('您输入的有误，没有该成员',del_name)
def modefy_people():   
    
    modefy_name = input('请输入要修改学员的名字：')
    
    for i in info:
        if i['name']==modefy_name:
            i['tel']= input('请输入要修改学员的电话：')          
            print('成员修改成功')
            break
        else:
            print('您输入的有误，没有该成员',del_name)    
def search_people():   
    
    search_name = input('请输入要查询学员的名字：')
    
    for i in info:
        if i['name']==search_name:          
            print('成员已查到，为',i)
            break
        else:
            print('您输入的有误，没有该成员',del_name)        

#主程序
in_sys()

while 1:
    num = int(input('请输入选择序号：'))
    print('您输入选择序号为：',num)
    if num==1:
        print('开始添加学员')
        add_people()
        
    elif num==2:
        print('开始删除学员')
        del_people()
        
    elif num==3:
        print('修改学员信息')
        modefy_people()
    elif num==4:
        print('查询学员信息')
        search_people()
    elif num==5:
        print('显示所有学员信息')
        global info
        print(info)
    elif num==6:
        ms=input('yes or not？')
        while ms != "yes":
            break
        if ms == "yes":
            print('退出系统')
            break
            
    else:
        print('您输入的序号有误，请重新输入')
        
    in_sys()
```

# 案例代码
目标：读懂代码，和自己写的代码进行比较


```python
# 定义功能界面函数
def info_print():
    print('请选择功能--------------')
    print('1、添加学员')
    print('2、删除学员')
    print('3、修改学员')
    print('4、查询学员')
    print('5、显示所有学员')
    print('6、退出系统')
    print('-' * 20)


# 等待存储所有学员的信息
info = []


# 添加学员信息的函数
def add_info():
    """添加学员函数"""
    # 1. 用户输入：学号、姓名、手机号
    new_id = input('请输入学号：')
    new_name = input('请输入姓名：')
    new_tel = input('请输入手机号：')

    # 2. 判断是否添加这个学员：如果学员姓名已经存在报错提示；如果姓名不存在添加数据
    global info
    # 2.1 不允许姓名重复：判断用户输入的姓名 和 列表里面字典的name对应的值 相等 提示
    for i in info:
        if new_name == i['name']:
            print('此用户已经存在')
            # return作用：退出当前函数，后面添加信息的代码不执行
            return

    # 2.2 如果输入的姓名不存在，添加数据：准备空字典，字典新增数据，列表追加字典
    info_dict = {}

    # 字典新增数据
    info_dict['id'] = new_id
    info_dict['name'] = new_name
    info_dict['tel'] = new_tel
    # print(info_dict)

    # 列表追加字典
    info.append(info_dict)
    print(info)


# 删除学员
def del_info():
    """删除学员"""
    # 1. 用户输入要删除的学员的姓名
    del_name = input('请输入要删除的学员的姓名：')

    # 2. 判断学员是否存在：存在则删除；不存在提示
    # 2.1 声明info是全局变量
    global info
    # 2.2 遍历列表
    for i in info:
        # 2.3 判断学员是否存在：存在执行删除(列表里面的字典)，break：这个系统不允许重名，删除了一个后面的不需要再遍历；不存在提示
        if del_name == i['name']:
            # 列表删除数据 -- 按数据删除remove
            info.remove(i)
            break
    else:
        print('该学员不存在')

    print(info)


# 修改函数
def modify_info():
    """修改学员信息"""
    # 1. 用户输入想要修改的学员您的姓名
    modify_name = input('请输入要修改的学员的姓名：')

    # 2. 判断学员是否存在：存在修改手机号；不存在，提示
    # 2.1 声明info是全局
    global info
    # 2.2 遍历列表，判断输入的姓名==字典['name']
    for i in info:
        if modify_name == i['name']:
            # 将tel这个key修改值，并终止此循环
            i['tel'] = input('请输入新的手机号：')
            break
    else:
        # 学员不存在
        print('该学员不存在')

    # 3. 打印info
    print(info)


# 查询学员信息函数
def search_info():
    """查询学员信息"""
    # 1. 用户输入目标学员姓名
    search_name = input('请输入要查询的学员的姓名：')

    # 2. 检查学员是否存在：存在打印这个学员的信息；不存在则提示
    # 2.1 声明info为全局
    global info
    # 2.2 遍历info，判断输入的学员是否存在
    for i in info:
        if search_name == i['name']:
            # 学员存在：打印信息并终止循环
            print('查询到的学员信息如下---------------')
            print(f"学员的学号是{i['id']}, 姓名是{i['name']}, 手机号是{i['tel']}")
            break
    else:
        # 学员不存在的提示
        print('查无此人...')


# 显示所有学员信息
def print_all():
    """显示所有学员信息"""
    # 1. 打印提示字
    print('学号\t姓名\t手机号')
    # 2. 打印所有学员的数据
    for i in info:
        print(f"{i['id']}\t{i['name']}\t{i['tel']}")


# 系统功能需要循环使用，直到用户输入6，才退出系统
while True:
    # 1. 显示功能界面
    info_print()

    # 2. 用户输入功能序号
    user_num = int(input('请输入功能序号：'))

    # 3. 按照用户输入的功能序号，执行不同的功能(函数)
    # 如果用户输入1，执行添加；如果用户输入2，执行删除... -- 多重判断
    if user_num == 1:
        # print('添加')
        add_info()
    elif user_num == 2:
        # print('删除')
        del_info()
    elif user_num == 3:
        # print('修改')
        modify_info()
    elif user_num == 4:
        # print('查询')
        search_info()
    elif user_num == 5:
        # print('显示所有')
        print_all()
    elif user_num == 6:
        # print('退出系统')
        # 程序要想结束，退出终止while True -- break
        exit_flag = input('确定要退出吗？yes or no')
        if exit_flag == 'yes':
            break
    else:
        print('输入的功能序号有误')


```

    请选择功能--------------
    1、添加学员
    2、删除学员
    3、修改学员
    4、查询学员
    5、显示所有学员
    6、退出系统
    --------------------
    请输入功能序号：1
    请输入学号：1
    请输入姓名：1
    请输入手机号：1
    [{'id': '1', 'name': '1', 'tel': '1'}]
    请选择功能--------------
    1、添加学员
    2、删除学员
    3、修改学员
    4、查询学员
    5、显示所有学员
    6、退出系统
    --------------------
    请输入功能序号：6
    确定要退出吗？yes or noyes
    
