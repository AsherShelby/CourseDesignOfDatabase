# 第1章 设计背景 <div>
随着互联网的普及和社交媒体的兴起，社交平台已成为人们分享信息、建立社交关系和交流互动的重要平台。为了有效地管理用户、帖子、评论、点赞等数据，并提供稳定和高效的用户体验，设计一个功能强大的数据库管理系统是至关重要的。<div>
  
# 第2章 需求分析<div>
 ## 2.1 功能需求<div>
  ### 2.1.1 用户数据管理<div>
社交平台涉及大量用户数据的收集、存储和管理。用户表是数据库的核心组成部分，记录了用户的基本信息，如用户名、密码、电子邮件和注册日期。通过这些信息，用户可以登录平台、建立个人资料，并与其他用户进行互动。<div>
  ### 2.1.2 社交关系管理<div>
社交平台的成功在于构建用户之间的社交关系网络。好友关系表记录了用户之间的好友关系，以便用户可以轻松地查找和互动。通过用户ID和好友ID，可以建立和管理用户之间的好友关系。<div>
  ### 2.1.3 社交互动数据<div>
社交平台的核心功能之一是用户之间的互动。帖子表是存储用户发表的内容的地方，包括文本、图片、链接等形式。帖子可以通过帖子ID与用户表进行关联，以确定发帖用户。用户可以在帖子下方发表评论，评论表记录了评论内容、评论用户和被评论的帖子。此外，点赞表用于记录用户对帖子的点赞操作，以及相关的用户和帖子信息。<div>
 ## 2.2 数据字典<div>
用户表（User）：<div>
UserID：用户ID（主键）（INT） - 用户的唯一标识符<div>
Username：用户名（VARCHAR(255)） - 用户的用户名<div>
Password：密码（VARCHAR(255)） - 用户的密码<div>
Email：邮箱（VARCHAR(255)） - 用户的邮箱地址<div>
RegistrationDate：注册日期（DATE） - 用户的注册日期<div>

帖子表（Post）：<div>
PostID：帖子ID（主键）（INT） - 帖子的唯一标识符<div>
UserID：用户ID（INT） - 发布该帖子的用户ID<div>
Content：内容（TEXT） - 帖子的内容<div>
PublishDate：发布日期（DATE） - 帖子的发布日期<div>

评论表（Comment）：<div>
CommentID：评论ID（主键）（INT） - 评论的唯一标识符<div>
PostID：帖子ID（INT） - 被评论的帖子ID<div>
UserID：用户ID（INT） - 发表该评论的用户ID<div>
Content：内容（TEXT） - 评论的内容<div>
CommentDate：评论日期（DATE） - 评论的日期<div>

点赞表（Likes）：<div>
LikeID：点赞ID（主键）（INT） - 点赞的唯一标识符<div>
PostID：帖子ID（INT） - 被点赞的帖子ID<div>
UserID：用户ID（INT） - 点赞的用户ID<div>
LikeDate：点赞日期（DATE） - 点赞的日期<div>

好友关系表（Friendship）：<div>
FriendshipID：好友关系ID（主键）（INT） - 好友关系的唯一标识符<div>
UserID1：用户ID1（INT） - 用户1的ID<div>
UserID2：用户ID2（INT） - 用户2的ID<div>
Status：状态（ENUM('Pending', 'Accepted')） - 好友关系的状态（Pending表示待处理，Accepted表示已接受）<div>

个人资料表（Profile）：<div>
UserID：用户ID（主键）（INT） - 用户的唯一标识符<div>
FirstName：名字（VARCHAR(10)） - 用户的名字<div>
LastName：姓氏（VARCHAR(10)） - 用户的姓氏<div>
Gender：性别（VARCHAR(10)） - 用户的性别<div>
BirthDate：出生日期（DATE） - 用户的出生日期<div>
Bio：个人简介（TEXT） - 用户的个人简介<div>
# 第3章 系统设计<div>
 ## 3.1 功能设计： <div>
   ### 3.1.1 用户功能：<div>
