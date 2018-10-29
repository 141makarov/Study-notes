# django
## 安装
### Django与Python版本对应关系
### 安装过程
* 进入黑屏终端
* 输入 pip install Django==1.11.4
* 等待安装，出现如上所示表示安装成功
* 验证是否安装成功
    * 进入Python环境
>>>import Django
>>>django.get_version()
## 创建项目
### 在合适的位置创建一个目录
### 打开黑屏终端，进入上一步创建的目录下
### 输入<django-admin startproject firstpt>
### 目录层级说明
* manage.py
    * 一个命令行工具，可以使我们用多种方式对Django项目进行交互
* project目录
    * __init__.py
        * 一个空文件，告诉python这个目录应该被看作一个python包
    * setting.py
        * 项目的配置文件
    * urls.py
        * 项目的URL声明
    * wsgi.py
        * 项目与WSGI兼容的Web服务器入口
## 基本操作
### 设计表结构
* 班级表结构
    * 表名
        * grades
    * 字段
        * 班级名称
            * gname
        * 成立时间
            * gdate
        * 女生总数
            * ggirlnum
        * 男生总数
            * gboynum
        * 是否删除
            * isDelete
* 学生表结构
    * 表名
        * students
    * 字段
        * 学生姓名
            * sname
        * 学生性别
            * sgender
        * 学生年龄
            * sage
        * 学生简介
            * scontend
        * 所属班级
            * sgrade
        * 是否删除
            * isDelete
### 配置数据库
* 注意：Django默认使用SQLite数据库
* 在setting.py文件中，通过DATABASES选项进行数据库配置
* 配置MySQL
    * Python3.x 安装的是PyMySQL
    * 在__init__.py文件中写入两行代码
        * import pymysql
pymysql.install_as_MySQLdb()
    * 格式
        * DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 数据库名,
        'USER': 用户名,
        'PASSWORD': 数据库密码,
        'HOST': 数据库服务器ip,
        'port': '3306',
    }
}

    * 配置示例
        * DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'firstpt',
        'USER': 'root',
        'PASSWORD': '',
        'HOST': 'localhost',
        'port': '3306',
    }
}

### 创建应用
* 在一个项目中可以创建多个应用，每个应用对应一种业务处理
* 打开黑屏终端，进入first目录下的firstpt目录
* 执行<python manage.py startapp myApp>
* myApp目录说明
    * admin.py
        * 站点配置
    * model.py
        * 模型
    * views.py
        * 视图
### 激活应用
* 在setting.py文件中，将myApp应用加入到INSTALLED_APPS选项中
* INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myApp',
]
### 定义模型
* 概述：一个数据表对应一个模型
* 在models.py文件中定义模型
    * from django.db import models
    * 模型类要继承models.Model类
    * from django.db import models

# Create your models here.

class Grades(models.Model):
    gname         = models.CharField(max_length=20)
    gdate           = models.DateField()
    ggirlnum     = models.IntegerField()
    gboynum    = models.IntegerField()
    isDelete      = models.BooleanField(default=False)

class Students(models.Model):
    sname      = models.CharField(max_length=20)
    sgender   = models.BooleanField()
    sage         = models.IntegerField()
    scontend  = models.CharField(max_length=20)
    isDelete   = models.BooleanField(default=False)
    #关联外键
    sgrade     = models.ForeignKey("Grades"，on_delete=models.DO_NOTHING)
* 说明
    * 不需要定义主键，在生成时自动添加，并且值为自动增加
### 在数据库中生成数据表
* 生成迁移文件
    * 执行<python manage.py makemigrations>
        * 在migrations目录下生成一个迁移文件，此时数据库中还没有生成数据表
* 执行迁移
    * 执行<python manage.py migrate>
    * 相当于执行sql语句创建数据表
### 测试数据操作
* 进入到Python shell
    * 执行<python manage.py shell>
        * 
* 引入包
    * from myApp.models import Grades,Students
from django.utils import timezone
from datetime import *
* 查询所有数据
    * 类名.objects.all()
    * Grades.objects.all()
* 添加数据
    * 本质：创建一个对象的模型实例
    * grade1 = Grades()
grade1.gname = "django1"
grade1.gdate = datetime(year=2018,month=9,day=13)
grade1.ggirlnum = 23
grade1.gboynum = 56
grade1.save()
* 查看某个对象
    * 类名.objects.get(pk=id)
    *  Grades.objects.get(pk=2)
* 修改数据
    * 模型对象.属性=新值
    * grade2.gboynum = 55
grade2.save()
* 删除数据
    * 模型对象.delete()
    * grade2.delete()
    * 注意：物理删除，数据库中的表里的数据被删除了
* 关联对象
    *  stu = Students()
 stu.sname = "Alice"
 stu.sgender = False
 stu.sage = 20
 stu.scontend = "I'm Alice."
 stu.sgrade = grade1
 stu.save()
    * 获得关联对象的集合
        * 需求：获取django1班级的所有学生
        * 对象名.关联的类名小写_set.all()
        * grade1.students_set.all()
    * 需求：创建曾志伟，属于django1班学生
        * stu3 = grade1.students_set.create(sname=u'曾志伟',sgender=True,scontend=u'曾志伟',sage=45)
        * 注意：直接添加到数据库中
### 启动服务器
* 格式
    * python manage.py runserver ip:port
    * ip可以不写，代表本机ip
    * 端口号默认是8000
    * python manage.py runserver
* 说明
    * 这是一个纯python写的轻量级web服务器，仅仅在开发测试中使用
### Admin站点管理
* 概述
    * 内容发布
        * 负责添加、修改、删除内容
    * 公告访问
* 配置Admin应用
    * 在setting.py文件中的INSTALLED_APPS中添加 'django.contrib.admin',
        * 默认是已经添加好的
* 创建管理员用户
    * 执行< python manage.py createsuperuser>,依次输入用户名、邮箱、密码