•	用户注册和登录：用户可以通过填写用户ID、密码来注册平台账号，并通过用户ID、邮箱和密码来登录平台。<div>
•	用户个人资料管理：用户可以查看和修改自己的个人资料，包括性别、个性签名等。<div>
•	用户好友关系管理：用户可以通过搜索其他用户的用户名或电子邮件来添加好友，并可以查看自己的好友列表，并可以删除自己的好友。<div>
•	用户发帖功能：用户可以在平台上发表文本形式的帖子，同时也可以删除自己发表过的帖子。<div>
•	用户评论功能：用户可以在其他用户和自己发表的帖子下方发表评论。<div>
•	用户点赞功能：用户可以对其他用户发表的帖子进行点赞。<div>
•	用户动态浏览功能：用户可以浏览自己和好友发表的最新帖子，并可以对其进行评论和点赞。<div>
### 3.1.2 系统业务流程图：<div>
![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/5413d305-b2d3-4089-9c8f-62d681ddd38c)
### 3.2 概念结构设计<div>
将需求分析得到的用户需求抽象为信息结构，分析数据字典中数据字典间内在语义关联，并将其抽象表示为数据的概念模式，从而能真实，充分地反应真实世界，包括事物和事物之间的联系，能满足用户对数据的处理需求，是现实世界的一个真实模型，易于理解，从而可以用它和不熟悉计算机的人交换意见，且易于更改。方法：首先分析整个系统中涉及到的实体，得到局部的ER图。然后分析这些实体之间的关系，进行连接从而得到。<div>
  ![E-R图 drawio](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/d7043a7c-4b2c-4e11-876c-ebcfa91347b8)

 ## 3.3 实体与联系<div>
  ### 3.3.1 实体<div>
用户（User）：<div>
UserID（用户ID），<div>
Username（用户名），<div>
Password（密码），<div>
Email（邮箱）<div>
  
消息（Message）：<div>
MessageID（消息ID），<div>
SenderID（发送者ID），<div>
ReceiverID（接收者ID），<div>
Content（消息内容），<div>
SendTime（发送时间）<div>
  
帖子（Post）：<div>
PostID（帖子ID），<div>
UserID（用户ID），<div>
Content（内容），<div>
PostTime（发布时间）<div>
  
评论（Comment）：<div>
CommentID（评论ID），<div>
UserID（用户ID），<div>
PostID（帖子ID），<div>
Content（内容），<div>
CommentTime（评论时间）<div>
  
点赞（Like）：<div>
LikeID（点赞ID），<div>
UserID（用户ID），<div>
PostID（帖子ID），<div>
LikeTime（点赞时间），<div>
  
好友关系（Friendship）：<div>
FriendshipID（好友关系ID），<div>
UserID1（用户ID1），<div>
UserID2（用户ID2），<div>
FriendshipDate（建立好友关系的日期），<div>
  
个人资料（Profile）：<div>
UserID（用户ID），FirstName（名字），<div>
LastName（姓氏），<div>
Gender（性别），<div>
BirthDate（出生日期），<div>
Bio（个人简介），<div>
  
  ### 3.1.2 联系：<div>
用户（User）和消息（Message）之间的联系：<div>
一对多关系：一个用户可以发送多个消息，但一条消息只能由一个用户发送。<div>
一对多关系：一个用户可以接收多条消息，但一条消息只能发送给一个用户。<div>
  
用户（User）和帖子（Post）之间的联系：<div>
一对多关系：一个用户可以发布多个帖子，但一个帖子只能由一个用户发布。<div>
  
用户（User）和评论（Comment）之间的联系：<div>
一对多关系：一个用户可以发表多个评论，但一个评论只能由一个用户发表。<div>
一对多关系：一个帖子可以有多个评论，但一个评论只属于一个帖子。<div>
  
用户（User）和点赞（Like）之间的联系：<div>
一对多关系：一个用户可以点赞多个帖子，但一个点赞只属于一个用户和一个帖子。<div>
  
用户（User）和好友关系（Friendship）之间的联系：<div>
多对多关系：一个用户可以有多个好友，一个好友也可以是多个用户的好友。<div>
  
用户（User）和个人资料（Profile）之间的联系：<div>
一对一关系：一个用户对应一个个人资料。<div>
  
  ## 3.3 逻辑结构设计<div>
   ### 3.1.3 逻辑关系图<div>
   根据整个系统的特性，可以设计出如下数据库逻辑关系图：<div>
  
![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/15fa68c3-2e9d-4c1e-994c-ce4d3c874819)
  
用户的个人信息：用户ID，用户名，密码，电子邮件，注册日期<div>
 User（UserID, Username, Password, Email, RegistrationDate）<div>
  
帖子的信息：帖子ID，用户ID，内容，发表日期
Post（PostID, UserID, Content, PublishDate）<div>
  
评论的信息：评论ID，帖子ID，用户ID，内容，评论日期
Comment（CommentID, PostID, UserID, Content, CommentDate）<div>
  
点赞信息：点赞ID，帖子ID，用户ID，点赞日期
Likes（LikeID, PostID, UserID, LikeDate）<div>
  