* 汉化
    * 修改setting.py文件
        * LANGUAGE_CODE = 'zh-Hans'
TIME_ZONE = 'Asia/Shanghai'
* 管理数据表
    * 修改admin.py文件
        * from .models import Grades,Students
#注册
admin.site.register(Grades)
admin.site.register(Students)
    * 自定义管理页面
        * from .models import Grades,Students
#注册
class GradesAdmin(admin.ModelAdmin):
    # 列表页属性
    list_display = ['pk', 'gname', 'gdate', 'ggirlnum', 'gboynum', 'isDelete']
    list_filter = ['gname']
    search_fields = ['gname']
    list_per_page = 5

    # 添加、修改页属性
    # fields = ['ggirlnum', 'gboynum', 'gname', 'gdate', 'isDelete']
    fieldsets = [
        ("num", {"fields":["ggirlnum", "gboynum"]}),
        ("base", {"fields":['gname', 'gdate', 'isDelete']}),
    ]
admin.site.register(Grades, GradesAdmin)
        * 属性说明
            * 列表页属性
                * list_display = []
                    * 显示字段
                * list_filter = []
                    * 过滤字段
                * search_fields = []
                    * 搜索字段
                * list_per_page =
                    * 分页
            * 添加、修改页属性
                *  fields = []
                    * 规定属性的先后顺序
                * fieldsets = []
                    * 给属性分组
                * 注意：field与fieldsets不能同时使用
        * 关联对象
            * 需求：在创建一个班级时，可以直接添加几个学生
            * class StudentsInfo(admin.TabularInline):
    model = Students
    extra = 2
class GradesAdmin(admin.ModelAdmin):
    inlines = [StudentsInfo]
        * 布尔值显示问题
            * class StudentsAdmin(admin.ModelAdmin):
    def gender(self):
        if self.sgender:
            return "男"
        else:
            return "女"

    gender.short_description = "性别"
    # 列表页属性
    list_display = ['pk', 'sname', 'sage', gender, 'scontend','sgrade', 'isDelete']
    list_filter = ['sname']
    search_fields = ['sname']
    list_per_page = 5

admin.site.register(Students, StudentsAdmin)
        * 执行动作的位置
            * class StudentsAdmin(admin.ModelAdmin):
    def gender(self):
        if self.sgender:
            return "男"
        else:
            return "女"

    gender.short_description = "性别"
    # 列表页属性
    list_display = ['pk', 'sname', 'sage', gender, 'scontend','sgrade', 'isDelete']
    list_filter = ['sname']
    search_fields = ['sname']
    list_per_page = 5

    #执行动作的位置
    actions_on_bottom = True
    actions_on_top = False
admin.site.register(Students, StudentsAdmin)
    * 使用装饰器完成注册
        * @admin.register(Students)
class StudentsAdmin(admin.ModelAdmin):
    def gender(self):
        if self.sgender:
            return "男"
        else:
            return "女"

    gender.short_description = "性别"
    # 列表页属性
    list_display = ['pk', 'sname', 'sage', gender, 'scontend', 'sgrade', 'isDelete']
    list_filter = ['sname']
    search_fields = ['sname']
    list_per_page = 5

    #执行动作的位置
    actions_on_bottom = True
    actions_on_top = False
#admin.site.register(Students, StudentsAdmin)
### 视图的基本使用
* 概述
    * 在Django中，视图对web请求进行回应
    * 视图是一个python函数，在views.py文件中定义
* 定义视图
    * from django.http import  HttpResponse
# request:浏览器给服务器的一个东西
def index(request):
    return HttpResponse("This is a practice.")
* 配置url
    * 修改firstpt目录下的urls.py文件
        * from django.contrib import admin
from django.conf.urls import url, include

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^', include('myApp.urls')),
]
    * 在myapp.py应用目录下创建一个urls.py文件
        * from django.conf.urls import url

from . import views

urlpatterns = [
    url(r'^$', views.index)
]
### 模板的基本使用
* 概述
    * 模板是HTML页面，可以根据视图中传递过来的数据进行填充
* 创建模板
    * 创建templates目录，在目录下创建对应项目的模板目录（firstpt/templates/myApp）
    * 配置路径
        * 修改settings.py文件下的TEMPLATES
            * TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
        'APP_DIRS': True,
    * 定义grades.html和students.html模板
        * 模板语法
            * {{输出值，可以是变量，也可以是对象属性值}}
            * %执行代码段%
    * http://http://127.0.0.1:8000/grades
        * 写grades.html模板
            * <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>班级信息</title>
</head>
<body>
    <h1>班级信息列表</h1>
    <ul>
        <!--[django1,django2]-->
        {%for grade in grades%}
        <li>
            <a href="#">{{grade.gname}}</a>>
        </li>
        {%endfor%}
    </ul>
</body>
</html>
        * 定义视图
            * from .models import  Grades

def grades(request):
    #模型取数据
    gradesList = Grades.objects.all()
    #将数据传递给模板，模板再渲染页面，将渲染好的页面返回给浏览器
    return render(request, 'myApp/grades.html', {'grades':gradesList})
        * 配置url
            * from . import views

urlpatterns = [
    url(r'^$', views.index),
    url(r'^(\d+)/(\d+)/$', views.detail),
    url(r'^grades/$', views.grades),
]
    * 点击班级，显示对应班级的所有学生
        * 定义视图
            * def gradesStudents(request,num):
    #获得对应的班级对象
    grade = Grades.objects.get(pk=num)
    #获得班级下的所有学生
    studentsList = grade.students_set.all()
    return render(request, 'myApp/students.html', {"students":studentsList})
        * 配置url
            *    url(r'^grades/(\d+)/$', views.gradesStudents),
## 流程梳理
### 创建工程
* 执行<django-admin startproject project>
### 创建项目
* 执行<python manage.py startapp myApp>
### 激活项目
* 修改setting.py中的INSTALLED_APPS
### 配置数据库
* 修改__init__.py
    * import pymysql
pymysql.install_as_MySQLdb()
* 修改setting.py文件中的DATABASES
    * DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'firstpt',
        'USER': 'root',
        'PASSWORD': '',
        'HOST': 'localhost',
        'port': '3306',
    }
}
### 创建模型类
* 在项目目录下的models.py文件中
### 生成迁移文件
* 执行<python manage.py makemigrations>
### 执行迁移
* 执行<python manage.py migrate>
### 配置站点
### 创建模板目录、项目模板目录
### 在setting.py文件目录中TEMPLATES配置模板路径
### 在project下修改urls.py
### 在项目目录下创建urls.py
## 模型
### Django对各种数据库提供了很好的支持，Django为这些数据库提供了统一的API，可以根据不同的业务需求选择不同的数据库。
### 配置数据库
* 修改工程目录下的__init__.py文件
    * import pymysql
pymysql.install_as_MySQLdb()
* 修改settings.py文件
    * DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'secondpt',
        'USER': 'root',
        'PASSWORD': '',
        'HOST': 'localhost',
        'port': '3306',
    }
}
### 开发流程
* 配置数据库
* 定义模型类
* 执行迁移生成数据表
* 使用模型类进行增删改查(curd)操作
### ORM
* 概述
    * 对象-关系-映射
* 任务
    * 根据对象的类型生成表结构
    * 将对象、列表的操作转换为sql语句
    * 将sql语句查询到的结果转换为对象、列表
* 优点
    * 极大地减轻了开发人员的工作、不需要面对因数据库的变更而修改代码
* 图解
    * 
### 定义模型
* 模型、属性、表、字段间的关系
    * 一个模型类在一个数据库中对应一张表，在模型类中定义的属性，对应该模型对照表中的一个字段
* 定义属性
    * 详情见定义属性.txt
* 创建模型类
* 元选项
    * 在模型类中定义的Meta类，用于设置元信息
    * db_table
        * 定义数据表名，推荐使用小写字母，数据表名默认为项目名小写_类名小写
    * ordering
        * 对象的默认排序字段，获取对象的列表时使用
        * ordering = ['id']
        * ordering = ['-id']
        * 注意：排序会增加数据库的开销
        * class Students(models.Model):
    sname      = models.CharField(max_length=20)
    sgender   = models.BooleanField()
    sage         = models.IntegerField(db_column='age')
    scontend  = models.CharField(max_length=20)
    isDelete   = models.BooleanField(default=False)
    #关联外键
    sgrade     = models.ForeignKey("Grades",on_delete=models.DO_NOTHING)

    def __str__(self):
        return self.sname

    lastTime = models.DateTimeField(auto_now=True)
    createTime = models.DateTimeField(auto_now_add=True)

    class Meta:
        db_table = "students"
        ordering = ['id']
* 模型成员
    * 类属性
        * objects
            * 是Manager类型的一个对象，作用是与数据库进行交互
            * 当定义模型类时没有指定管理器，则Django为模型创建一个名为objects的管理器
        * 自定义管理器
            * class Students(models.Model):
    # 自定义模型管理器
    # 当自定义模型管理器，objects就不存在了

    stuObj = models.Manager()
            * 当为模型指定模型管理器，Django就不再为模型类生成objects模型管理器
        * 自定义管理器Manager类
            * 模型管理器Django的模型进行与数据库交互的接口，一个模型可以有多个模型管理器
            * 作用
                * 向管理器中添加额外的方法
                * 修改管理器返回的原始查询集
                    * 重写get_queryset()方法
            * 代码示例
                * class StudentsManager(models.Manager):
   def get_queryset(self):
       return super(StudentsManager, self).get_queryset().filter(isDelete=False)


class Students(models.Model):
    # 自定义模型管理器
    # 当自定义模型管理器，objects就不存在了

    stuObj = models.Manager()
    stuObj2 = StudentsManager()
    * 创建对象
        * 目的
            * 向数据库中添加数据
        * 当创建对象时，Django不会对数据库进行读写操作，当调用save（）方式时才与数据库交互，将对象保存到数据库表中
        * 注意：__init__方法已经在父类model.Model中使用，在自定义的模型中无法使用
        * 方法
            * 在模型类中添加一个类方法
                * class Students(models.Model):
    #定义一个类方法创建对象
    @classmethod
    def createStudent(cls, name, age, gender, contend, grade, lastT, createT, isD=False):
        stu = cls(sname = name, sage = age, sgender = gender, scontend = contend, sgrade = grade,
                  lastTime = lastT, createTime = createT, isDelete=isD)
        return stu
            * 在定义管理器中添加一个方法
                * class StudentsManager(models.Manager):
   def get_queryset(self):
       return super(StudentsManager, self).get_queryset().filter(isDelete=False)

   def createStudent(self, name, age, gender, contend, grade, lastT, createT, isD=False):
       stu = self.model()
       print(type(grade))
       sname=name
       sage=age
       sgender=gender
       scontend=contend
       sgrade=grade
       lastTime=lastT
       createTime=createT
       isDelete=isD
       return stu