关系信息：关系ID，用户ID1，用户ID2，状态
Friendship（FriendshipID, UserID1, UserID2, Status）<div>
  
个人资料：用户ID，姓氏，名字，性别，生日，个性签名
Profile（UserID, FirstName, LastName, Gender, BirthDate, Bio）<div>
  
消息信息：发送者ID，接收者ID，消息内容，发送时间
Message（SenderID，ReceiverID，Content，SendTime）<div>

#第4章 系统实现<div>
 ## 4.1 数据库表的定义<div>
  创建用户表（User）：<div>
CREATE TABLE User (<div>
  UserID INT PRIMARY KEY AUTO_INCREMENT,<div>
  Username VARCHAR(255) NOT NULL,<div>
  Password VARCHAR(255) NOT NULL,<div>
  Email VARCHAR(255) NOT NULL,<div>
  RegistrationDate DATE NOT NULL<div>
);<div>

  创建帖子表（Post）：<div>
CREATE TABLE Post (<div>
  PostID INT PRIMARY KEY AUTO_INCREMENT,<div>
  UserID INT NOT NULL,<div>
  Content TEXT NOT NULL,<div>
  PublishDate DATE NOT NULL,<div>
  FOREIGN KEY (UserID) REFERENCES User(UserID)<div>
);<div>

  创建评论表（Comment）：<div>
CREATE TABLE Comment (<div>
  CommentID INT PRIMARY KEY AUTO_INCREMENT,<div>
  PostID INT NOT NULL,<div>
  UserID INT NOT NULL,<div>
  Content TEXT NOT NULL,<div>
  CommentDate DATE NOT NULL,<div>
  FOREIGN KEY (PostID) REFERENCES Post(PostID),<div>
  FOREIGN KEY (UserID) REFERENCES User(UserID)<div>
);<div>

创建点赞表（Like）：<div>
CREATE TABLE Like (<div>
  LikeID INT PRIMARY KEY AUTO_INCREMENT,<div>
  PostID INT NOT NULL,<div>
  UserID INT NOT NULL,<div>
  LikeDate DATE NOT NULL,<div>
  FOREIGN KEY (PostID) REFERENCES Post(PostID),<div>
  FOREIGN KEY (UserID) REFERENCES User(UserID)<div>
);<div>
  
创建好友关系表（Friendship）：<div>
CREATE TABLE Friendship (<div>
  FriendshipID INT PRIMARY KEY AUTO_INCREMENT,<div>
  UserID1 INT NOT NULL,<div>
  UserID2 INT NOT NULL,<div>
  Status ENUM('Pending', 'Accepted') NOT NULL,<div>
  FOREIGN KEY (UserID1) REFERENCES User(UserID),<div>
  FOREIGN KEY (UserID2) REFERENCES User(UserID)<div>
);<div>

创建个人资料表（Profile）：<div>
CREATE TABLE Profile (<div>
  ProfileID INT PRIMARY KEY AUTO_INCREMENT,<div>
  UserID INT NOT NULL,<div>
  FirstName VARCHAR(255),<div>
  LastName VARCHAR(255),<div>
  Gender VARCHAR(10),<div>
  BirthDate DATE,<div>
  Bio TEXT,<div>
  FOREIGN KEY (UserID) REFERENCES User(UserID)<div>
);<div>

 ## 4.2 各类功能实现<div>
用户功能（注册、注销、更新信息、查询）：<div>

![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/2ddc9e15-a073-401e-a730-cb1007f16a82)
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/f7a3e50a-f5a2-45e1-8b66-2fc23a93a2c8)<div>

![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/5b8746b8-a939-44b4-b9c3-2839cedc2f30)<div>
好友功能（添加、删除、更新、查找）：<div>
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/8a7fb61a-ab66-4431-b9d5-c66d2237029f)
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/5960e8b0-7654-4f82-b388-2ef63183ef58)<div>
信息的各类操作（发送、删除、查找）：<div>
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/3642a39d-5280-411a-ac12-f2be9f52ba4a)
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/13b4f22f-5d3c-4ff6-8838-b0e74c99e6d8)<div>
个人资料更新功能：<div>
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/dca9cd9d-808a-4805-8a5c-17c26a49dba2)<div>
帖子操作（发表、删除、更新、查询）：<div>
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/b3a8e99e-8d85-430b-b0ca-2bad5e15a61d)
![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/c36af77c-bae0-4593-928d-8f30867ea888)<div>

  
#第5章 系统测试<div>
 ## 5.1注册、登录功能测试：<div>
 ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/08da92ce-468f-419e-b45f-69bd4e7f0c62)
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/077d5e6a-6c75-4ae8-ba60-1665a15c8725)<div>
可以看见数据库里已经更新用户信息：<div>
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/a3b9536f-fb75-489f-8936-e9b53576aae5)<div>
注册已完成，已经可以登录：<div>
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/f2d1fd75-47a5-445c-8364-b87f97de5abc)<div>
 ## 5.2 好友功能、消息功能、帖子功能测试<div>
 在好友界面添加好友：<div>