* 模型查询
    * 概述
        * 查询集表示从数据库获得的对象集合
        * 查询集可以有多个过滤器
        * 过滤器就是一个函数，基于所给的参数限制查询集结果
        * 从sql角度来说，查询集和select语句等价，过滤器就像where条件
    * 查询集
        * 在管理器上调用过滤方法返回查询集
        * 查询集经过过滤器筛选后返回新的查询集，所以可以写成链式调用
        * 惰性执行
            * 创建查询及不会带来任何数据的访问，直到调用数据时，才会访问数据
        * 直接访问数据的情况
            * 迭代
            * 序列化
            * 与if合用
        * 返回查询集的方法称为过滤器
            * all()
                * 返回查询集中的所有数据
            * filter()
                * 返回符合条件的数据
                * filter(键=值)
                * filter(键=值，键=值)
                * filter(键=值)，filter(键=值)
            * exclude()
                * 过滤掉符合条件的值
            * order_by()
                * 排序
            * values()
                * 一条数据就是一个对象（字典），返回一个列表
        * 返回单个数据
            * get()
                * 返回一个满足条件的对象
                * 注意
                    * 如果没有找到符合条件的对象，会引发‘模型类.DoesNotExist’异常
                    * 如果找到多个对象，会引发‘模型类.MultipleObjectsReturned’异常
            * count()
                * 返回当前查询集中的对象个数
            * first()
                * 返回查询集中的第一个对象
            * last()
                * 返回查询集中的最后一个对象
            * exists()
                * 判断查询集中是否有数据，如果有返回True
        * 限制查询集
            * 查询集返回列表，可以使用下标的方法进行限制，等同于sql中的limit语句
            * studentsList = Students.stuObj2.all[0:5]
            * 注意：下标不能是负数
        * 查询集的缓存
            * 概述
                * 每个查询集都包含一个缓存，来最小化的对数据库访问
                * 在新建的查询集中，缓存首次为空，第一次对查询集求值，会发生数据缓存，django会将查询出的数据做一个缓存，并返回查询结果，以后的查询直接使用查询集的缓存
        * 字段查询
            * 概述
                * 实现了sql中的where语句，作为方法filter(),exclude(),get()的参数
                * 语法
                    * 属性名称_比较运算符=值
                * 外键
                    * 属性名_id
                * 转义
                    * like语句中使用%是为了匹配占位，匹配数据中的%（where like '\%'）
                    * filter(sname_contains='%')
            * 比较运算符
                * exact
                    * 判断，大小写敏感
                    * filter(iDelete=False)
                * contains
                    * 是否包含，大小写敏感
                    * studentsList = Students.stuObj2.filter(sname__contains="孙")
                * startswith、endswith
                    * 以value开头或结尾，大小写敏感
                    * studentsList = Students.stuObj2.filter(sname__startswith="孙")
                * 以上四个在前边加i，就表示不区分大小写iexact,icontains,istartswith,iendswith
                * isnull、isnotnull
                    * 是否为空
                    * filter(sname_isnull=False)
                * in
                    * 是否包含在范围内
                    * studentsList = Students.stuObj2.filter(pk__in=[2, 4, 6, 7, 10])
                * gt 
gte 
lt 
lte         
                    * 大于
大于等于
小于
小于等于
                    * studentsList = Students.stuObj2.filter(sage__gt=30)
                * year
month
day
week_day
hour
minute
second
                    * studentsList = Students.stuObj2.filter(lastTime__year=2018)
                * 跨关联查询
                    * 处理join查询
                        * 语法
                            * 模型类名_属性名_比较运算符
                    * #描述中带有“向方”的数据时属于哪个班级
    grade = Grades.objects.filter(students__scontend__contains="向方")
    print(grade)
                * 查询快捷
                    * pk
                        * 代表的主键
            * 聚合函数
                * 使用aggregate（）函数返回聚合函数的值
                * Avg
                * Count
                * Max
                    * from django.db.models import Max                maxAge = Students.stuObj2.aggregate(Max('sage'))
    print(maxAge)
                * Min
                * Sum
            * F对象
                * 可以使用模型的A属性与B属性进行比较
                * from django.db.models import F