![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/997a6157-a7a4-4f68-9ac4-7ac7d91e3879)<div>
可以看见数据库里好友状态更新：<div>
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/dd90af30-35a2-43bc-972a-3788021ca6f0)<div>
在好友界面向好友发消息：<div>
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/8cda2187-be04-46cf-8988-a35d00a21d74)<div>
可以看见数据库里消息表更新：<div>
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/0d7196cc-2b0a-4605-9700-d6174ee88133)<div>
打开帖子界面，发一个帖子，可以看见好友和自己发的帖子：<div>
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/56cd6ad1-cf6e-4f07-bc67-31c0eda8fbac)<div>
数据库里记录了帖子的各种信息<div>
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/180d1597-4e90-4b2c-a115-bdab5e31651b)<div>
在帖子界面选一个帖子进行点赞、评论操作：<div>
![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/07e7d354-a93d-47b0-8aff-ff8d93df679e)<div>
![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/d84dceb7-b5a4-47ef-a3dd-6a36c943d657)<div>
可以看见数据库里点赞表、评论表里更新了信息：<div>
  ![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/d4e24e74-16df-4e35-b7ca-9a263453bce3)
![image](https://github.com/2249899756/CourseDesignOfDatabase/assets/94681217/d3554dc9-fe61-47a5-b4ac-5e44dcd84cfc)<div>
 ## 5.3 测试结论<div>
经过各项功能测试，社交平台数据管理系统各项功能都正常，能够达到预期效果。但是，这个数据库管理系统还存在一些问题：<div>
1、在一些问题的处理和考虑的方面存在很大的缺陷和漏洞，希望在进一步的学习中能更好处理好相关问题。这次课题设计不能堪称完美，甚至来说还很不健全。<div>
2、在对数据库进行设计的过程中，结构比较简单，不能够应对是否能复杂的情况，只能对用户的简单信息进行操作。另外，在安全性方面做得也不够完善，主要原因在于设计的重点是功能的正常执行，而不是在每一个细节做到完美。另外，执行虚度方面没有做出专门的优化。因此，这个数据库系统需要我在以后相信的去完成每一个细节。但我会在以后的时间里去尽量的完善它，不断的对它进行升级和完善，解决系统可能会出现的。<div>
# 第6章 总结<div>
在课设过程中，遇到了一些挑战，同时也会有一些宝贵的收获和经验。下面是我可能存在的不足和收获的例子：<div>
不足：<div>
数据库设计不完善：在初期的设计阶段，可能存在对数据库的需求分析不充分或理解不准确的情况。这可能导致数据库结构的设计不够完善，难以满足实际需求，或者在后续阶段需要频繁地修改数据库结构。<div>
性能问题：在设计数据库时，可能未充分考虑到数据的规模和访问模式，导致数据库性能不佳。这可能包括查询速度慢、响应时间延迟等问题，需要通过优化查询语句、建立适当的索引等方式来改进性能。<div>
安全性考虑不足：在课设过程中，可能没有充分考虑到数据库的安全性。例如，缺乏合适的访问控制机制，导致数据被未经授权的用户访问或篡改。<div>

收获：<div>
数据库设计经验：通过课设，我将获得实际的数据库设计经验。我掌握了如何进行需求分析、设计数据库模式、优化查询性能等方面的技能，这对我日后在实际项目中设计数据库将会有很大帮助。<div>
数据库管理技能：通过实践，你将了解和掌握数据库管理系统的各种功能和工具。我学会了如何创建和管理数据库、执行查询、备份和恢复数据等操作，这对我日后从事数据库相关工作非常重要。<div>
问题解决能力：在课设过程中，我可能会遇到各种问题和挑战，例如数据完整性的保证、性能优化、安全性等方面的问题。通过解决这些问题，让我成功得提高了自己解决问题的能力和分析能力。<div>
总体而言，课设是一个宝贵的学习机会，可以将课堂上学到的知识应用到实践中，同时也可以提升我的技术能力和解决问题的能力。尽管可能存在不足，但通过总结经验教训，我相信可以在今后的项目中做得更好。<div>


  