def grades(request):
    g = Grades.objects.filter(ggirlnum__gt=F('gboynum'))
    print(g)
    return HttpResponse("Hello!")
                * 支持F对象的算术运算
                    * g = Grades.objects.filter(ggirlnum__gt=F('gboynum')+20)
            * Q对象
                * 概述
                    * 过滤器的方法中的关键字参数，条件为And模式
                * 需求
                    * 进行or查询
                * 解决
                    * 使用Q对象
                * studentsList = Students.stuObj2.filter(Q(pk__lte=3)|Q(sage__gt=50))
                * studentsList = Students.stuObj2.filter(Q(pk__lte=3)）
                    * 只有一个Q对象，就是用于匹配的
                * studentsList = Students.stuObj2.filter(~Q(pk__lte=3)）
                    * 取反
## 视图
### 概述
* 作用
    * 视图接受web请求，并响应web请求
* 本质
    * 视图就是一个python中的函数
* 响应
    * 网页
        * 重定向
        * 错误视图
            * 404
            * 500
            * 400
    * JSON数据
* 过程
    * 
### 配置流程
* 制定根级url配置文件
    * settings.py文件中的ROOT_URLCONF
    * ROOT_URLCONF = 'project.urls'
    * 默认实现了
* urlpatterns
    * 一个url实例的列表
    * url对象
        * 正则表达式
        * 视图名称
        * 名称
* url匹配正则的注意事项
    * 如果想要从url中获取一个值，需要对正则加小括号
    * 匹配正则前方不需要加反斜杠
    * 正则前需要加r表示字符串不转义
### 引入其它url配置
* 在应用中创建urls.py,定义本应用的url配置，在工程urls.py文件中使用include()方法
    * from django.contrib import admin
from django.conf.urls import url,include

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^', include('myApp.urls',namespace="myApp"))
]
    * from  django.conf.urls import url
from . import views
app_name = 'myApp'
urlpatterns = [
    url(r'^$', views.index,name="index"),
]
* 匹配过程
### URL的反向解析
* 概述
    * 如果在视图、模板中使用了硬编码链接，在url配置发生改变时，动态生成链接的地址
* 解决
    * 在使用链接时，通过url配置的名称，动态生成url地址
* 作用
    * 使用url模板
### 视图函数
* 定义视图
    * 本质：一个函数
    * 视图参数
        * 一个HttpRequest的实例
        * 通过正则表达式获取的参数
    * 位置
        * 一般在views.py中定义
* 错误视图
    * 404视图
        * 找不到网页(url匹配不成功)时返回
        * 在templates目录下定义404.html
            * <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>404页面</title>
</head>
<body>
    <h1>页面丢失</h1>>
    <h2>{{request_path}}</h2>>
</body>
</html>
            * request_path
                * 导致错误的网址
        * 配置settings.py
            * DEBUG
                * 如果为True，永远不会调用404.html页面
            * ALLOWED_HOSTS = ['*']
    * 500视图
        * 在视图代码中出现错误（服务器代码）
    * 400视图
        * 错误出现在客户的操作
### HttpRequest对象
* 概述
    * 视图的第一个对象就是HttpResponse对象
    * django创建的，之后调用视图时传递给视图
* 属性
    * path
        * 请求的完整路径（不包括域名和端口）
    * method
        * 表示请求的方式，常用的有GET/POST
    * encoding
        * 表示浏览器提交的数据的编码方式
            * 一般为utf-8
    * GET
        * 类似字典的对象，包含了get请求的所有参数
    * POST
        * 类似字典的对象，包含了post请求的所有参数
    * FILES
        * 类似字典的对象，包含了所有上传的文件
    * COOKIES
        * 字典，包含所有的cookie
    * session
        * 类似字典的对象，表示当前会话
* 方法
    * is_ajax()
        * 如果是通过XMLHttpRequest发起的，返回True
* QueryDict对象
    * request对象中的GET、POST都属于QueryDict对象
    * 方法
        * get(）
            * 作用：根据键获取值
            * 只能获取一个值
        * getlist()
            * 将键的值以列表的形式返回
            * 可以获取多个值
* GET属性
    * 获取浏览器传递过来给服务器的数据
    * http://127.0.0.1:8000/third/get1?a=1&b=2&c=3
        * def get1(request):
	a = request.GET.get('a')
	b = request.GET.['b']
	c = request.GET.get('c')
	return HttpResponse(a + " "+ b + " "+c)
    * http://127.0.0.1:8000/third/get2?a=1&a=2&c=3
        * def get2(request):
	a = request.GET.getlist('a')
	a1 = a[0]
	a2 = a[1]
	c = request.GET.get('c')
	return HttpResponse(a1 + " "+ a2 + " "+c)
* POST属性
    * 使用表单提交实现post请求
    * 关闭csrf
        * MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    #'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
    * def showregist(request):
    return render(request, 'myApp/regist.html')

def regist(request):
    name = request.POST.get("name")
    gender = request.POST.get("gender")
    age = request.POST.get("age")
    hobby = request.POST.get("hobby")
    print(name)
    print(gender)
    print(age)
    print(hobby)
    return HttpResponse("successful!")
### HttpResponse对象
* 概述
    * 作用：给浏览器返回数据
    * HttpRequest对象是由django创建的，HttpResponse对象由程序员创建
* 返回用法
    * 不调用模板，直接返回数据
        * from django.http import HttpResponse
def index(request):
    return HttpResponse("This is the second practice.")
    * 调用模板
        * 使用render方法
            * 原型
                * render(request,templateName,context)
            * 作用
                * 结合数据和模板，返回完整的HTML页面
            * 参数
                * request
                    * 请求体对象
                * templateName
                    * 模板路径
                * context
                    * 传递给需要渲染在模板上的数据
            * 示例
                * def index(request):
    return render(request,'myApp/index.html')
* 属性
    * content
        * 表示返回的内容类型
    * charset
        * 编码格式
    * status_code
        * 响应码状态
            * 200
            * 304
            * 404
    * content-type
        * 指定输出的MIME类型
### 方法
* init
    * 使用页面内容实例化HttpResponse对象
* write(content)
    * 以文件的形式写入
* flush()
    * 以文件的形式输出缓冲区
* set_cookie(key,value='',max_age=None,exprise=None)
* delete_cookie(key)
    * 删除cookie
    * 注意
        * 如果删除一个不存在的key，就当什么都没发生
* 子类HttpResponseRedirect
    * 功能
        * 重定向，服务器端跳转
    * 简写
        * redirect(to)
    * to推荐使用反向解析
    * #重定向
from django.http import HttpResponseRedirect
from django.shortcuts import redirect
def redirect1(request):
    #return HttpResponseRedirect('/third/redirect2')
    return redirect('/third/redirect2') 

def redirect2(request):
    return HttpResponse('我是重定向后的视图')
* 子类JsonResponse
    * 返回json数据，一般用于异步请求
    * __init__(self,data)
    * data
        * 字典对象
    * 注意
        * Content-type类型为application/json
### 状态保持
* 概述
    * http协议是无状态的，每次请求都是一次新的请求，不记得以前的请求
    * 客户端与服务器端的一次通信就是一次会话
    * 实现状态保持，在客户端或者服务器端存储有关会话的数据
    * 存储方式
        * cookie
            * 所有的数据存储在客户端，不要存敏感数据
        * session
            * 所有数据存储在服务端，在客户端用cookie存储session_id
    * 状态保持的目的
        * 在一段时间内跟踪请求者的状态，可以实现跨页面访问当前的请求者的数据
    * 注意
        * 不同的请求者之间不会共享这个数据，与请求者一一对应的
* 启用session
    * settings.py文件中
        * INSTALLED_APPS
            * 'django.contrib.sessions',
        * MIDDLEWARE
            * 'django.contrib.sessions.middleware.SessionMiddleware',
* 使用session
    * 启用session后，每个HttpRequest对象都有一个session属性，就是类似字典的对象
    * get(key,default=None)
        * 根据键获取session值
    * clear()
        * 清空所有的会话
    * flush()
        * 删除当前的会话，并删除会话的cookie
    * #session
def main(request):
    #取session
    username = request.session.get('name',"游客")
    print(username)
    return render(request, 'myApp/main.html', {'username': username})
def login(request):
    return render(request, 'myApp/login.html')
def showmain(request):
    print("hello")
    username = request.POST.get("username")
    print("username=", username)
    #存储session
    request.session['name'] = username
    return redirect('/third/main/')

from django.contrib.auth import  logout
def quit(request):
    #清除session
    #logout(request)
    #request.session.clear()
    request.session.flush()
    return redirect('/third/main/')
* 设置过期时间
    * set_expiry(value)
    * 如不设置，两星期后过期
    * 整数
        * request.session.set_expiry(10)
    * 时间对象
    * 0
        * 关闭浏览器时失效
    * None
        * 永不过期
* 存储session的位置
    * 数据库
        * 默认存储在数据库中
        * SESSION_ENGINE = 'django.contrib.sessions.backends.db'
    * 缓存
        * 只存储在本地内存中，如果丢失不能找回，比数据库快
        * SESSION_ENGINE = 'django.contrib.sessions.backends.cache'
    * 数据库和缓存
        * 优先从本地缓存中读取，读取不到再去数据库中获取
        * SESSION_ENGINE = 'django.contrib.sessions.backends.cached_db'
* 使用redis缓存session
    * #SESSION_ENGINE = 'redis_sessions.session'
SESSION_REDIS_HOST = 'localhost'
SESSION_REDIS_PORT = 6379
SESSION_REDIS_DB = 0
SESSION_REDIS_PASSWORD = ''
SESSION_REDIS_PREFIX = 'session'
## 模板
### 概述
* 模板由两部分组成
    * HTML代码
    * 逻辑控制代码
* 作用
    * 快速生成HTML页面
* 优点
    * 模板的设计实现了业务逻辑与现实内容的分离
    * 视图可以使用任何模板
* 模板处理
    * 加载
    * 渲染
### 定义模板
* 变量
    * 视图传递给模板的数据
    * 要遵守标识符规则
    * 语法
        * {{var}}
    * 注意
        * 如果使用的变量不存在，则插入的时空字符串
    * 在模板中使用点语法
        * 字典查询
        * 属性或者方法
        * 数字索引
    * 在模板中调用对象的方法
        * 注意
            * 不能传递参数
* 标签
    * 语法
        * {%tag%}
    * 作用
        * 在输出中创建文本
        * 控制逻辑和循环
    * if
        * 格式
            * {% if 表达式 %}
语句
{% endif %}
            * {% if 表达式1 %}
语句1
{% else %}
语句2
{% endif %}
            * {% if 表达式1 %}
语句1
{% elif 表达式2 %}
语句2
...
{% elif 表达式n %}
语句n
{% else %}
语句e
{% endif %}
        * 示例
            *     {% if num %}
        <h1>This is the fourth practice.</h1>
    {% endif %}
    * for
        * 格式
            * {% for 变量 in 列表 %}
语句
{% endfor %}
            * {% for 变量 in 列表 %}
语句1
{% empty %}
语句2
{% endfor %}
                * 注意
                    * 列表为空或者列表不存在时执行语句2
            * {{forloop.counter}}
                * 表示当前是第几次循环
        * 示例
            *     <ul>
        {%for student in students%}
        <li>
            {{student.sname}}--{{student.scontend}}--{{student.sgrade}}
        </li>
        {% empty %}
            <li>目前没有学生</li>>
        {%endfor%}
    </ul>
    * comment
        * 注释多行
        *     {% comment %}
        注释的内容
    {% endcomment %}
        *     {% comment %}
        <h1>This is the fourth practice.</h1>
        <h1>This is the a practice.</h1>
        {{stu.sname}}
    {% endcomment %}
    * ifequal、ifnotequal
        * 作用
            * 判断是否相等或者不等
        * 格式
            * {% ifequal 值1 值2 %}
语句
{% enifequal%}
                * 如果值1等于值2执行语句
                    *     {% ifequal 'hello' 'hello' %}
         <h1>This is the fourth practice.</h1>
    {% endifequal %}
    * include
        * 作用
            * 加载模板并以标签内的参数渲染
        * 格式
            * {% include '模板目录' 参数1 参数2 %}
    * url
        * 作用
            * 反向解析
        * 格式
            * {% url 'namespace:name' p1 p2 %} 
    * csrf_token
        * 作用
            * 用于跨站请求伪造保护
        * 格式
            * {%csrf_token%}
    * block、extends
        * 作用
            * 用于模板的继承
    * autoescape
        * 作用
            * 用于HTML转义
* 过滤器
    * 语法
        * {{var|过滤器}}
    * 作用
        * 在变量被显示前修改它
    * lower
    * upper
        *     <h1>{{str|upper}}</h1>>
    <h1>{{str}}</h1>>
    * 过滤器传递参数，参数用引号引起来
        * json
            * 格式
                * 列表|json‘#’
            * 示例
                * <h1>{{list|join:'#'}}</h1>
    * 如果一个变量没有被提供，或者值为False，空，可以使用默认值
        * default
            * 格式
                * {{var|default：‘good’}}
            * 示例
                * <h1>{{test|default:'没有'}}</h1>
    * 根据给定格式转换日期为字符串
        * date
            * 格式
                * {{dateVal|date:'y-m-d'}}
    * HTML转义
        * escape
    * 加减乘除
        *     <h1>num = {{num}}</h1>
    <h1>{{num|add:10}}</h1>
    <h1>{{num|add:-5}}</h1>
    <!--num/1*5-->
    <!--num*5-->
    <h1>{% widthratio num 1 5%}</h1>
    <!--num/5-->
    <h1>{% widthratio num 5 1%}</h1>
* 注释
    * 单行注释
        * 语法
            * {#注释内容#}
    * 多行注释
    * 子主题 3
### 反向解析
* url(r'^', include('myApp.urls', namespace="app"))
* url(r'^good/(\d+)/$', views.good, name="good"),
* <a href="{% url 'app:good' 1 %}">链接</a>
### 模板继承
* 作用
    * 模板继承可以减少页面内容的重复定义，实现页面的重用
* block标签
    * 在父模板中预留区域，子模板去填充
    * 语法
        * {% block main %}

{% endblock main %}
* extends标签
    * 继承模板，需要写在模板文件的第一行
    * 语法
        * {% extends '父模板路径' %}
* 示例
    * 定义父模板
        * <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
       #header{
           width: 100%;
           height: 100px;
           background-color: lightskyblue;
       }
        #footer{
           width: 100%;
           height: 100px;
           background-color: cornflowerblue;
       }
    </style>
</head>
<body>
    <div id="header">header</div>

    <div id="main">
        {% block main %}
        {% endblock main %}
        <hr/>
        {% block main2 %}
        {% endblock main2 %}
    </div>
    <div id="footer">footer</div>
</body>
</html>
    * 第一子模板
        * {% extends 'myApp/base.html' %}

{% block main %}
    <h1>Good job!</h1>
{% endblock main %}

{% block main2 %}
    <h1>Good Good Study!</h1>
{% endblock main2 %}
### HTML转义
* return render(request, 'myApp/index.html',{"code":"<h1>This is the fourth practice.</h1>"})  {{code}}
* 将收到的code当成普通字符串渲染
* 将收到的code当成HTML代码渲染
    * {{code|safe}}
    * {% autoescape off%}
        {{code}}
    {% endautoescape%}
### CSRF
* 跨站请求伪造
    * 某些恶意网站包含链接、表单、按钮、js，利用登录用户在浏览器中认证，从而攻击服务
* 防止CSRF
    * 在settings.py文件的MIDDLEWARE增加‘'django.middleware.csrf.CsrfViewMiddleware',’
    * {% csrf_token %}
### 验证码
* 作用
    * 在用户注册、注册页面的时候使用，为了防止暴力请求，减轻服务器的压力
    * csrf的一种
## Django高级扩展
### 静态文件
* css,js,json文件，图片，字体文件等
* 配置settings.py文件
    * STATIC_URL = '/static/'
#普通文件用
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static')
]
* {% load static from staticfiles %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>首页</title>
    <link rel="stylesheet" type="text/css"
    href="{% static 'myApp/css/style.css' %}"/>
   <script type="text/javascript"
            src="/static/myApp/js/jquery-3.3.1.min.js">
    </script>
    <script type="text/javascript"
            src="/static/myApp/js/fifth.js">
    </script>
</head>
<body>
    <h1>This is the fifth practice.</h1>
    <img src="/static/myApp/img/1.png"/>
    <img src="{% static 'myApp/img/1.png' %}"/>
</body>
</html>
### 中间件
* 概述
    * 一个轻量级、底层的插件，可以介入Django的请求和响应
* 本质
    * 一个Python类
* 方法
    * __init__
        * 不需要传参数，服务器响应第一个请求的时候自动调用，用于确定是否启用该中间件
    * process_request(self,request)
        * 在执行视图之前被调用(分配url匹配视图前)，每个请求都会调用，返回None或者HttpResponse对象
    * process_view(self,request,view_func,view_args,view_kwargs)
        * 调用视图之前执行，每个请求都会调用，返回None或者HttpResponse对象
    * process_template_response(self,request,response)
        * 在试图刚好执行完后调用，每个请求都会调用，返回None或者HttpResponse对象
        * 使用render
    * process_response(self,request,response)
        * 所有响应返回浏览器之前调用，每个请求都会调用，返回None或者HttpResponse对象
    * process_exception(self,request,exception)
        * 当视图跑出异常时调用
* 执行位置
    * 
* 自定义中间件
    * 工程目录下middleware目录下创建myApp目录
    * 创建一个python文件
    * from django.utils.deprecation import MiddlewareMixin
class myMiddle(MiddlewareMixin):
    def process_request(self,request):
        print("get参数为：",request.GET.get("a"))
* 使用自定义中间件
    * 配置settings.py文件
        * MIDDLEWARE中添加
            * 'middleware.myApp.myMiddle.myMiddle'
### 上传图片
* 概述
    * 文件上传时，文件数据存储在request.FILES属性中
    * 注意：form要上传文件需要加enctype="multipart/form-data"
    * 上传文件必须是post请求
* 存储路径
    * 在static目录下创建upfile目录用于存储接收上传的文件
    * 配置settings.py文件
        * MEDIA_ROOT=os.path.join(BASE_DIR, r'static\upfile')
* 代码示例
    * <body>
    <form method="post" action="=/savefile/" enctype="multipart/form-data">
        <input type="file" name="file"/>
        <input type="submit" value="上传"/>
    </form>>
</body>
    * def upfile(request):
    return render(request, 'myApp/upfile.html')

import os
from django.conf import settings
def savefile(request):

    if request.method == 'POST':
        f = request.FILES["file"]
        #文件在服务器的路径
        filepath = os.path.join(settings.MEDIA_ROOT, f.name)
        with open(filepath, 'wb') as fp:
            for info in f.chunks():
                fp.write(info)
        return HttpResponse("上传成功")

    else:
        return HttpResponse("上传失败")
### 分页
* paginator对象
    * 创建对象
        * 格式
            * paginator（列表，整数）
        * 返回值
            * 返回的分页对象
    * 属性
        * count
            * 对象总数
        * num_pages
            * 页面总数
        * page_range
            * 页码列表
            * [1,2,3,4,5]
            * 页码从1开始
    * 方法
        * page(num)
            * 获得一个page文件，如果提供的页码不出现会出现“InvalidPage“异常
    * 异常
        * InvalidPage
            * 当向page()传递的是无效的页码时抛出
        * PageNotAnInteger
            * 当向page()传递的不是一个整数时抛出
        * EmptyPage
            * 当向page()传递一个有效值，但是该页面上没有数据时抛出
* page对象
    * 创建对象
        * paginator对象的page()方法返回得到page对象
        * 不需要手动创建
    * 属性
        * object_list
            * 当前页上所有的数据(对象)列表
        * number
            * 当前的页码值
        * paginator
            * 当前page对象关联的paginator对象
    * 方法
        * has_next()
            * 判断是否有下一页，如果有返回True
        * has_previous()
            * 判断是否有上一页，如果有返回True
        * has_other_pages()
            * 判断是否有上一页或下一页，如果有返回True
        * next_page_number()
            * 返回下一页的页码，如果下一页不存在抛出InvalidPage异常
        * previous_page_number()
            * 返回上一页的页码，如果上一页不存在抛出InvalidPage异常
        * len()
            * 返回当前页的数据(对象)个数
    * Paginator对象与page对象的关系
        * 
    * 代码示例
        * url(r'^studentpage/(\d+)/$', views.studentpage),
        * from .models import Students
from  django.core.paginator import Paginator
def studentpage(request, pageid):
    #所有学生列表
    allList = Students.objects.all()

    paginator = Paginator(allList, 6)
    page = paginator.page(pageid)

    return render(request,'myApp/studentpage.html', {'students':page})
        * <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>学生分页显示</title>
</head>
<body>
    <ul>
        {% for stu in students %}
        <li>
            {{stu.sname}}--{{stu.scontend}}--{{stu.sgrade}}
        </li>
        {%endfor%}
    </ul>

    <ul>
        {% for index in students.paginator.page_range %}
            {% if index == students.number %}
                <li>
                    {{index}}
                </li>
            {% else %}
            <li>

            <a href="/studentpage/{{index}}"/>{{index}}</a>
            </li>
            {% endif %}
        {% endfor%}
    </ul>
</body>
</html>
### ajax
* 需要动态生成，请求json数据
* <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript"
            src="/static/myApp/js/jquery-3.3.1.min.js">
    </script>


</head>
<body>
    <h1>学生信息列表</h1>
    <button id="btn">显示学生信息</button>
    <script type="text/javascript"
            src="/static/myApp/js/fifth.js">
    </script>
</body>
</html>
* $(document).ready(function () {
    document.getElementById("btn").onclick =
function () {
        $.ajax({
            type:"get",
            url:"/studentsinfo/",
            dataType:"json",
            success:function (data, status) {
                console.log(data)
                var d = data["data"]

                for(var i = 0;i < d.length;i++){
                    document.write('<p>'+d[i][0]+'</p>')

                }
            }
            })
}
})
* def ajaxstudents(request):
    return render(request, 'myApp/ajaxstudents.html')
from django.http import  JsonResponse
def studentsinfo(request):
    stus = Students.objects.all()
    list = []
    for stu in stus:
        list.append([stu.sname,stu.sage])

    return JsonResponse({"data":list})
### 富文本
* pip install django-tinymce
* 在站点中使用
    * 配置settings.py文件
        * INSTALLED_APPS添加
            * 'tinymce',
        * 增加
            * #富文本
TINYMCE_DEFAULT_CONFIG = {
    'theme' : 'advanced',
    'width' : 600,
    'height': 400,
}
    * 创建一个模型类
        * from tinymce.models import  HTMLField
class Text(models.Model):
    str = HTMLField()
    * 配置站点
        * from .models import Text
admin.site.register(Text)
* 在自定义视图中使用
    * <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>富文本</title>
    <script type="text/javascript"
            src="/static/tiny_mce/tiny_mce.js">
    </script>
    <script type="text/javascript">
        tinyMCE.init({
            'mode' : 'textareas',
            'theme' : 'advanced',
            'width' : 800,
            'height' :600,
            })
    </script>
</head>
<body>
    <form>
        <textarea name="str">HelloWorld!</textarea>
        <input type="submit" value="提交">
    </form>
</body>
</html>
### celery
* [http://docs.jinkan.org/docs/celery/](http://docs.jinkan.org/docs/celery/)
* 问题
    * 用户发起request,并且要等待response返回，但是在视图中有一些耗时的操作，导致用户会等待很长时间才能接受response，这样用户体验很差
    * 网站每隔一段时间要同步一次数据，但是http请求是需要触发的
* 解决
    * celery来解决
        * 将耗时的操作放到celery中执行
        * 使用celery定时执行
* celery
    * 任务task
        * 本质是一个python函数，将耗时操作封装成一个函数
    * 队列queue
        * 将要执行的任务放队列里
    * 工人worker
        * 负责执行队列中的任务
    * 代理broker
        * 负责调度，在部署环境中使用redis
* 安装
    * pip install celery
    * pip install celery-with-redis
    * pip install django-celery
* 配置settings.py
    * INSTALLED_APPS
        * 'djcelery',
    * #celery
import djcelery
djcelery.setup_loader()#初始化
BROKER_URL='Redis://liying@127.0.0.1:6379/0'
CELERY_IMPORTS=('myApp.task')
* 在应用目录下创建task.py文件
* 迁移，生成celery需要的数据库表
    * python manage.py migrate
* 在工程目录下的project目录下创建celery.py文件
    * from __future__ import absolute_import

import os
from celery import  Celery
from django.conf import  settings

os.environ.setdefault('DJANGO_SETTINGS_MODULE','whthas_home.settings')

app = Celery('portal')

app.config_from_object('django.conf:setting')
app.autodiscover_tasks(lambda :settings.INSTALLED_APPS)

@app.task(bind=True)
def debug_task(self):
    print('Request:{0|r}'.format(self.request))
* 在工程目录下的project目录下的__init__.py文件中添加
    * from .celery import app as celery_app
* 创建celery.html文件
    * <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>celery</title>
</head>
<body>
    <h1>I AM CELERY.</h1>
</body>
</html>

*XMind: ZEN - Trial Version*